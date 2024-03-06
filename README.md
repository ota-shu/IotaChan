# IotaChan

## 構築手順

1. テキスト分析（Language）リソース作成手順

   1. Azure Portal で、「テキスト分析」リソースを作成
      - 日本語の Bot を作る場合は、リージョンを「Japan East」にする
      - カスタム質問応答を選択する
      - インスタンスの詳細
        - 価格レベル：Free F0
      - カスタム質問応答
        - Azure Search リージョン：Japan East
        - Azure Search 価格レベル：Free F
        - このボックスをオンにすることで、責任ある AI 通知の条項を承認し、同意したことを確認します。：チェックあり

2. プロジェクト作成手順

   1. Azure AI の[Language Studio](https://language.cognitive.azure.com/home) を開く
      - 「Select an Azure resource」のダイアログが出る場合は以下の設定にする
        - Resource name：手順 1-1 で作成したリソース
   2. 「Create new」ボタン > 「Custom question answering」を選択し、プロジェクトを作成
   3. 「Choose language setting」では、「I want to select the language when I create a project in this resource」を選択
   4. 「Enter basic information」は以下の設定にする
      - Source language：Japanese

3. Knowledge Base 構築手順

   1. 作成したプロジェクトを開き、左ペインから「Edit knowledge base」を開く
   2. 「Import question and answers」 > 「Import as Excel」を選択し、当リポジトリの「iota-chan-qa_qnas.xlsx」を選択する
   3. 「Test」ボタンを押下し、日本語で質問する。期待した回答が返ってこれば OK

4. デプロイ手順

   1. 作成したプロジェクトを開き、左ペインから「Deploy knowledge base」を開く
   2. 「Deploy」ボタンを押下
   3. 「Create a bot」ボタンを押下

5. ボットの作成

   1. 手順 4-3 にて Azure Portal の Web app bot のリソース作成画面に遷移し、以下の設定にする
      - リソースグループ：手順 1-1 で作成したリソースと同じリソースグループ
      - Pricing tier：Free
      - Creation type：Create new User-assigned managed identity
      - App Service Plan
        - Creation type：Create new app service plan
      - App Settings
        - Language Resource Key：手順 1-1 で作成したリソースの「キーとエンドポイント」のキー
   2. Azure bot リソースを開き、左ペインの設定から「Web チャットでテスト」画面を開き、質問を送信して期待した回答が返ってこれば OK

6. ボットチャネルを作成
   1. Slack など利用したいクライアントに対応したボットチャネルを構成する
      - 参照： https://learn.microsoft.com/ja-jp/azure/bot-service/bot-service-manage-channels?view=azure-bot-service-4.0
