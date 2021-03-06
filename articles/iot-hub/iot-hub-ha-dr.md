---
title: Azure IoT Hub の高可用性とディザスター リカバリー | Microsoft Docs
description: ディザスター リカバリー機能を持つ高可用性 Azure IoT ソリューションの構築を支援する Azure および IoT Hub 機能について説明します。
author: fsautomata
manager: ''
ms.service: iot-hub
services: iot-hub
ms.topic: conceptual
ms.date: 10/13/2017
ms.author: elioda
ms.openlocfilehash: 428209defa554599c01789e6f2a8b62f155b0f2f
ms.sourcegitcommit: 266fe4c2216c0420e415d733cd3abbf94994533d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/01/2018
ms.locfileid: "34633708"
---
# <a name="iot-hub-high-availability-and-disaster-recovery"></a>IoT Hub の高可用性とディザスター リカバリー
IoT Hub は、Azure サービスとして、Azure リージョン レベルの冗長性を使用して高可用性 (HA) を提供します。その際、ソリューションによる追加操作は必要ありません。 さらに、Microsoft Azure Platform には、ディザスター リカバリー (DR) 機能または複数のリージョンにわたる可用性を備えたソリューションを構築するのに役立つ機能が用意されています。 複数のリージョンにわたるグローバルな高可用性をデバイスまたはユーザーに提供する場合は、これらの Azure DR 機能を利用してください。 ビジネス継続性および障害復旧のための Azure の組み込み機能については、[Azure のビジネス継続性テクニカル ガイダンス](../resiliency/resiliency-technical-guidance.md)に関する記事を参照してください。 [Azure アプリケーションの障害復旧と高可用性][Disaster recovery and high availability for Azure applications]に関するページでは、HA と DR を実現するための Azure アプリケーションの戦略に関するアーキテクチャのガイダンスを確認できます。

## <a name="azure-iot-hub-dr"></a>Azure IoT Hub DR
IoT Hub では、リージョン内の HA だけでなく、ユーザーの介入を必要としないディザスター リカバリーのためのフェールオーバー メカニズムを実装します。 IoT Hub DR は自己開始型のメカニズムであり、目標復旧時間 (RTO) は 2 ～ 26 時間で、回復ポイントの目標 (RPO) は次のとおりです。

| 機能 | RPO |
| --- | --- |
| レジストリと通信操作に対するサービス可用性 |CName が失われる可能性あり |
| ID レジストリの ID データ |0 ～ 5 分間のデータ損失 |
| デバイスからクラウドへのメッセージ |すべての未読メッセージが失われる |
| 操作の監視メッセージ |すべての未読メッセージが失われる |
| クラウドからデバイスへのメッセージ |0 ～ 5 分間のデータ損失 |
| クラウドからデバイスへのフィードバックのキュー |すべての未読メッセージが失われる |
| デバイス ツイン データ |0 ～ 5 分間のデータ損失 |
| 親とデバイスのジョブ |0 ～ 5 分間のデータ損失 |

## <a name="regional-failover-with-iot-hub"></a>IoT Hub での地域フェールオーバー
IoT ソリューションでのデプロイ トポロジの詳しい説明はこの記事の範囲外です。 この記事では、高可用性とディザスター リカバリーを実現するために、*地域フェールオーバー* デプロイ モデルについて検討します。

地域フェールオーバー モデルの場合、ソリューション バック エンドは主に 1 つのデータセンターの場所で実行されます。 セカンダリ IoT ハブとバック エンドは、別のデータセンターの場所にデプロイされています。 プライマリ データセンターの IoT ハブに障害が発生した場合、またはデバイスからプライマリ データセンターへのネットワーク接続が中断された場合、デバイスはセカンダリ サービス エンドポイントを使用します。 1 つのリージョン内ではなく、リージョン間フェールオーバー モデルを実装することで、ソリューションの可用性を改善できます。 

大まかに言えば、IoT Hub で地域フェールオーバー モデルを実装するには、以下を行う必要があります。

* **セカンダリ IoT Hub とデバイス ルーティングのロジック**: プライマリ リージョンでサービスの中断が発生した場合、セカンダリ リージョンへのデバイスの接続を開始する必要があります。 関連するサービスのほとんどが状態認識型の場合、ソリューションの管理者がリージョン間のフェールオーバー プロセスをトリガーするのはよくあることです。 プロセスの制御を維持しながら、新しいエンドポイントをデバイスに伝達する最善の方法は、"*コンシェルジェ*" サービスで、現在のアクティブなエンドポイント サービスがないかどうかを定期的にチェックすることです。 コンシェルジェ サービスは Web アプリケーションで、DNS リダイレクト手法 ([Azure Traffic Manager][Azure Traffic Manager] など) を使用してレプリケートされ、到達可能な状態が保持されます。
* **ID レジストリ レプリケーション**: 使用するには、ソリューションに接続できるすべてのデバイス ID をセカンダリ IoT ハブに格納する必要があります。 ソリューションでは、デバイス ID の geo レプリケートされたバックアップを保持し、デバイスのアクティブなエンドポイントを切り替える前に、そのバックアップをセカンダリ IoT ハブにアップロードしなければなりません。 IoT Hub のデバイス ID エクスポート機能は、この点で役に立ちます。 詳細については、「[IoT Hub 開発者ガイド - ID レジストリ][IoT Hub developer guide - identity registry]」を参照してください。
* **マージ ロジック**: 再度プライマリ リージョンが使用可能になった時点で、セカンダリ サイトで作成されたすべての状態とデータをプライマリ リージョンに移行する必要があります。 状態とデータは主にデバイス ID およびアプリケーション メタデータと関連しており、プライマリ IoT ハブとマージする必要があります。また、プライマリ リージョンにある他のアプリケーション固有のストアとのマージが必要になることもあります。 この手順を簡単にするには、べき等操作を使用する必要があります。 べき等操作により、最終的に一貫性のあるイベント分布だけでなく、イベント重複や順不同配信の副次的な影響を最小限に抑えられます。 また、アプリケーション ロジックは、潜在的な不整合を許容するように、あるいは "少しばかり" 時代遅れに設計する必要があります。 これは、回復ポイントの目標 (RPO) に基づいてシステムが "回復する" ために追加の時間がかかるためです。

## <a name="next-steps"></a>次の手順
Azure IoT Hub についてさらに学習するには、次のリンクを使用してください。

* [IoT Hubs の使用 (チュートリアル)][lnk-get-started]
* [Azure IoT Hub とは][What is Azure IoT Hub?]

[Disaster recovery and high availability for Azure applications]: ../resiliency/resiliency-disaster-recovery-high-availability-azure-applications.md
[Azure Business Continuity Technical Guidance]: https://azure.microsoft.com/documentation/articles/resiliency-technical-guidance/
[Azure Traffic Manager]: https://azure.microsoft.com/documentation/services/traffic-manager/
[IoT Hub developer guide - identity registry]: iot-hub-devguide-identity-registry.md

[lnk-get-started]: iot-hub-csharp-csharp-getstarted.md
[What is Azure IoT Hub?]: iot-hub-what-is-iot-hub.md
