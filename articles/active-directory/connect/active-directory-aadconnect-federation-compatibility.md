---
title: Azure AD のフェデレーション互換性リスト
description: このページには、シングル サインオンの実装に使用できる Microsoft 以外の ID プロバイダーが記載されています。
services: active-directory
documentationcenter: ''
author: billmath
manager: mtillman
editor: curtand
ms.assetid: 22c8693e-8915-446d-b383-27e9587988ec
ms.service: active-directory
ms.workload: identity
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 04/27/2018
ms.component: hybrid
ms.author: billmath
ms.openlocfilehash: f5e85a551181a3dd4618db2611a99675329cfabd
ms.sourcegitcommit: 266fe4c2216c0420e415d733cd3abbf94994533d
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/01/2018
ms.locfileid: "34592015"
---
# <a name="azure-ad-federation-compatibility-list"></a>Azure AD のフェデレーション互換性リスト
Azure Active Directory は、サードパーティ ソリューションを必要とすることなくハイブリッド実装とクラウド専用の実装を実現するために、Office 365 などの Microsoft オンライン サービスに対してシングル サインオンとアプリケーション アクセスのセキュリティ強化を提供します。 Office 365 は、Microsoft のオンライン サービスのほとんどと同様に、ディレクトリ サービス、認証、承認のために Azure Active Directory と統合されます。 また、Azure Active Directory では、多数の SaaS アプリケーションやオンプレミスの Web アプリケーションにもシングル サインオンを提供しています。 サポートされている SaaS アプリケーションについては、Azure Active Directory [アプリケーション ギャラリー](https://azuremarketplace.microsoft.com/marketplace/apps)を参照してください。 

## <a name="idp-validation"></a>IDP の検証
組織でサードパーティのフェデレーション ソリューションを使用している場合、Office 365 などの Microsoft Online サービスを使用して、オンプレミスの Active Directory ユーザー向けにシングルサインオンを構成することができます。ただし、サードパーティのフェデレーション ソリューションが Azure Active Directory と互換性がある必要があります。  互換性に関する質問については、ID プロバイダーに問い合わせてください。  Microsoft によって Azure AD との互換性を以前にテストされている ID プロバイダーの一覧を表示するには、[ここ](https://www.microsoft.com/download/details.aspx?id=56843)をクリックしてください。 

>[!NOTE]
>Microsoft では、Azure Active Directory との互換性のための独立 ID プロバイダーの検証テストは現在提供していません。 製品の相互運用性をテストしたい場合は、こちらの[ガイドライン](https://www.microsoft.com/download/details.aspx?id=56843)を参照してください。 

## <a name="next-steps"></a>次の手順

- [オンプレミスのディレクトリと Azure Active Directory の統合](active-directory-aadconnect.md)
- [Azure AD Connect とフェデレーション](active-directory-aadconnectfed-whatis.md)
