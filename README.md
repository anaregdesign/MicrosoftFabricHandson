# MicrosftFabricHandson

## はじめに
[Microsoft Fabric](https://www.microsoft.com/ja-jp/microsoft-fabric) はMicrosoftが提供する、フルSaaS型のデータ基盤ソリューションです。

従来、データ基盤の構築には多くの知識と工数を必要としていました。
「データ基盤」と一言に言ってもその構成要素は多岐にわたります。データ基盤は様々な機能を適切に構成、オーケストレーションさせ、
それらを継続的に運用できて初めて実現されるものです。

Microsoft Fabricではデータ分析基盤に必要なあらゆる機能をSaaSとして提供しています。

データ基盤の構成にはいくつかのバリエーションがありますが、データ基盤の構成要素のうち、代表的なものを以下でご紹介します。

### データレイク
散在するデータを一箇所に集約するストレージです。データを一箇所に集約することにより、利活用の際に必要なデータを用意に参照できるようにすることを目指します。
また様々なデータを一箇所で管理することにより、組織の重要なデータに対するセキュリティを効率よく担保することができます。

### 大規模集計/加工リソース・データウェアハウス
大規模なデータを加工・集計するための計算リソースです。
集約されたデータを効率よく活用するために、データはときに適切な形に加工する必要があります。この「分析のために加工されたデータ」を *中間テーブル* と言います。

構成によっては *データウェアハウス* と呼ばれる、分析シナリオに特化したデータベースを保有することがあります。
これはより高頻度なアドホック分析を多用する組織に適しています。

### データ転送
様々なデータソースからデータを集約したり、より適切なインフラへの相互の転送を担います。

### パイプライン管理
データの転送や、集計・加工などの処理のスケジュールと依存関係を管理します。
データ基盤における様々な処理は、複数のシステムを横断して実行されます。
その処理を適切なスケジュールで、適切な順番で実行させるひと続きの処理を *パイプライン* といいます。

### リソース管理
データ基盤の様々な機能に必要なCPU・メモリ・ディスク・ネットワークを適切に割り当てる役割を担います。


## Microsoft Fabricの概要
Microsoft Fabricは従来のPowerBIを拡張する形で提供されます。PowerBI Serviceではワークスペースを作成する際に、Pro、Premiumなどのライセンスを選択できましたが、
この度追加されたライセンスである「ファブリック容量」を選択することで、従来の機能に加えてMicrosoft Fabric特有の機能を使うことができるようになります。


<img width="400" alt="Screenshot 2023-12-13 at 15 41 42" src="https://github.com/anaregdesign/MicrosoftFabricHandson/assets/6128022/e9e3b3b7-b426-412b-b77e-8ead54809ed0">


「ファブリック容量」が割り当てられたワークスペースにおいては、データ基盤の構築に有用な様々な機能が作成できます。後で説明しますが、「レイクハウス」や「データフロー」などがそれに該当します。
従来から存在していた「レポート」のようなBIにフォーカスしていましたが、ファブリック容量では新たにデータ基盤の構築に必要なリソースを作成することができます

<img width="400" src="https://github.com/anaregdesign/MicrosoftFabricHandson/assets/6128022/8cf5c79c-332c-4541-828f-24b825673ee2">


## 主要コンポーネントの概要
ここではファブリック容量で新たに追加された、主要なリソースを紹介します。

### レイクハウス
<img width="400" src="https://github.com/anaregdesign/MicrosoftFabricHandson/assets/6128022/1e9c4c1d-9ad1-4562-a992-b670e92a64c5">

データを蓄積するストレージです。とくに構造化データはDeltalakeというオープンな形式で取り扱うことができ、様々な外部の計算リソースとの柔軟な連携を可能にしています。

#### レイクハウスのショートカット機能
<img width="400" alt="Screenshot 2023-12-15 at 14 48 27" src="https://github.com/anaregdesign/MicrosoftFabricHandson/assets/6128022/ddbb6958-3cd6-4f5c-8604-c8381078cbb4">
AWS S3やGoogle Cloud Storage、Dataverseなど外部のストレージに対して、レイクハウスが持つ柔軟なインターフェースを提供することができます。

<!--
#### レイクハウスのミラーリング機能
<img width="400" srd="https://github.com/anaregdesign/MicrosoftFabricHandson/assets/6128022/25a9e40f-4b3e-43e7-a272-5f619f61baa9">

ショートカットがMicrosoft Fabric上にデータの実体を持たないのに対して、ミラーリング機能では外部のデータソースとのリアルタイムな同期・レプリケーションを提供します。
この機能は将来的にCosmosDBやPostgresSQL、Snowflakeなどの対応が予定されており、ETLの作業を大幅に簡単にします。
-->
### SQLエンドポイント
<img width="400" src="https://github.com/anaregdesign/MicrosoftFabricHandson/assets/6128022/091a0ccf-e835-468b-b259-f1de1ed0ca08">

レイクハウスに対してODBCを含むSQL Server互換のインターフェースを提供します。サーバレス構成のため`create table`など一部の構文の利用が制限されていますが、多くのアドホック分析シナリオに対応できます。


### データフローGen2

<img width="400" src="https://github.com/anaregdesign/MicrosoftFabricHandson/assets/6128022/2298a15f-ba05-49e9-8d5d-4b803addcd16">

非開発者向けのノーコードETLツールです。様々なデータソースから読み込んだデータを処理して、様々なストレージに記録することができます。
多くのシナリオではレイクハウス上にあるDeltalake形式のテーブルを読み込み、処理したものを再びレイクハウスに記録するために使用します。

### パイプライン
<img width="400" srd="https://github.com/anaregdesign/MicrosoftFabricHandson/assets/6128022/0596738c-f379-4ba3-86ff-c6f1c0c98fc9">


グラフィカルなノーコードツールによって、様々なインフラを横断して実行される様々な処理の、依存関係とその実行スケジュールを定義するために使用します。
データフローや、ストアドプロシージャ・SparkNotebookなど、様々な処理のが実行でき、定義した処理はアクティビティと呼びます。

#### パイプラインのコピーアシスタント


アクティビティの一つに「データのコピー」と言われるデータを転送するためのアクティビティがあります。
パイプラインのコピーアシスタントは、このコピーアクティビティを簡単に作成するためのウィザードです。


# Handson
TSの皆様が対象の手順書です。

## 1.レイクハウスの作成

### 手順概要
* レイクハウスを３つ作成する
  * bronze
  * silver
  * gold
* レイクハウスと同時に作成されるリソースを確認する

### 参考
* 完了した状態
  
<img width="400" src="https://github.com/anaregdesign/MicrosoftFabricHandson/assets/6128022/11101cf0-7f88-4d37-966b-ec5f9f7495f1">


## 2.データのコピー

### 手順概要
* パイプラインのコピーアシスタントで、サンプルデータをレイクハウスにコピーしてくる
* あまりgithubを意識させないような話し方。いろんなデータソースがある中の一つ
* 接続情報 
  * protocol: https
  * endpoint: https://github.com/anaregdesign/MicrosoftFabricHandson/raw/main/data/
  * files
    - dboAddresses.parquet
    - dboCustomers.parquet
    - dboOrders.parquet
    - dboOrderDetails.parquet
* それぞれのファイルに対して４つのコピーアクティビティをコピーアシスタントで作成


### 参考
*
<img width="800" src="https://github.com/anaregdesign/MicrosoftFabricHandson/assets/6128022/a102d944-72a5-45b8-8d2a-138c8cb537d1">


* パイプラインのコピーアシスタントでデモデータに対する接続の作成

<img width="800" alt="Screenshot 2023-12-15 at 15 11 39" src="https://github.com/anaregdesign/MicrosoftFabricHandson/assets/6128022/f08eea98-736c-467e-aef0-52f837effe59">

* ４つそれぞれのファイルに対してコピーアクティビティを作成する
  
<img width="800" alt="Screenshot 2023-12-15 at 15 13 07" src="https://github.com/anaregdesign/MicrosoftFabricHandson/assets/6128022/67a6075f-fb30-4d7d-b36b-0541c9fa42f7">

* 完了した状態

<img width="800" alt="Screenshot 2023-12-15 at 15 17 50" src="https://github.com/anaregdesign/MicrosoftFabricHandson/assets/6128022/10d99178-b2e8-48c5-b303-1e8f2a3010fe">


## 3.データ加工

### 手順概要
* 完璧に再現できなくても「加工できた感」があればOKだと思ってます
* データフローGen2を利用
* silverに保存
  * `silver.fact_orders`
    * `bronze`に配置した`orders`と`order_details`を`OrderID`をkeyに左外部結合
    * 更に`addresses`と`CustomerID`をkeyひ左外部結合、`AddressID`だけを展開
    * ID型の列を左側に並び替え
    * 不要そうな列は適当に削除
  * `silver.dim_addresses`
    * `addresses`をそのまま
  * `silver.dim_customers`
    * `customers`もそのまま
    
 
   
### 参考
* データフローの完成図
<img width="800" alt="Screenshot 2023-12-15 at 15 44 34" src="https://github.com/anaregdesign/MicrosoftFabricHandson/assets/6128022/369918b6-5140-4e14-a430-5916bd07bf85">

## 4.パイプラインの作成
### 概要
* 2で作成したデータのコピーが終了したら3で作成したデータの加工を実行する簡単なパイプラインを作成する
* 作成したパイプラインを実行

### 参考
* 完成したパイプライン
<img width="800" alt="Screenshot 2023-12-15 at 16 51 38" src="https://github.com/anaregdesign/MicrosoftFabricHandson/assets/6128022/df55db2b-37c2-48ee-8660-543047fb0b16">

* 実行後の`silver`の状態
<img width="800" alt="Screenshot 2023-12-15 at 16 53 57" src="https://github.com/anaregdesign/MicrosoftFabricHandson/assets/6128022/3d828e8c-84ca-4476-ae80-7f0068c4da3e">

## 可視化

### 概要
* コピーツールを用いてRetailSamleDataをコピーしてくる
  * `dimension_city`
  * `dimension_stock_item`
  * `fact_sales`
* セマンティックモデルの作成
  * `StockItemKey`と`CityKey`でそれぞれのテーブルとリレーションを作成する
* 自由にグラフ作る
