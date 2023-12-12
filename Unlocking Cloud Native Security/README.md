https://event.cloudnativedays.jp/cndt2023/talks/2065

https://speakerdeck.com/kyohmizu/unlocking-cloud-native-security

## マルウェア種類

- kinsing malware
    - phpunitやwordpresなどの脆弱なコンテナイメージを主に悪用
- ransomware in the cloud
    - aws s3を標的とするランサムウェア攻撃事例
        - S3バケットのデータ流出
        - **githubにawsのクレデンシャルアップすると5分以内に随時監視していて取られる**
- malicious python package in pypl
    - 正規の難読化ツールを装ったもの

## Code Security

- アプリケーションコードの脆弱性対策
    - 静的コード解析ツール導入
    - アプリケーションへの動的解析 trivy dependbotなどを使う

## Container Security

- Dockerfileの堅牢化　 trivy dependbotなどを使う
    - Dockerfileのベストプラクティスに準拠する

## Cluster Security

- クラスタコンポーネントの堅牢化と脆弱性管理
    - kubelet,kube-api-serverなどの適切な設定
    - RBACによる権限管理、Secretの暗号化、NetWorkPolicyの設定など
    - リソースのポリシーチェック
    - ワークロード監視ツール falco,テトラゴンが有名

## Cloud Security

- 適切なIAM設計、アカウントへのアクセス元制限など
- 組織全体でのアカウント管理
- WAFログ、ネットワークログ、イベントログなどの監視
