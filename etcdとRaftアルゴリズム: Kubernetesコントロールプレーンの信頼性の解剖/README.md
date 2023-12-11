https://event.cloudnativedays.jp/cndt2023/talks/2029

## etcdとは

## ****Raftとは****

- コンセンサスアルゴリズムの1種
- paxosと比べ耐障害性や性能を維持しつつ理解しやすいように設計
- 採用されているで意表的なサービス
    - etcd, kafkaなど ****Raft導入により****zookperがいらなくなった
- raft basics
    - leader,follwoer,candidateのいづれかの役割をもつnode
    - Leader election
    - log replication
    - node構成はK数台ノード構成が推奨
    - 

## etcdの****Raftの実装を読む****
