---
title: AEM Content AI用のAdobe Developer Console プロジェクトのセットアップ
description: サーバー間またはAPI キー認証を使用して、Adobe Developer Console プロジェクトを設定し、AEM Content AI サービスへのAPI呼び出しを認証する方法について説明します。
topic: Configuration
role: Developer, Admin
level: Beginner
solution: Experience Manager
keywords: AEM Content AI、Adobe Developer Console、認証、サーバー間、API キー、アクセストークン
source-git-commit: 2ff1bbdd3ff224e2a6b389243c78af5fd228d5ee
workflow-type: tm+mt
source-wordcount: '714'
ht-degree: 3%

---


# Adobe Developer Console プロジェクトの設定 {#configure-adc-project}

AEM Content AI Services APIを呼び出すには、Adobe Developer Console（ADC）プロジェクトによって発行された資格情報が必要です。 このページでは、プロジェクトの作成、認証方法の選択、API リクエストごとに含める資格情報の生成について説明します。

開始するには、[Adobe Developer Console](https://developer.adobe.com/console/)にアクセスしてください。

## 前提条件 {#prerequisites}

始める前に、次の点を確認してください。

* お客様の組織の[Adobe Developer Console](https://developer.adobe.com/console/)にアクセスできます。
* **Adobe Admin Console**&#x200B;のAEM Content AI Services製品プロファイルに&#x200B;**開発者**&#x200B;として追加されました。 このロールがないと、**[!UICONTROL AEM Content AI Services]** API カードは無効になり、**[!UICONTROL サーバー間]**&#x200B;認証オプションは非表示になります。
* 選択する製品プロファイルのプログラム番号と環境番号（例：`AEM User - publish - Program 12345 - Environment 67890`）を知っています。
* プログラムのAdmin Consoleで&#x200B;**[システム管理者](https://experienceleague.adobe.com/ja/docs/support-resources/adobe-support-tools-guide/adobe-admin-console/admin-roles)**&#x200B;の役割を持っています。 この役割では、製品プロファイルを管理し、環境にユーザーを割り当てることができます。

## 認証方法の選択 {#choose-auth}

AEM Content AI Servicesでは、2つの認証方法をサポートしています。 統合に一致するものを選択してください：

| メソッド | 次に最適 |
| --- | --- |
| [&#x200B; サーバー間](#s2s-auth) | ユーザーの操作なしでAPIを呼び出すバックエンドサービス。 短期間有効なアクセストークンを返します。 |
| [API キー](#api-key-auth) | APIを直接呼び出すクライアントサイドまたはブラウザーベースの統合。 許可されたドメインに対してスコープが設定された長期間有効なキーを返します。 |

## サーバー間認証 {#s2s-auth}

1. **[!UICONTROL APIとサービス]**、次に&#x200B;**[!UICONTROL API]**&#x200B;を選択します。

   ![APIとサービスを表示するDeveloper Console](../assets/e2e-env-setup-28.png)

1. **AEM Content AI サービス**&#x200B;でフィルタリングし、**[!UICONTROL プロジェクトを作成]**&#x200B;して新しいプロジェクトを開始するか、既存のプロジェクトにサービスを追加する場合は&#x200B;**[!UICONTROL API]**&#x200B;を追加します。

   >[!NOTE]
   >
   >「ライセンスが必要です」というメッセージが表示されてAPI カードが無効になっている場合、AEM as a Cloud Service環境が最新化されていない可能性があります。 [AEM as a Cloud Service環境の最新化](https://experienceleague.adobe.com/ja/docs/experience-manager-learn/cloud-service/aem-apis/openapis/setup#modernization-of-aem-as-a-cloud-service-environment)を参照してください。

1. **[!UICONTROL Configure API]** ダイアログで、**[!UICONTROL サーバー間]**&#x200B;認証を選択します。

   ![&#x200B; サーバー間のAPI ダイアログを選択しました](../assets/e2e-env-setup-29.png)

   >[!TIP]
   >
   >サーバー間オプションが使用できない場合、統合を設定するユーザーは開発者として製品プロファイルに追加されません。 [&#x200B; サーバー間認証を有効にする](https://developer.adobe.com/developer-console/docs/guides/authentication/ServerToServerAuthentication/implementation)を参照してください。

1. 必要に応じて、資格情報の名前を変更します。 「**[!UICONTROL 次へ]**」を選択します。

   ![Adobe Developer Consoleの手順を実行して、新しいサーバー間資格情報の名前を変更してから、「次へ](../assets/e2e-env-setup-30.png)」を選択します

1. **[!UICONTROL AEM User - publish - Program XXX - Environment XXX]**&#x200B;および/または&#x200B;**[!UICONTROL AEM User - author - Program XXX - Environment XXX]** Product Profileを選択し、**[!UICONTROL Save]**&#x200B;を選択します。

   ![対象プログラムと環境のAEM ユーザーの公開プロファイルと作成者プロファイルを示す製品プロファイルピッカー](../assets/e2e-env-setup-31.png)

1. APIと認証設定を確認します。

   ![選択したAPI、認証タイプ、資格情報名を要約する画面を確認](../assets/e2e-env-setup-33.png)

   ![資格情報に割り当てられた製品プロファイルを表示する画面の詳細を確認](../assets/e2e-env-setup-34.png)

### アクセストークンの生成 {#generate-token}

1. ADC プロジェクトで、**[!UICONTROL 資格情報]**&#x200B;に移動し、**[!UICONTROL アクセストークンの生成]**&#x200B;を選択します。

   「アクセストークンを生成」ボタンが強調表示された![資格情報ページ &#x200B;](../assets/e2e-env-setup-32.png)

1. すべてのAPI リクエストの`Authorization` ヘッダーにトークンを含めます。

   ```http
   Authorization: Bearer YOUR_ACCESS_TOKEN
   ```

   >[!WARNING]
   >
   >トークンを安全に保管する： 有効期限が切れ、定期的に再生成する必要があります。

## API キー認証 {#api-key-auth}

1. AEM Content AI Services APIをプロジェクトに追加する際、**[!UICONTROL 認証タイプを選択]** ダイアログで「**[!UICONTROL API Key]**」を選択します。

   ![API キー認証タイプを選択](../assets/onboarding-api-key-01.png)

1. API キー資格情報を確認します。

   ![API キー資格情報を追加](../assets/onboarding-api-key-02.png)

1. キーを使用できるオリジンを制限するには、許可されたドメインを設定します。

   ![許可されたドメインの設定](../assets/onboarding-api-key-03.png)

1. API キー（クライアント ID）は、**[!UICONTROL 接続済み資格情報]**&#x200B;の下に表示されます。 「**[!UICONTROL コピー]**」を選択します。

   ![接続された資格情報からAPI キーをコピー](../assets/onboarding-api-key-04.png)

1. すべてのAPI リクエストにキーを含めます。

   ```http
   x-api-key: YOUR_API_KEY
   ```

   これでプロジェクトの準備ができました。 AEM Content AI Servicesへのリクエストのたびにキーを使用します。

## 次の手順 {#next-steps}

* [&#x200B; コンテンツソースの制御](contentsources.md) - Cloud Managerとトリガーの取得でコンテンツソースを設定します。
* [&#x200B; コンテンツ AI API リファレンス &#x200B;](https://developer.adobe.com/experience-cloud/experience-manager-apis/api/experimental/contentai/) - アクセストークンまたはAPI キーを使用して、インデックス付きコンテンツをクエリします。
