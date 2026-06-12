---
title: コンテンツ AI ソースの設定と管理
description: 最初のコンテンツソースを設定し、取得をトリガーすることで、Cloud ManagerでAEM Content AIを設定する方法について説明します。
topic: Configuration
role: Developer, Admin
level: Beginner
solution: Experience Manager
keywords: AEM Content AI, Content AI Sources，獲得，Cloud Manager, Adobe Developer Console
source-git-commit: 86c0b8b910583701dc4bd42b61e082cc5429cee8
workflow-type: tm+mt
source-wordcount: '928'
ht-degree: 1%

---


# コンテンツ AI ソースの設定と管理

このガイドでは、Cloud Managerでコンテンツ AI ソースを設定する方法（前提条件の確認から、コンテンツソースの作成、インデックス作成、使用可能な状態の確認まで）について説明します。

## 前提条件 {#prerequisites}

開始する前に、次の条件が満たされていることを確認してください。

* 1つ以上のAEM as a Cloud Service環境を持つアクティブなCloud Manager プログラムがあります。
* プログラムのAdmin Consoleで&#x200B;**[システム管理者](https://experienceleague.adobe.com/en/docs/support-resources/adobe-support-tools-guide/adobe-admin-console/admin-roles)**&#x200B;の役割を持っています。
* 環境製品プロファイルが&#x200B;**Adobe Admin Console**&#x200B;でプロビジョニングされました。[Adobe Developer Console プロジェクトの設定](setup-adc-project.md)を参照してください。

## 手順1 - 「コンテンツ AI設定」タブを開く {#open-tab}

1. [Cloud Manager](https://my.cloudmanager.adobe.com/)にログインし、プログラムを選択します。

   プログラムカードを表示する![Cloud Manager ホーム &#x200B;](../assets/content-ai-onboarding-step-1.png)

1. **[!UICONTROL プログラムの概要]**&#x200B;から、**[!UICONTROL 環境]** セクションを見つけ、設定する環境を選択します。

   ![実稼動環境がハイライト表示されたプログラムの概要](../assets/content-ai-onboarding-step-2.png)

1. 環境の詳細ページで、「**[!UICONTROL コンテンツ AI設定]**」タブを選択します。

   ![&#x200B; コンテンツ AI設定タブが強調表示された環境の詳細ページ &#x200B;](../assets/content-ai-onboarding-step-3.png)

## ステップ 2 - コンテンツ AI Sourceの作成 {#create-source}

コンテンツソースは、Content AIがクロールするweb サイトとインデックスを定義します。

1. 「**[!UICONTROL Content AI Configuration]**」タブで、「**[!UICONTROL Sourceを作成]**」を選択します。

   ![Sourceを作成ボタンを表示する「Content AI Configuration」タブ &#x200B;](../assets/content-ai-onboarding-step-4.png)

1. **[!UICONTROL 新しいコンテンツ AI Source]** ダイアログで、次のフィールドに入力します。

   | フィールド | 説明 |
   | --- | --- |
   | **[!UICONTROL Content AI設定名]** | このソースの一意のID （例：`my-site-index`）。 作成後に変更することはできません。 |
   | **[!UICONTROL 説明]** | *（オプション）* コンテンツソースの簡単な説明。 |
   | **[!UICONTROL Web サイトのアドレス]** | クロールするweb サイトのルート URL （例：`https://www.example.com/`）。 |
   | **[!UICONTROL URLを除外]** | クロール中にスキップする&#x200B;*（オプション）* URL パターン。 |
   | **[!UICONTROL 更新頻度]** | Content AIがソースを再クロールする頻度（毎週、毎日、毎日4×、60分、または15分）。 |

   ![名前とweb サイトのアドレスフィールドが入力され、「Sourceを作成」ボタンがハイライト表示されたコンテンツ AI Sourceを作成ダイアログ &#x200B;](../assets/content-ai-onboarding-step-5-0.png)

   利用可能なオプションを表示する![更新頻度ドロップダウン &#x200B;](../assets/content-ai-onboarding-step-5-1.png)

1. 「**[!UICONTROL Sourceを作成]**」を選択します。

## ステップ 3 - トリガーの獲得 {#trigger-acquisition}

ソースを作成した後、そのステータスは&#x200B;**新規**&#x200B;です。 インデックス作成を開始するには、最初の取得を実行します。

1. ソースリストで、ソースの横にある&#x200B;**その他のアクション** （。..）アイコンを選択し、**[!UICONTROL トリガー獲得]**&#x200B;を選択します。

   ![その他のアクションメニューが開き、トリガー獲得がハイライト表示されたコンテンツ AI ソース リスト &#x200B;](../assets/content-ai-onboarding-step-7.png)

1. **[!UICONTROL トリガー獲得]** ダイアログで、ソースの詳細 – **[!UICONTROL コンテンツソース]**、**[!UICONTROL 前回の実行]**、**[!UICONTROL 次回のスケジュール実行]** – を確認し、**[!UICONTROL トリガー]**&#x200B;を選択します。

   ![トリガー獲得の確認ダイアログ &#x200B;](../assets/content-ai-onboarding-step-8.png)

## 手順4 - インデックス作成ステータスの監視 {#monitor-status}

顧客獲得が開始されると、ソースステータスがリアルタイムで更新されます。

| ステータス | 意味 |
| --- | --- |
| **新規** | Sourceが作成されました。まだ買収は実行されていません。 |
| **インデックス作成** | 顧客獲得が進行中です。コンテンツをクロールし、インデックスを作成しています。 |
| **使用可能** | インデックス作成が完了しました。ソースは検索クエリを提供する準備ができました。 |

インデックス作成ステータスを表示する![&#x200B; コンテンツソースリスト &#x200B;](../assets/content-ai-onboarding-step-9.png)

![利用可能なステータスを表示するコンテンツソースリスト &#x200B;](../assets/content-ai-onboarding-step-10.png)

インデックスを検索するかAPIをテストする前に、ステータスが&#x200B;**Available**&#x200B;に達するのを待ちます。

## 手順5 - インデックス付きコンテンツの検索 {#search-content}

ソースのステータスが&#x200B;**Available**&#x200B;になると、Cloud Managerから直接検索クエリを実行して、コンテンツが正しくインデックス付けされていることを確認できます。

1. ソースリストで、ソースの横にある&#x200B;**[!UICONTROL 検索]**&#x200B;を選択します。

   ![利用可能なソースで「検索」ボタンがハイライト表示されたコンテンツソースリスト &#x200B;](../assets/content-ai-onboarding-step-13.png)

1. 検索フィールドにクエリを入力します。 結果には、一致するスコアとコンテンツタイプを持つ一致する項目のリストが表示されます（例：**PAGE**&#x200B;または&#x200B;**PDF**）。 結果を選択すると、右側にプレビューが開きます。

   ![&#x200B; クエリを含む検索パネル、一致スコアと一致する結果、上位の結果のプレビューペイン &#x200B;](../assets/content-ai-onboarding-step-14.png)

## Sourceの変更または削除 {#modify-source}

ソース設定を作成後に更新するには、次の手順に従います。

1. ソースリストで、ソースの横にある&#x200B;**その他のアクション** （。..）アイコンを選択し、**[!UICONTROL 編集]**&#x200B;を選択します。

   ![その他のアクションメニューが開き、編集が強調表示されたコンテンツソースリスト &#x200B;](../assets/content-ai-onboarding-step-11.png)

1. **[!UICONTROL コンテンツ AI Sourceを変更]** ダイアログで、必要に応じて&#x200B;**[!UICONTROL 説明]**、**[!UICONTROL Web サイトのアドレス]**、**[!UICONTROL URLを除外]**、または&#x200B;**[!UICONTROL 更新頻度]**&#x200B;を更新します。 **[!UICONTROL Content AI設定名]**&#x200B;は読み取り専用で、変更できません。

1. **[!UICONTROL 保存]**&#x200B;を選択して変更を適用するか、ダイアログの左下にある&#x200B;**[!UICONTROL 削除]**&#x200B;を選択して、ソースを完全に削除します。

   >[!WARNING]
   >
   >ソースの削除は永続的です。 そのソースのすべてのインデックス付きコンテンツが削除され、検索クエリを提供できなくなります。

   ![編集可能なフィールドがハイライト表示され、左下に「削除」ボタンが表示された「コンテンツ AI Sourceを変更」ダイアログ &#x200B;](../assets/content-ai-onboarding-step-12.png)

ソースリストが更新され、変更内容が反映されます。 ソースを削除すると、そのソースはリストに表示されなくなります。

## 次の手順 {#next-steps}

* [Adobe Developer Console プロジェクトの設定](setup-adc-project.md) - APIを呼び出すために必要なADC プロジェクトと資格情報を作成します。
* [&#x200B; コンテンツ AI API リファレンス &#x200B;](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/contentai/) - セマンティック、フルテキスト、またはハイブリッド検索エンドポイントを使用して、インデックス化されたコンテンツをクエリします。

## トラブルシューティング {#troubleshooting}

* **Sourceは、長期間[!UICONTROL &#x200B; インデックス作成]に滞在します。** （。..） メニューから取得を再試行します。 2回目の実行後にステータスが進まない場合は、**[!UICONTROL Web サイトのアドレス]**&#x200B;に公開可能であること、および&#x200B;**[!UICONTROL URLの除外]** パターンがすべてのページをフィルタリングしていないことを確認してください。
* **Sourceは、実行後に[!UICONTROL 新規]に戻ります。** Web クローラーは、設定されたルート URLからページを取得できませんでした。 URLが`200 OK`で応答し、サイトが自動要求をブロックしていないことを確認してください。
* **[!UICONTROL 検索]では、[!UICONTROL 使用可能な] ソースの結果は返されません。** インデックス作成は成功しましたが、クエリに一致するコンテンツはありません。 より幅広いクエリを試すか、クロールされたURLに想定されるページが含まれていることを確認します。
