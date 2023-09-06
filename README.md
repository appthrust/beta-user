こんにちは！クラフトマンソフトウェアのreoringです！ 僕達は「HerokuやVercelといったアプリケーション開発プラットフォームを自分のクラウドにすぐ構築できるサービス」を水面下で開発してきました。ある程度形になってきたので、ベータテストに参加してくださる方を募集したいと思います！この投稿を読んで、少しでも興味を持たれた方は、ベーターテスト申し込みフォームからお申し込みください。

# ウェブサービス開発の難問: 速度、品質、コストに振り回されていませんか？

今世界中でよりソフトウェアに対する需要が増えていると思います。なので、これまでよりもアプリケーション開発の速度とか、品質の向上、機能の拡充などが、以前より求められてくるようになっていると感じています。

アプリケーションやサービスのユーザとか、顧客からはアプリケーションをより早くリリースしてほしい、とか、品質を向上させてほしい、機能を追加してほしい、もっと安く作って欲しいと言われます。しかし、こうしたことは複雑になっているソフトウェア開発ですべてを満たすことはとても難しいことだと私達は考えています。

アプリケーションは開発して、テストを行い、本番環境にデプロイする方法を考え、インフラを構築し、アプリケーションをデプロイし、本番環境で動作確認を行い、さらに常に正しく動作しているか見守り続ける必要もあります。次のバージョンをリリースする際には、壊れていないかを確認したり、実際ユーザが使いだしたときにちゃんと動作しているか不安になります。さらにサービスが成長していくと顧客の情報が漏洩していないか、ハッキングなどの被害にあわないかなど、セキュリティも気になりだし、サービスが障害で停止しないかなど、このようなことを考えると夜も眠れなくなります。

本来は、このような事を気にせずにアプリケーション開発にだけ貴重な時間を費やしたいのです。

<!--
source: [ソリューションインタビュー](https://innovation.esa.io/posts/267)
-->

### 具体的な苦痛: これらがあなたのプロジェクトを阻んでいませんか？

- アプリケーションをデプロイするための、AWSやGCPといったインフラ環境の構築やアップデート、動作確認するためのコストや時間がかかりすぎる
- アプリケーションが本番環境で正常に稼働しているか安心するために確認する時間が多くかかっている
- 次のバージョンが、本番環境で正常に動作するかわからずリリース速度が落ちている
- アプリケーションやインフラ、クラウドのセキュリティが安全かわからない、安全か確認するために時間がかかりすぎる
- セキュリティやスケーラビリティを確保するためにAWSのサーバレスサービスを使用しているが、開発体験がよくない
- Herokuを使いたいがAWSのリージョンを自由に選べない
- Vercelを使いたいがローカルのデータベースに接続できない
- PaaSを使いたいが自分のAWSに配置できず、データなどの資産管理ができない
- AWSでKubernetesを使いたいが構築や保守にコストがかけられない

# 開発がスイスイ進むプラットフォーム「AppThrust」

これらの課題を解決するために、僕たちはが開発している開発プラットフォームが「AppThrust」です。

AppThrustは、上記の課題を一挙に解決するプラットフォームを提供します。AWSやGCPのインフラの構築から本番環境での安定運用、始めてのリリースからバージョンアップまで、手間と時間を削減しながら、品質の高いソフトウェア開発の実現を目指します。

## AWS環境構築・保守
AppThrustは本番環境ですぐに使えるセキュリティやスケーラビリティを考慮したインフラをAWSに構築します。このAWSはあなたが用意した自分のAWSです。なので、どのAWSリージョンを使うか、データやクラウド資産は全てご自身のAWS内に配置されます。もしもAppThrustが無くなってしまっても、ご自身のAWSに構築された環境には何も影響はありません。そのまま使い続けることができます。
## Kubernetes基盤
AppThrustが構築するプラットフォームはKubernetesが基盤になっています。その為Kubernetesのエコシステムや開発体験が全て活用できます。AWSに構築されたKubernetes環境はAppThrustによって管理され、クラスタバージョンのアップデートや、セキュリティアップデートが自動で提供されます。しっかりと本番環境の利用に耐えるKubernetesクラスタを構築、運用していくには専門のインフラエンジニアが数名必要になるくらいコストがかかります。AppThrustでは本番利用に耐えるクラスタの構築が瞬時に行えます。
## コスト最適化
AWS Lambdaのようなサーバレスと同様に、AppThrustにデプロイされたアプリケーションは使用されていないときは起動されません。アクセスがあると瞬時に起動し、アクセスが無くなると停止します。Kubernetesのノードは負荷状況によって自動的に増減し、AWSのコストが最適化されます。
## ビルド&デプロイ
AppThrustの管理画面からデプロイしたいアプリケーションのソースコードがあるレポジトリを指定すると、そのレポジトリのDockerfileがビルドされ、AppThrustにデプロイされます。
## 通信量制御
GitHubのレポジトリにあたらしい変更がpushされるとAppThrustは自動的にビルドを開始し、新しいリビジョンを配置します。しかし、このリビジョンはまだリリースされていません。新しいリビジョンにはまだ通信がきていません。新しいリビジョンに通信を1%だけ向けて、新しいリビジョンがエラーなく動作しているか確認できます。1%の通信で問題ないことが確認できたら、2%, 10%と通信量を増やしていき、安定性を確認しながら徐々にリリースすることができます。

# 課題が解決することで、ひいてはこんなベネフィットがあります
AppThrustを使うと、これまでアプリケーションを開発して公開するために必要だったAWSへのインフラ構築やセキュリティ対策、ビルド環境の整備やデプロイメントパイプラインの構築などの初期作業が不要になります。これによってアプリケーション開発者がやることは開発したソースコードをGitHubへpushするだけになり、本番グレードのインフラでアプリケーションをすぐに公開できます。すぐに公開できると、競合よりはやくアプリケーションをユーザに提供できます。

アプリケーション公開後も、インフラ障害で夜中に叩き起されることや、アプリケーションの不具合対応に悩まされることがなくなります。アプリケーションのアップデートはGitHubにソースコードをpushするだけです。

# 将来的にこうなっていきます
## オートパイロット
GitHubへの変更でリビジョンが作成され、その後AppThrustが自動的に新しいリビジョンへの通信量を増加させ安定性を確認します。問題なく動作していれば新しいリビジョンへの通信量を徐々に増加させていき、問題があれば安定していたリビジョンに戻ります。アプリケーション開発者はGitHubに変更を加えるだけでアプリケーションが次々にリリースされていきます。
## モニタリング
AppThrustではPrometheusやLokiといったオープンで標準的なモニタリングプラットフォームを提供する予定です。このモニタリングで得られる様々な指標を参照し、オートパイロットが機能します。
## ミドルウェア
PostgreSQLやAWSのRDSデータベース、 RedisなどのミドルウェアをUIから配置するだけでAppThrustがデプロイし運用管理されます。デプロイしたアプリケーションとミドルウェアをUI上から接続するとアプリケーションから使えるようになります。
## Kubernetesクラスタのダウンタイム無しアップデート
通常Kubernetesクラスタのバージョンを更新する際は稼動しているクラスタを、稼動した状態で更新します。更新時にKubernetesのコアコンポーネントが障害になってしまうと、クラスタ障害になり本番環境も障害になってしまいます。AppThrustではKubernetesクラスタそのものをBlue/Greenで切り替えて完全に無停止でKubernetesクラスタを更新できるようになります。


# ベータユーザーを募集しています
## 実施内容
実際にAppThrustを使ってご自身のAWSにプラットフォームを構築、アプリケーションが稼動させます。
## 実施期間
2023年9月10日~2023年9月30日 (期間は予告なく変更・終了となる場合がございます)
## 募集対象
- アプリケーション開発者
- AWS環境上にKubernetesを構築・運用しているインフラエンジニア
## 募集人数
- 5名
## 募集期間
2023年9月6日~2023年9月10日 (期間は予告なく変更・終了となる場合がございます)
## お申し込みフォーム
https://docs.google.com/forms/d/1e4_iWsIr23R4-lrA62DNGDzjNZ-2KcF0wreN00imaoA/edit

ご入力いただいた個人情報は、ベータテストユーザー募集及びサービスの改善のために利用いたします。
当社におけるその他取り扱いはプライバシーポリシーに従います。ご同意の上、ご応募ください。

# 上記のような課題で困っている方で、ベータテストにご協力いただける方はご連絡ください
ベータテストを通じて得られたデータや皆様からのご感想・ご意見をもとに、正式サービス開始に向けてさらに品質向上に努めてまいります。皆様のご協力を心よりお待ちしております。
