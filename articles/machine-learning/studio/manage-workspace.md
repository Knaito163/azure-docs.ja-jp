---
title: Machine Learning ワークスペースの管理 | Microsoft Docs
description: Azure Machine Learning ワークスペースへのアクセスを管理し、ML API Web サービスをデプロイおよび管理します
services: machine-learning
documentationcenter: ''
author: heatherbshapiro
ms.author: hshapiro
manager: hjerez
editor: cgronlun
ms.assetid: daf3d413-7a77-4beb-9a7a-6b4bdf717719
ms.service: machine-learning
ms.component: studio
ms.workload: data-services
ms.tgt_pltfrm: na
ms.devlang: na
ms.topic: article
ms.date: 02/27/2017
ms.openlocfilehash: 8c8e65d5fd7efd1f9212b76e1a72b91a0ea07272
ms.sourcegitcommit: 944d16bc74de29fb2643b0576a20cbd7e437cef2
ms.translationtype: HT
ms.contentlocale: ja-JP
ms.lasthandoff: 06/07/2018
ms.locfileid: "34835068"
---
# <a name="manage-an-azure-machine-learning-workspace"></a>Azure Machine Learning ワークスペースの管理

> [!NOTE]
> Machine Learning Web サービス ポータルでの Web サービスの管理については、「[Azure Machine Learning Web サービス ポータルを使用して Web サービスを管理する](manage-new-webservice.md)」をご覧ください。
> 
> 

Machine Learning ワークスペースは、Azure Portal で管理できます。

[!INCLUDE [machine-learning-free-trial](../../../includes/machine-learning-free-trial.md)]

## <a name="use-the-azure-portal"></a>Azure ポータルの使用

Azure Portal のワークスペースは次のとおりに管理します。

1. Azure サブスクリプション管理者アカウントを使用して [Azure Portal](https://portal.azure.com/) にサインインします。
2. ページ上部の検索ボックスに、"machine learning workspaces" と入力して、**[Machine Learning ワークスペース]** を選択します。
3. 管理するワークスペースをクリックします。

標準のリソース管理情報と利用可能なオプションに加え、以下のことも可能です。

- **[プロパティ]** の表示 - このページではワークスペースとリソースの情報が表示され、このワークスペースに接続されているサブスクリプションとリソース グループが変更できます。
- **[ストレージの再同期]** - ワークスペースによってキーがストレージ アカウントに維持されます。 ストレージ アカウントによってキーが変更された場合は、**[キーの再同期]** をクリックして、ワークスペースでキーを同期できます。

このワークスペースに関連付けられた Web サービスを管理するには、Machine Learning Web サービス ポータルを使用します。 詳細な情報については、「[Azure Machine Learning Web サービス ポータルを使用して Web サービスを管理する](manage-new-webservice.md)」をご覧ください。

> [!NOTE]
> New Web サービスをデプロイして管理するには、Web サービスがデプロイされているサブスクリプションで共同作成者または管理者ロールが割り当てられている必要があります。 別のユーザーを Machine Learning ワークスペースに招待したら、Web サービスをデプロイまたは管理する前に、そのユーザーを共同作成者または管理者ロールに割り当てる必要があります。 
> 
>アクセス許可の設定の詳細については、「[Azure Portal のユーザーとグループのアクセス権の割り当てを表示](../../role-based-access-control/role-assignments-users.md)」をご覧ください。

## <a name="next-steps"></a>次の手順
* [Azure Resource Manager テンプレートを使用した Machine Learning のデプロイ](deploy-with-resource-manager-template.md)の詳細を確認する。 