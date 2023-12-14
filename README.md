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
また実際にビジネスに対するインサイトを得るためには、更に中間テーブルを集計する必要があります。

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
従来から存在していた「レポート」のような機能はデータ基盤の中でもBIにフォーカスしていたものが多かった一方で、Microsoft Fabricでは新たにデータ基盤の構築に必要な要素

<img width="400" src="https://github.com/anaregdesign/MicrosoftFabricHandson/assets/6128022/8cf5c79c-332c-4541-828f-24b825673ee2">





## 主要コンポーネントの概要

### レイクハウス

### データフロー

### パイプライン





# Handson

## レイクハウスの作成
## データのコピー
## データ加工
## セマンティックモデル
## 
