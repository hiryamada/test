# Module 1 コンピューティング ソリューションを設計する


## コンピューティングサービスを選択する


### 比較表/決定表
Azureには多数のコンピューティングサービスが存在する。

適切なサービスを選択するためのフローチャートを利用できる。
https://docs.microsoft.com/ja-jp/azure/architecture/guide/technology-choices/compute-decision-tree

### IaaS


#### Azure Virtual Machines (VM)


##### 概要
■概要

- Windows VM: https://docs.microsoft.com/ja-jp/azure/virtual-machines/windows/overview
- Linux VM: https://docs.microsoft.com/ja-jp/azure/virtual-machines/linux/overview

Azure上で、Windows ServerやLinuxを仮想マシン（VM）として実行。
物理ホストの管理が不要。
任意のアプリケーションをVM上で実行できる。

■イメージ

Windows Server や、Linuxの、構築済みの様々なイメージを選択してVMを数分で起動。OSをインストールする必要がない。

Linuxディストリビューション
https://docs.microsoft.com/ja-jp/azure/virtual-machines/linux/overview#distributions

■サイズ

https://docs.microsoft.com/ja-jp/azure/virtual-machines/sizes

様々なサイズを指定して、VMのスペック（CPU、メモリ等）を指定できる。後から変更することもできる。

タイプ＞シリーズ＞サイズ
汎用＞Dv4＞Standard_D2_V4

■ネットワーク帯域幅

https://docs.microsoft.com/ja-jp/azure/virtual-network/virtual-machine-network-throughput

仮想マシンのサイズによってネットワーク帯域幅が決定される。

■ディスク（マネージドディスク）

https://docs.microsoft.com/ja-jp/azure/virtual-machines/managed-disks-overview

VMはOSディスク、データディスク、一時ディスクを持つ。

ディスク単位でスナップショットを取ることができる。

■接続

SSH, RDP, Azure Bastionを使用して接続し、管理操作を実行できる。

■仮想ネットワーク

https://docs.microsoft.com/ja-jp/azure/virtual-network/virtual-networks-overview

VMは仮想ネットワーク（VNet）にデプロイされる。
仮想ネットワークはVPNや専用線でオンプレミスに接続することができる。オンプレミスからVMにプライベートに接続できる。

■NIC (ネットワーク インターフェイス)

https://docs.microsoft.com/ja-jp/azure/virtual-network/virtual-network-network-interface-vm

Azure VM は、NICを使用して、別のVM、Azureのサービス（ロードバランサーやストレージ等）、インターネット、オンプレミスと通信する。

VMにはNICが接続される。

NICはパブリックIPアドレスとプライベートIPアドレスを持つことができる。

■バックアップ

https://docs.microsoft.com/ja-jp/azure/backup/quick-backup-vm-portal

Azure Backupを使用して、VM全体のバックアップをかんたんに構成することができる。

■ロードバランサー

https://docs.microsoft.com/ja-jp/azure/load-balancer/load-balancer-overview

Azure Load Balancerなどの負荷分散サービスと組み合わせて、復数のVMに負荷分散を行うことができる。

■スケーリング

https://docs.microsoft.com/ja-jp/azure/virtual-machine-scale-sets/overview

需要または定義されたスケジュールに応じて、VM インスタンスの数を自動的に増減させることができる。

※需要（demand）とは、VMの利用率の高さのこと。VMで稼働しているアプリケーションに多数のエンドユーザーが接続して利用している場合などに、需要が多い、という。

■拡張機能

https://docs.microsoft.com/ja-jp/azure/virtual-machines/extensions/overview

カスタムスクリプト拡張機能、DSC拡張機能などを使用して、VMの構成を自動化できる。

拡張機能を使用して、VMに様々なソフトウェア（ドライバ等）を導入することもできる。

■デプロイ

https://docs.microsoft.com/ja-jp/azure/azure-resource-manager/templates/overview
https://docs.microsoft.com/ja-jp/azure/azure-resource-manager/bicep/overview

ARMテンプレート、Bicepファイルなどを使用して、デプロイを自動化できる。

■可用性

https://azure.microsoft.com/ja-jp/support/legal/sla/virtual-machines/

VMのSLAが定義されている。

- 単一VM: 99.9%
- 可用性セット: 99.95%
- 可用性ゾーン: 99.99%

■価格

https://azure.microsoft.com/ja-jp/pricing/details/virtual-machines/windows/
https://azure.microsoft.com/ja-jp/pricing/details/virtual-machines/linux/

秒単位で課金される。

コストを節約する方法
- Azureハイブリッド特典
- スポットインスタンス
- 予約
- リージョンの選択
- 使用していない間VMを停止・削除する

### PaaS


#### Azure App Service


##### 概要
■概要

- 製品ページ: https://azure.microsoft.com/ja-jp/services/app-service/
- ドキュメント: https://docs.microsoft.com/ja-jp/azure/app-service/overview
- 価格: https://azure.microsoft.com/ja-jp/pricing/details/app-service/windows/

WebアプリやWeb APIをホスティングできるPaaSサービス。VMや言語ランタイムを管理する必要がない。さまざまなデプロイ方法をサポート。負荷分散やスケーリングの機能が組み込まれている。

■言語

.NET、Java、Ruby、Node.js、PHP、Pythonに対応

■デプロイ

- ローカルGit
  - https://docs.microsoft.com/ja-jp/azure/app-service/deploy-local-git?tabs=cli
- Visual Studio Codeの拡張機能「Deploy to Azure」を使用する
  - https://marketplace.visualstudio.com/items?itemName=ms-vscode-deploy-azure.azure-deploy
- Visual Studioから「発行(publish)」する
  - https://docs.microsoft.com/ja-jp/visualstudio/deployment/quickstart-deploy-aspnet-web-app

■継続的デプロイ(CD: Continuous Deployment)

- GitHub Actions
  - 「azure/webapps-deploy」アクションを使用
  - https://docs.microsoft.com/ja-jp/azure/app-service/deploy-github-actions?tabs=applevel
- Azure Pipelines
  - 「AzureRMWebAppDeployment」タスクを使用
  - https://docs.microsoft.com/ja-jp/azure/devops/pipelines/tasks/deploy/azure-rm-web-app-deployment?view=azure-devops

### サーバーレス


#### Azure Functions


##### 概要
■概要

https://docs.microsoft.com/ja-jp/azure/azure-functions/functions-overview

- サーバーレス - コンピューティングリソースをオンデマンドで提供
- イベントの処理 - 多数のAzureサービスと連携
- C#、Java、JavaScript、PowerShell、Python、TypeScriptなどを利用できる
- [Durable Functions](https://docs.microsoft.com/ja-jp/azure/azure-functions/durable/durable-functions-overview?tabs=csharp): ステートフルな処理をサポート

### コンテナー


#### Azure Container Instances (ACI)


#### Azure Kubernetes Service (AKS)


#### Azure Service Fabric


### 大規模な並列コンピューティング, HPC


#### Azure Batch


## プロビジョニング・構成管理


### ARMテンプレート


### Azure Bicep


### VMの構成


#### DSC機能拡張


#### カスタムスクリプト機能拡張


### サードパーティ


#### Chef


#### Puppet


#### Ansible


#### Terraform


### Azure Automation


#### 概要
1. プロセス自動化
  - Runbook（スクリプト）を管理、実行
  - たとえばサーバーの起動・停止・スケーリングなどを自動化
2. 構成管理
  - サーバーの「望ましい状態」を宣言、適用 - SC
  - サーバーのファイル等の変更を記録 - 変更履歴
  - サーバーの構成をクエリ - インベントリ
3. 更新管理
  - サーバーに「更新プログラム」を適用

2014/10/28 一般提供開始
https://azure.microsoft.com/en-us/updates/general-availability-azure-automation/

#### プロセス自動化 - Runbook
■Runbookとは

PythonスクリプトやPowerShellスクリプトを自動的に実行する機能。

多数の開発済みスクリプトが「ギャラリー」に登録されており、それらを利用することができる。

■Runbookの実行

Azure portalから手動で実行
PowerShellから実行
Automation APIで実行
Webhookから実行(Azure DevOps, GitHub等を含む)
Azureアラートから実行
別のRunbookから実行
スケジュールで実行

■スケジュール実行

Runbookを指定の時刻に（1回または繰り返し）実行できる。

https://docs.microsoft.com/ja-jp/azure/automation/shared-resources/schedules

Runbook を 1 つ以上のスケジュールにリンクできる。

■Webhookからの実行

https://docs.microsoft.com/ja-jp/azure/automation/automation-webhooks

HTTP 要求により、Azure Automation で特定の Runbook を開始することができます。

■Runbookの実行の詳細

Runbookが開始されると「ジョブ」が作成される
ジョブは「ワーカー」で実行される

■Runbookのワーカーの実行環境

- Azure サンドボックス
  - Azureでホストされる環境
- Hybrid Runbook Worker
  - オンプレミスのデータセンターや他のクラウドでホストされる環境

#### 構成管理


##### Azure Automation State Configration
任意のクラウドまたはオンプレミスのデータセンターのノードについて PowerShell Desired State Configuration (DSC) の構成を記述、管理、およびコンパイルできる Azure 構成管理サービス

##### 変更履歴とインベントリ
■変更履歴
Linux と Windows の仮想マシンおよびサーバー インフラストラクチャの変更を追跡できます。 

サービス、デーモン、ソフトウェア、レジストリ、ファイル全体にわたって変更を追跡し、不要な変更を診断したりアラートを生成したりすることができます。

■インベントリ

ゲスト リソースでクエリを実行して、インストール済みのアプリケーションやその他の構成アイテムを可視化できます。

#### 更新管理


##### Azure Automation Update Management
https://docs.microsoft.com/ja-jp/azure/automation/update-management/overview

OSの更新プログラムを管理。

対象
- Azure での Windows および Linux 仮想マシン
- オンプレミス環境の物理・仮想マシン
- その他のクラウド環境での物理マシン・仮想マシン

■スケジュール

デプロイ スケジュールを作成して、定義済みのメンテナンス期間中に更新プログラムがインストールされるように調整できます。

#### 価格
https://azure.microsoft.com/ja-jp/pricing/details/automation/

プロセス自動化、構成管理、更新管理の料金が発生。

### Azure Automanage


#### 概要
https://azure.microsoft.com/ja-jp/services/azure-automanage/

VM 管理のベスト プラクティスを自動的に実装。

VM の構成が適用されたベスト プラクティスからずれているVM を検出し、自動的に目的の構成に戻す。

※ベストプラクティス: 「Azure クラウド導入フレームワーク」で定義されているビジネス継続性とセキュリティに関するベストプラクティス

2020/9/22 パブリックプレビュー(Windows Serverに対応)
https://azure.microsoft.com/ja-jp/updates/announcing-the-public-preview-of-azure-automanage/

2021/5/2 Linuxに対応
https://techcommunity.microsoft.com/t5/azure-governance-and-management/azure-automanage-for-virtual-machines-public-preview-update/ba-p/2161199

2021/6/29 Azure Arc enabled serversに対応
https://azure.microsoft.com/ja-jp/updates/automanage-arc/

