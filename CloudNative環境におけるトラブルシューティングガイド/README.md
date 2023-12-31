https://event.cloudnativedays.jp/cndt2023/talks/2001

# CloudNativeな環境におけるアラートや障害などのシステムトラブルに対してどのように調査対応したか

## HPAを設定することで自動的にpodをふやすことができる

## CloudNative環境のトラブル

- クラウド自体の障害
- オートスケーリングでも救えないケース
    - 設定したMax値やクラウドリソースの上限に当たる
        - Maxまでスケールしても足りない時がある
    - オートスケールが間に合わない
        - kubernetesのデプロイメント、node poolのスケールが間に合わないなどは結構ある
    - 依存する外部システムのキャパシティの限界
    - 期待通りオートスケールできない
        - CPU使用率を元にオートスケール設定することが多い。CPU使用率が上がる前に
- オートヒーリングでも救えないケース
    - オートヒーリングとは監視に基づいて問題を検知し自動的にシステムを自動で修復する機能
    - 再起動しても同じ問題が起こる場合救えない。

## どのような準備が必要か

- 自分の運用しているシステムの構成を理解する
- 自分たちのシステムの正常な状態を定義する
    - SLOを定義
- トラブルを観測できるようにする
    - SLOを達成できているか確認できる状態を作る。各種メトリクスの取得
- トラブルを調査できるようにする
    - メトリクス、ログ、トレーシングを使って、問題の深掘りできるようにする

## トラブルシューティング

1. 何が起きているか把握する
    1. いつどこで何が
        1. どこで(どのマイクロサービス)

リクエストは増えているか、オートスケールは発動しているか

正常な部分と異常な部分を切り分ける

1. 問題の原因を調査する
    1. 仮説を立てる、裏付けるデータがないか確認するの繰り返し
        1. メトリクスに変化が起きた時刻のログを見る
        2. 気になるログを見つけたら、エラーはいつから発生していたか確認
- エラー増加の原因調査 とにかくアプリケーションログを見て気になるエラーメッセージがないか見る。　いつから発生したか、発生場所、タイミングに偏りがないか
- れいてんし増加やタイムアウトエラー トレースをみて、時間がかかっている場所特定
- 切り口を変える

## よくある事例

- kubernetes nodeの不調
    - podが動いているnodeを確認するとエラー率が上昇していた他のサービスのpodも存在
- 想定を超えるリクエスト数の増加
- Databeseセッションのリーク
    - 復旧対応:失敗したらlibenesProbeがエラーとなる対応を入れて、自動的に再起動するようにした
