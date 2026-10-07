---
title: コンテンツ AI ソースの設定と管理
description: 最初のコンテンツソースを設定し、獲得をトリガーして、Cloud Manager で AEM コンテンツ AI を設定する方法について説明します。
topic: Configuration
role: Developer, Admin
level: Beginner
solution: Experience Manager
keywords: AEM コンテンツ AI, コンテンツ AI ソース, 獲得, Cloud Manager, Adobe Developer Console
source-git-commit: d8bd542a6a2d7e467b0d50e022f1e019d6f5b5ff
workflow-type: tm+mt
source-wordcount: '1671'
ht-degree: 77%
---

# コンテンツ AI ソースの設定と管理

このガイドでは、前提条件を満たすことから、コンテンツソースの作成、インデックス作成と使用可能性の確認まで、Cloud Manager でコンテンツ AI ソースを設定する方法を順を追って説明します。

## 前提条件 {#prerequisites}

開始する前に、次の条件を満たしていることを確認してください。

* 1 つ以上の AEM as a Cloud Service 環境を持つアクティブな Cloud Manager プログラムがある。
* Cloud Manager製品プロファイルがあり、Cloud Managerにログインできます。以下の「[Cloud Managerへのアクセスを取得する](#cloud-manager-access)」を参照してください。
* ユーザーがターゲット環境の **AEM ユーザー**&#x200B;製品プロファイルに割り当てられ、これによりコンテンツソースを表示できる。
* ユーザーがターゲット環境の **AEM 管理者**&#x200B;製品プロファイルに割り当てられ、これによりコンテンツソースを作成および編集できる。 Cloud Manager へのアクセス権のみでは不十分です。以下の [AEM 製品プロファイルへのユーザーの割り当て](#assign-product-profile)を参照してください。
* 環境の製品プロファイルが **Adobe Admin Console** でプロビジョニングされている。

## Cloud Managerにアクセス {#cloud-manager-access}

「**[!UICONTROL Content AI Configuration]**」タブを開くには、Cloud Manager UIにアクセスする必要があります。 組織の[!DNL Adobe Admin Console]管理者（システム管理者または製品管理者）がこのアクセス権を付与します。

1. [[!DNL Adobe Admin Console]](https://adminconsole.adobe.com/)の管理者にお問い合わせください。 まだ組織のメンバーでない場合は、管理者にAdobe IDまたは電子メールアドレスの追加を依頼します。
1. 組織のAEM as a Cloud Service プログラム用のCloud Manager製品プロファイルを割り当てるように管理者に依頼します。

   | 製品プロファイル | できること |
   | --- | --- |
   | **[!UICONTROL ビジネスオーナー]** | プログラムの管理： **[!UICONTROL アクセスの管理]**&#x200B;など、幅広いCloud Manager権限を持っています。 |
   | **[!UICONTROL デプロイメントマネージャー]** | 環境、デプロイ、パイプラインを管理します。 |
   | **[!UICONTROL プログラムマネージャー]** | チーム設定とプログラム監視を管理します。 |
   | **[!UICONTROL 開発者]** | コードとGitで動作します。 Cloud Manager権限が制限されています。 |

1. Cloud Managerを開くには、[Cloud Manager](https://my.cloudmanager.adobe.com/)でログインするか、[[!DNL Adobe Experience Cloud]](https://experience.adobe.com/) > **[!DNL Experience Manager]** > **[!UICONTROL Cloud Manager]**&#x200B;に移動します。 Adobe IDが複数の組織に属している場合は、正しい組織を選択します。

>[!NOTE]
>
>Cloud Manager製品プロファイルでは、コンテンツソースへのアクセス権がありません。 環境には&#x200B;**[!UICONTROL AEM Users]**&#x200B;または&#x200B;**[!UICONTROL AEM Administrators]**&#x200B;製品プロファイルも必要です。[AEM製品プロファイルへのユーザーの割り当て](#assign-product-profile)を参照してください。 デフォルトのCloud Manager ユーザーロールのみを持つユーザーは、環境を開くことができますが、プログラムレベルのアクセス権は取得できません。

ログインしてもプログラムまたは「**[!UICONTROL コンテンツ AI設定]**」タブが表示されない場合は、管理者に割り当てられた製品プロファイルの確認を依頼してください。 ログイン時に正しい組織を選択したことも確認します。 AEM Managed Servicesでは、AEM as a Cloud Serviceとは異なる[!DNL Admin Console]製品コンテキストと設定が使用されています。

最初のオンボーディング中にプログラムを作成するには、システム管理者が最初に&#x200B;**[!UICONTROL Business Owner]** プロファイルを持ち、Cloud Managerにログインする必要があります。

詳しくは、次を参照してください。

* [Cloud Manager製品プロファイルへのチームメンバーの割り当て](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/journey/assign-profiles-cloud-manager)
* [Cloud Manager へのアクセス](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-service/content/onboarding/journey/cloud-manager)
* [AEM as a Cloud Serviceのチームと製品のプロファイル](https://experienceleague.adobe.com/en/docs/experience-manager-cloud-service/content/onboarding/concepts/aem-cs-team-product-profiles)
* [ユーザーと役割の追加](https://experienceleague.adobe.com/ja/docs/experience-manager-cloud-manager/content/requirements/users-and-roles)

## AEM 製品プロファイルへのユーザーの割り当て {#assign-product-profile}

特定の環境に対する [!DNL Adobe Experience Manager] as a Cloud Service へのアクセス権をユーザーに付与するには、次の手順に従います。 ユーザーが必要とするアクセス権に一致するプロファイルを割り当てます。

* **[!UICONTROL AEM ユーザー]** - コンテンツソースを表示します。
* **[!UICONTROL AEM 管理者]** - コンテンツソースを作成および編集します。

>[!NOTE]
>
>AEM にアクセスするには、ユーザーは **[!UICONTROL AEM ユーザー]**&#x200B;や **[!UICONTROL AEM 管理者]**&#x200B;などの AEM 製品プロファイルに属している必要があります。 Cloud Manager へのアクセス権のみでは不十分です。

これらのプロファイルを割り当てるには、[!UICONTROL ビジネスオーナー Cloud Manager 製品プロファイル]を持つシステム管理者である必要があります。 ユーザーの名前とメールアドレスを準備します。

1. [Cloud Manager](https://my.cloudmanager.adobe.com/) でプログラムに移動し、ターゲット環境の「**[!UICONTROL アクセスを管理]**」を選択します。 新しいタブで、その環境の [!DNL Adobe Admin Console] が開きます。
1. **作成者**&#x200B;層と&#x200B;**パブリッシュ**&#x200B;層（例：`AEM Administrators - author - Program 12345 - Environment 67890`と`AEM Administrators - publish - Program 12345 - Environment 67890`など）の両方の&#x200B;**[!UICONTROL AEM Users]**&#x200B;または&#x200B;**[!UICONTROL AEM Administrators]**&#x200B;製品プロファイルを選択します。
   * **[!UICONTROL AEM ユーザー]** – 読み取り専用の操作。
   * **[!UICONTROL AEM管理者]** - コンテンツソースの作成、編集、削除、取得のトリガーなどの書き込み操作。
1. 「**[!UICONTROL ユーザーを追加]**」を選択します。
1. ユーザー名とメールアドレスを入力し、変更を保存します。 ユーザーが製品プロファイルに追加されます。

開発、ステージング、本番など、ユーザーがアクセスを必要とする各環境で、これらの手順を繰り返します。

>[!CAUTION]
>
>**[!UICONTROL AEM 管理者]**&#x200B;または **[!UICONTROL AEM ユーザー]**&#x200B;という名前のデフォルトの製品プロファイルは、編集または削除しないでください。 **[!UICONTROL AEM 管理者]**&#x200B;の名前を変更すると、その役割が割り当てられているすべてのユーザーから管理者権限が削除されます。

### 割り当ての確認 {#verify-assignment}

割り当てが成功したことを確認するには：

1. [!DNL Admin Console] で、割り当てた製品プロファイルを再度開きます。
1. ユーザーがメンバーリストに表示されていることを確認します。

アクセスやトークンに関する問題をトラブルシューティングする際は、ユーザーがグループを通じてだけでなく、製品プロファイルに直接追加されていることを確認します。

## 手順 1 -「コンテンツ AI 設定」タブを開く {#open-tab}

1. [Cloud Manager](https://my.cloudmanager.adobe.com/) にログインし、プログラムを選択します。

   ![プログラムカードを示す Cloud Manager ホーム](../assets/content-ai-onboarding-step-1.png)

1. **[!UICONTROL プログラムの概要]**&#x200B;から、「**[!UICONTROL 環境]**」セクションを見つけ、設定する環境を選択します。

   ![本番環境がハイライト表示されたプログラムの概要](../assets/content-ai-onboarding-step-2.png)

1. 環境の詳細ページで、「**[!UICONTROL コンテンツ AI 設定]**」タブを選択します。

   ![「コンテンツ AI 設定」タブがハイライト表示された環境の詳細ページ](../assets/content-ai-onboarding-step-3.png)

## 手順 2 - コンテンツ AI ソースを作成 {#create-source}

コンテンツソースでは、コンテンツ AI がクロールしてインデックス作成する web サイトを定義します。

1. 「**[!UICONTROL コンテンツ AI 設定]**」タブで、「**[!UICONTROL ソースを作成]**」を選択します。

   ![「ソースを作成」ボタンを示す「コンテンツ AI 設定」タブ](../assets/content-ai-onboarding-step-4.png)

1. **[!UICONTROL 新規コンテンツ AI ソースを作成 / 追加]**&#x200B;ダイアログで、次のフィールドに入力します。

   | フィールド | 説明 |
   | --- | --- |
   | **[!UICONTROL コンテンツ AI 設定名]** | このソースの一意の ID（例：`my-site-index`）。 作成後は変更できません。 |
   | **[!UICONTROL 説明]** | *（オプション）* コンテンツソースの短い説明。 |
   | **[!UICONTROL Web サイトアドレス]** | クロールする web サイトのルート URL（例：`https://www.example.com/`）。 |
   | **[!UICONTROL URL を除外]** | *（オプション）*&#x200B;クロール中にスキップする URL パターン。 |
   | **[!UICONTROL 更新頻度]** | コンテンツ AI がソースを再クロールする頻度：週単位、日単位、日単位 4 回、60 分または 15 分。 |

   ![名前と web サイトアドレスのフィールドが入力され、「ソースを作成」ボタンがハイライト表示されたコンテンツ AI ソースを作成ダイアログ](../assets/content-ai-onboarding-step-5-0.png)

   ![使用可能なオプションを示す更新頻度ドロップダウン](../assets/content-ai-onboarding-step-5-1.png)

1. 「**[!UICONTROL ソースを作成]**」を選択します。 獲得が自動的に開始され、ソースは&#x200B;**インデックス作成**&#x200B;に移行します。

   ![インデックス作成ステータスに新規作成されたソースを示すコンテンツソースリスト](../assets/content-ai-onboarding-step-6.png)

## 手順 3 - 獲得を再実行 {#trigger-acquisition}

ソースを作成すると獲得が自動的に実行され、その後は&#x200B;**[!UICONTROL 更新頻度]**&#x200B;で設定したスケジュールに従って実行されます。 また、新しいコンテンツを公開した直後にインデックスを再作成するなど、いつでも手動で実行をトリガーできます。

1. ソースリストで、ソースの横にある&#x200B;**その他のアクション**（…）アイコンを選択し、「**[!UICONTROL 獲得をトリガー]**」を選択します。

   ![その他のアクションメニューが開き、「獲得をトリガー」がハイライト表示されたコンテンツ AI ソースリスト](../assets/content-ai-onboarding-step-7.png)

1. **[!UICONTROL 獲得をトリガー]**&#x200B;ダイアログで、ソースの詳細（**[!UICONTROL コンテンツソース]**、**[!UICONTROL 前回の実行]**、**[!UICONTROL 次のスケジュールされた実行]**）を確認し、「**[!UICONTROL トリガー]**」を選択します。

   ![獲得をトリガー確認ダイアログ](../assets/content-ai-onboarding-step-8.png)

## 手順 4 - インデックス作成ステータスを監視 {#monitor-status}

獲得が開始されると、ソースステータスはリアルタイムで更新されます。

| ステータス | 意味 |
| --- | --- |
| **新規** | ソースが作成されたばかりです。自動獲得はまだ開始されていません。 このステータスは一時的なものです。 |
| **インデックス作成** | 獲得は処理中です。コンテンツのクロールとインデックス作成が実行されています。 |
| **使用可能** | インデックス作成が完了しました。ソースは検索クエリを提供する準備が整いました。 |

![インデックス作成ステータスを示すコンテンツソースリスト](../assets/content-ai-onboarding-step-9.png)

![使用可能なステータスを示すコンテンツソースリスト](../assets/content-ai-onboarding-step-10.png)

インデックスの検索や API のテストを実行する前に、ステータスが&#x200B;**使用可能**&#x200B;に達するまで待機します。

## 手順 5 - インデックス作成済みコンテンツを検索 {#search-content}

ソースステータスが&#x200B;**使用可能**&#x200B;になったら、Cloud Manager から直接検索クエリを実行して、コンテンツが正しくインデックス作成されていることを確認できます。

1. ソースリストで、ソースの横にある&#x200B;**検索**（虫眼鏡）アイコンを選択します。

   ![使用可能なソースで検索アイコンがハイライト表示されたコンテンツソースリスト](../assets/content-ai-onboarding-step-13.png)

1. 検索フィールドにクエリを入力します。 結果には、一致スコアとコンテンツタイプ（例：**ページ**&#x200B;または **PDF**）と一致する項目のリストが表示されます。 結果を選択すると、右側にプレビューが開きます。

   ![クエリを含む検索パネル、一致スコアと一致する結果、上位結果のプレビューパネル](../assets/content-ai-onboarding-step-14.png)

## ソースの変更または削除 {#modify-source}

### ソースの変更 {#modify}

ソース設定を作成後に更新するには：

1. ソースリストで、ソースの横にある&#x200B;**その他のアクション**（…）アイコンを選択し、「**[!UICONTROL 編集]**」を選択します。

   ![その他のアクションメニューが開き、「編集」がハイライト表示されたコンテンツソースリスト](../assets/content-ai-onboarding-step-11.png)

1. **[!UICONTROL コンテンツ AI ソースを変更]**&#x200B;ダイアログで、必要に応じて&#x200B;**[!UICONTROL 説明]**、**[!UICONTROL Web サイトアドレス]**、**[!UICONTROL URL を除外]**&#x200B;または&#x200B;**[!UICONTROL 更新頻度]**&#x200B;を更新します。 **[!UICONTROL コンテンツ AI 設定名]**&#x200B;は、読み取り専用で、変更できません。

   ![編集可能なフィールドがハイライト表示されたコンテンツ AI ソースを変更ダイアログ](../assets/content-ai-onboarding-step-12.png)

1. 「**[!UICONTROL 保存]**」を選択して、変更を適用します。 ソースリストが更新され、変更が反映されます。

### ソースの削除 {#delete}

1. ソースリストで、ソースの横にある&#x200B;**その他のアクション**（…）アイコンを選択し、「**[!UICONTROL 削除]**」を選択します。

   >[!WARNING]
   >
   >ソースの削除は永続的です。 そのソースのすべてのインデックス作成済みコンテンツは削除され、検索クエリを提供できなくなります。

削除後、ソースはリストに表示されなくなります。

## 次の手順 {#next-steps}

* [Adobe Developer Console プロジェクトの設定](setup-adc-project.md) - API を呼び出すために必要な ADC プロジェクトと資格情報を作成します。
* [Content AI API リファレンス](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/contentai/) - セマンティック、フルテキストまたはハイブリッド検索エンドポイントを使用して、インデックス作成済みコンテンツのクエリを実行します。

## トラブルシューティング {#troubleshooting}

* **ソースが[!UICONTROL インデックス作成]中に長期間留まります。** （…）メニューから獲得を再試行します。 2 回目の実行後にステータスが進まない場合は、**[!UICONTROL web サイトアドレス]**&#x200B;が公開可能であることと、**[!UICONTROL URL を除外]**&#x200B;パターンがすべてのページを除外していないことを確認してください。
* **ソースが実行後に[!UICONTROL 新規]に戻ります。** クローラーは、設定済みルート URL からページを取得できませんでした。 URL が `200 OK` で応答し、サイトが自動リクエストをブロックしていないことを確認してください。
* **[!UICONTROL 検索]では、[!UICONTROL 使用可能]なソースの結果が返されません。** インデックス作成は成功しましたが、クエリに一致するコンテンツはありませんでした。 より広範なクエリを試すか、クロールされた URL に期待するページが含まれているかどうかを確認してください。
