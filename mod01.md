# モジュール 1: ガバナンスとコンピューティング ソリューションを設計する


## Lesson 1: ガバナンスを設計する


## Lesson 2: コンピューティング ソリューションを設計する


### 比較表/決定表
Azureには多数のコンピューティングサービスが存在する。

適切なサービスを選択するためのフローチャートを利用できる。
https://docs.microsoft.com/ja-jp/azure/architecture/guide/technology-choices/compute-decision-tree

### Azure Virtual Machines (VM)


#### 概要
https://azure.microsoft.com/ja-jp/services/virtual-machines/

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

単一VM: 99.9%
可用性セット: 99.95%
可用性ゾーン: 99.99%

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

