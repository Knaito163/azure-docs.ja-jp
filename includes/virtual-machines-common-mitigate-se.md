---
title: インクルード ファイル
description: インクルード ファイル
services: virtual-machines
author: cynthn
ms.service: virtual-machines
ms.topic: include
ms.date: 05/21/2018
ms.author: cynthn;kareni
ms.custom: include file
ms.openlocfilehash: 49db6b625a9e4fc46fe414eb723dfccd890efd64
ms.sourcegitcommit: 266fe4c2216c0420e415d733cd3abbf94994533d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/01/2018
ms.locfileid: "34677361"
---
**ドキュメントの最終更新日**: 2018 年 5 月 21 日午後 3:00 (PST)。

予測実行のサイドチャネル攻撃として知られる [CPU 脆弱性の新しいクラス](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/ADV180002)の最近の公開では、顧客がよりわかりやすい説明を求めていることがわかりました。  

Microsoft は、クラウド サービス全体に軽減策を展開しました。 Azure を実行し、顧客ワークロードを互いに分離するインフラストラクチャは保護されています。  つまり、Azure を使用する他の顧客は、これらの脆弱性を使用してアプリケーションを攻撃することはできません。

さらに、Azure では、[メモリ保持メンテナンス](https://docs.microsoft.com/azure/virtual-machines/windows/maintenance-and-updates#memory-preserving-maintenance)の使用を可能な限り拡大して、ホストが更新されたり、VM が既に更新されているホストに移動されたりする間、VM を最大 30 秒間一時停止させます。  さらに、メモリ保持メンテナンスによって顧客への影響が最小限に抑えられ、再起動する必要がなくなります。  Azure では、ホストに対してシステム全体の更新を行うときに、これらの方法が使用されます。

> [!NOTE] 
2018 年 5 月 21 日に、Google Project Zero と Microsoft は、Speculative Store Bypass と呼ばれる予測実行サイド チャネルの脆弱性の新しいサブクラスを発表しました。 徹底的な防御のための追加の防御手段が Microsoft クラウド インフラストラクチャ全体にわたって導入されました。これは予測実行の脆弱性を直接解決します。 詳細については、以下を参照してください: https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/ADV180012 
>
> Intel Corporation は、2018 年 2 月下旬に「[Microcode Revision Guidance](https://newsroom.intel.com/wp-content/uploads/sites/11/2018/03/microcode-update-guidance.pdf)」(マイクロコード リビジョン ガイダンス) の Intel 製マイクロコードのリリース状況を更新しました。このリリースにより、[Google Project Zero](https://googleprojectzero.blogspot.com/2018/01/reading-privileged-memory-with-side.html) から開示された最近の脆弱性に対する安定性が改善されています。 [2018 年 1 月 3 日](https://azure.microsoft.com/blog/securing-azure-customers-from-cpu-vulnerability/)に Azure で実施された軽減策は、Intel 製マイクロコードの更新プログラムの影響を受けません。 Microsoft は、Azure ユーザーを他の Azure 仮想マシンから保護するために、既に強力な軽減策を実施しています。  
>
> Intel 製マイクロコードでは、スペクター バリアント 2 ([CVE-2017-5715](https://www.cve.mitre.org/cgi-bin/cvename.cgi?name=2017-5715)、分岐先のインジェクション) に対処しています。このマイクロコードで、Azure 上の VM 内で共有ワークロードまたは信頼できないワークロードを実行する場合にのみ適用される攻撃から保護できます。 Microsoft のエンジニアは、Azure ユーザーにマイクロコードを提供する前に、パフォーマンスへの影響を最小限に抑えるために安定性をテストしています。  VM 内で信頼できないワークロードを実行するお客様がほとんどいないため、ほとんどのお客様はこの機能がリリースされても有効にする必要がありません。 
>
> このページは、新しい情報を入手できた時点で、直ちに更新されます。  






## <a name="keeping-your-operating-systems-up-to-date"></a>オペレーティング システムを最新の状態に保つ

Azure で実行するアプリケーションを、Azure を使用する他の顧客から切り離すために OS 更新は必要ありませんが、OS のバージョンを常に最新に保つことをお勧めします。 2018 年 1 月以降の [Windows 用セキュリティ ロールアップ](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/ADV180002)には、これらの脆弱性に対する軽減策が含まれています。

次のサービスでは、オペレーティング システムを更新するために次の操作が推奨されます。 

<table>
<tr>
<th>サービス</th> <th>推奨される操作 </th>
</tr>
<tr>
<td>Azure クラウド サービス </td>  <td>自動更新を有効にするか、最新のゲスト OS を実行していることを確認します。</td>
</tr>
<tr>
<td>Azure Linux Virtual Machines</td> <td>使用可能な場合、オペレーティング システムのプロバイダーからの更新プログラムをインストールします。 </td>
</tr>
<tr>
<td>Azure Windows Virtual Machines </td> <td>OS の更新プログラムをインストールする前に、サポートされているウイルス対策アプリケーションを実行します。 互換性については詳しくは、ウイルス対策ソフトウェア ベンダーにお問い合わせください。<p> [1 月のセキュリティ ロールアップ](https://portal.msrc.microsoft.com/en-US/security-guidance/advisory/ADV180002)をインストールします。 </p></td>
</tr>
<tr>
<td>その他の Azure PaaS サービス</td> <td>これらのサービスを使用している顧客がとる必要のある操作はありません。 Azure では、お使いの OS バージョンが自動的に最新に保たれます。 </td>
</tr>
</table>

## <a name="additional-guidance-if-you-are-running-untrusted-code"></a>信頼できないコードを実行する場合の追加のガイダンス 

信頼できないコードを実行していない限り、顧客がとる必要のある追加の操作はありません。 信頼できないコードを許可する場合は (たとえば、お客様がアプリケーション内のクラウドで実行するバイナリまたはコード スニペットのアップロードをお客様の顧客に許可する場合など)、次の追加の手順が必要になります。  


### <a name="windows"></a>Windows 
Windows を使用して信頼できないコードをホストする場合、予測実行のサイドチャネルの脆弱性 (具体的には variant 3 Meltdown である [CVE-2017-5754](https://www.cve.mitre.org/cgi-bin/cvename.cgi?name=2017-5754)、データ キャッシュの不正な読み込み) に対する追加の保護を提供する、Kernel Virtual Address (KVA) Shadowing と呼ばれる Windows の機能を有効にする必要もあります。 この機能は既定ではオフになっており、有効にすると、パフォーマンスに影響が出る場合があります。 サーバーで保護を有効にする方法については、[Windows Server KB4072698](https://support.microsoft.com/help/4072698/windows-server-guidance-to-protect-against-the-speculative-execution) を参照してください。 Azure Cloud Services を実行している場合は、WA-GUEST-OS-5.15_201801-01 または WA-GUEST-OS-4.50_201801-01 (2018 年 1 月 10 日から利用可能) を実行していることを確認し、スタートアップ タスクを使用してレジストリ キーを有効にします。


### <a name="linux"></a>Linux
Linux を使用していて、信頼できないコードをホストしている場合は、カーネルによって使用されるページ テーブルをユーザー スペースに属すページ テーブルから分離する Kernel Page Table Isolation (KPTI) を実装するより新しいバージョンに更新する必要があります。 これらの軽減策では Linux OS 更新が必要で、利用可能な場合は、ディストリビューション プロバイダーから取得できる場合があります。 OS プロバイダーは、保護が既定で有効か無効かを判断できます。



## <a name="next-steps"></a>次の手順

詳しくは、[CPU の脆弱性からの Azure 顧客の保護](https://azure.microsoft.com/blog/securing-azure-customers-from-cpu-vulnerability/)に関する記事を参照してください。
