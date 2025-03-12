# RAG Chatbot in Amazon Bedrock

<table>
  <tr>
    <!-- Left Side -->
    <td style="vertical-align: top; width: 50%;">
      <img src="https://github.com/user-attachments/assets/6276b3e1-8e41-4657-8d3e-1e09ac2b6376" width="100%" />
    </td>
    <!-- Right Side -->
    <td style="vertical-align: top; width: 50%;">
      <img src="https://github.com/user-attachments/assets/5163fa7b-db6f-4db3-a659-268be73c3cc7" width="100%" />
    </td>
  </tr>
</table>

[日本語](https://github.com/Ryo-samuraiJP/RAG-Chatbot-in-AmazonBedrock/blob/main/README.jp.md) | [English](https://github.com/Ryo-samuraiJP/RAG-Chatbot-in-AmazonBedrock)

**RAG (Retrieval Augmented Generation) チャットボット**とは、ドキュメントやウェブリンクなどをデータソースとして組み込むことで、
言語モデルを強化する AI 搭載のチャットボットです。この AI 技術により、最新の情報やオンラインで入手不可能な情報であっても、正確かつ最新の回答を提供することが可能になります。
通常の非 RAG チャットボット（例：ChatGPT）は事前学習されたデータに依存しており、最新の情報や専門的な知識の提供が難しい場合があります。一方で、RAG チャットボットは
特定のナレッジベースや外部ソースから情報を取得できるため、最新の法律・政府の制度更新や製品リリース情報、そしてパーソナルなコンテンツなど、
最新の情報が重要となるアプリケーションにおいて特に役立ちます。

## 目次

- [使用ツールとコンセプト](#使用ツールとコンセプト)
- [目的（問題提起）](#目的（問題提起）)
- [ワークフロー](#ワークフロー)
- [ドキュメント](#ドキュメント)
- [デモンストレーション](#デモンストレーション)
- [データに基づいた検証結果](#データに基づいた検証結果)
- [ライセンス](#ライセンス)

## 使用ツールとコンセプト

![AWS](https://img.shields.io/badge/AWS%20-%20?style=for-the-badge&logo=AmazonWebServices&logoColor=FF9900&logoSize=auto&color=232F3E)
![Amazon Bedrock](https://custom-icon-badges.demolab.com/badge/Amazon%20Bedrock%20-%20?style=for-the-badge&logo=amazon-bedrock&color=01a88d)
![Amazon S3](https://img.shields.io/badge/Amazon%20S3%20-%20?style=for-the-badge&logo=AmazonS3&logoColor=white&color=%23569A31)
![Amazon OpenSearch Service](https://custom-icon-badges.demolab.com/badge/Amazon%20OpenSearch%20Service%20-%20?style=for-the-badge&logo=amazon-opensearch&color=884df7)

このプロジェクトでは、Amazon Bedrock、S3、OpenSearch Serverless を使用しました。主なコンセプトとしては、S3 へのデータ保存、Web クローラーを使用したソース URL の追加、ナレッジベースの作成、
AI モデルへのアクセスリクエスト、AI モデルとナレッジベースを活用したチャットボットの応答生成、ベクトルストア（Vector Store）を利用した効率的な情報検索などがあります。

## 目的（問題提起）

**I. ユースケース１** – パーソナライズされた Q&A チャットボット

最近婚約した親友が挙式するので、何か思い出に残るユーモア溢れるプレゼントはないかと考えていました。そこで、RAG チャットボットを統合したアプリケーションを開発し、
新婦が新郎に関する質問をできるようにすればユニークなトリセツになると考えました。これにより、新婦が新郎の子供の頃や学生時代の面白エピソードを楽しめたり、
結婚生活で彼に関するアドバイスなどを取得できることで、より彼への理解が深まるようになります。

**II. ユースケース２** – カナダ移民政策更新の自動アップデート

カナダ政府が VISA や永住権に関する制度を更新する度に、信頼性のある情報を求めて複数の文書やソースを調べたり、膨大な文章を読むのに約 15 ～ 20 分費やしていました。
そこで、RAG チャットボットのナレッジベースに公的なウェブリンクと結合できれば、信頼できる情報源から直接、確実な情報を取得できると考えました。このシステムがあれば、
検索時間を大幅に短縮しつつ、正確かつ最新の情報を確実に得られるようになります。

## ワークフロー

1. **データソースの追加**

   - **ユースケース１：**
     - **S3 へのデータ保存** – チャットボットのデータソースとして、関連するドキュメントを **Amazon S3** に保存する。
   - **ユースケース２：**
     - **ソース URL の追加** – S3 の代わりとなる **Web クローラー**を選択し、ソース URL をデータソースとして追加する。

2. **ナレッジベースの作成** – **Amaozon Bedrock** にナレッジベースを作成し、検索ベースの AI 応答を可能にする。

3. **AI モデルへのアクセスリクエスト** - 特定の AI モデルを選択し、アクセスをリクエスト。これにより、検索結果を人間のようなテキストに変換可能にする。

4. **ベクトルストアの設定** – **OpenSearch Serverless** を使用し、ベクターベースの検索を設定。これにより、関連情報を効率的に取得可能にする。

5. **ナレッジベースの同期** – S3 のデータをナレッジベースと同期し、以下の 3 つのポイントを確認する。
   - **データインジェスト:** Bedrock が S3 からデータを取り込む。
   - **データ処理:** Bedrock がデータを大きく切り分け（チャンク化し）、埋め込み処理を実行する。
   - **データ保存:** Bedrock が処理済みデータをベクトルストア（OpenSearch Serverless）に保存する。

これらのワークフローによって、AI チャットボットが RAG チャットボットへと進化し、より特定の専門的・個人的情報に基づいた回答を生成できるようになります。

## ドキュメント

さらに詳しい説明については、[ドキュメント](https://drive.google.com/file/d/1XI0iy7e4DZWXX6lX_3I3Uwdojo5s6tiJ/view?usp=sharing) を参照してください。

## デモンストレーション

**I. ユースケース１** – パーソナライズされた Q&A チャットボット

<table>
   <tr>
      <!-- Left Side -->
      <td style="vertical-align: top; width: 50%;">
         <img src="https://github.com/user-attachments/assets/5c4b71ce-a3ba-42b8-bc45-4b1a091e9a66" width="100%" />
         <img src="https://github.com/user-attachments/assets/8e9a25ac-232d-4184-a792-5f95ad40b984" width="100%" />
      </td>
      <!-- Right Side -->
      <td style="vertical-align: top; width: 50%;">
         <img src="https://github.com/user-attachments/assets/dc521897-aa34-4dab-b6a6-79f7f5b3f5c5" width="100%" />
         <img src="https://github.com/user-attachments/assets/c17d8825-4a90-4468-8aff-17bd6c0af49f" width="100%" />
      </td>
   </tr>
</table>

**II. ユースケース２** – カナダ移民政策更新の自動アップデート

<table>
   <tr>
      <!-- Left Side -->
      <td style="vertical-align: top; width: 50%;">
         <img src="https://github.com/user-attachments/assets/3630186b-0d82-4826-9dc4-18381811e2ff" width="100%" />
      </td>
      <!-- Right Side -->
      <td style="vertical-align: top; width: 50%;">
         <img src="https://github.com/user-attachments/assets/dc25a488-e930-4bd8-b264-6b4444fd3ba0" width="100%" />
      </td>
   </tr>
</table>

## データに基づいた検証結果

**I. ユースケース１** – パーソナライズされた Q&A チャットボット

同じプロンプトを使用し、S3 に 15 個と 5 個のドキュメントを保存した状態で応答速度を比較した結果、保存するドキュメントの量によって応答速度が変化する可能性があることが判明しました。
以下はその測定データです。

- 1 回目のプロンプト: **_4.61 秒_**（15 個） → **_3.26 秒_**（5 個）
- 2 回目のプロンプト: **_5.70 秒_**（15 個） → **_5.50 秒_**（5 個）
- 3 回目のプロンプト: **_6.18 秒_**（15 個） → **_5.78 秒_**（5 個）
- 4 回目のプロンプト: **_6.81 秒_**（15 個） → **_6.80 秒_**（5 個）

保存するドキュメントを減らすことで応答速度が **平均で 0.49 秒向上** しました。これは、おそらく AI チャットボットがより多くのドキュメントを処理・検索するのに時間を要したためと考えられます。

ただし、保存するドキュメントの数を減らすことで応答速度が向上する可能性がある一方で、情報量の減少により回答の質が低下する可能性もあります。そのため、チャットボットのパフォーマンスを最適化するには、
応答速度と知識の深さのバランスを見極めることが重要です。

**II. ユースケース２** – カナダ移民政策更新の自動アップデート

カナダ政府が VISA や永住権に関する制度を更新するたびに、信頼できる情報源を探し、膨大な文章を読むのに 約 15 ～ 20 分 を費やしていました。しかし、RAG チャットボットを活用することで、
追加したソース URL から情報を取得し、それを基に最新かつ信頼性のある回答ができるようになりました。その結果、検索時間を **66.67% ～ 75% 削減** し、わずか **5 分に短縮** することに成功しました。

## ライセンス

このプロジェクトは MIT ライセンスの下で認可されています。詳細については、[LICENSE](https://github.com/Ryo-samuraiJP/RAG-Chatbot-in-AmazonBedrock/blob/main/LICENSE.md) ファイルを参照してください。
