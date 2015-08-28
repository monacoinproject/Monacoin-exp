#Monacoin 0.10.2.2 Lyra2REv2 プレビュー版
- - -
このプレビュー版はアルゴリズムの切り替えをテストしたい人向けのもので、Lyra2REv2の採用を決定するものではありません。  
上記のバイナリは[こちら  ](https://github.com/monacoinproject/monacoin/tree/pending-0.10.2.2-Lyra2REv2)のソースをビルドしたものになります。

**このプレビュー版は開発中のもので、予期せぬ不具合が発生する可能性があります。**  
必ず -testnet、-regtest のどちらかの引数を指定して起動してください。  
-testnet、-regtest のどちらの引数も指定せずに実行した場合、現行バージョンのウォレット等のデータを操作します。  
自己責任において利用してください。

**Download : [Monacoin-exp-0.10.2.2_Lyra2REv2-preview.zip](https://github.com/monacoinproject/Monacoin-exp/archive/0.10.2.2_Lyra2REv2-preview.zip)**

win32版のzip内には下記で説明するテスト例のバッチファイルも入っています。

##テストネット
引数 -testnet を指定した場合、テストネットに接続します。  
ただし、Monacoinではグローバルなテストネットは構築されていないので、ローカル環境で複数起動してテストしてください。  
0.10.2.2では同期が完了していない状態で`setgenerate`でブロックの生成が出来ません。  
ですので0.8.7.1もテストネットに参加させ、0.8.7.1で最初のブロックを生成し、qt上の<span style="color:red">（同期していない）</span>が消えてからマイニングをしてください。  

テストネットでは5Block目にLyra2REv2・DGWv3にフォークします。

##リグレッションテスト
引数 -regtest を指定した場合、リグレッションテストモードで起動します。  
こちらはローカル環境を前提に作られているテストモードで、addnodeしたノード以外には接続に行きません。  
また、コマンド`setgenerate`にてマイニングをせずにブロックを生成することができます。

`例）デバッグコンソールにて「setgenerate true 10」と入力すると10ブロック生成します。`

リグレッションテストでは20Block目にKGW、40Block目にDigiShield、60Block目にLyra2REv2・DGWv3にフォークします。  
Monacoinでは採掘後に120ブロック経過しないと採掘したコインの操作はできませんが、このモードでは自由にブロックが生成できるため短時間で送金などの確認をすることができます。  

##テスト例
port、rpcportが重複しないようにすれば１台のPCで複数クライアントを起動することができます。  
Monacoin_0.10.2.2-Lyra2REv2-preview.zip 内に0.8.7.1、0.10.2.2を１台のPCで同時に立ち上げ、テストをするサンプルを用意しました。  
以下、testnet、regtest での実行方法です。  

####［testnet］
先に testnet-0.10.2.2.bat を実行し、続いて testnet_0.8.7.1.bat を実行してください。  
先に起動した monacoin-qt_0.10.2.2-Lyra2REv2-pre.exe に monacoin-qt_0.8.7.1.exe が接続し、2クライアントでテストネットが形成されます。  

####［regtest］
先に regtest1-0.10.2.2.bat を実行し、続いて regtest2-0.10.2.2.bat を実行してください。  
先に起動した monacoin-qt_0.10.2.2-Lyra2REv2-pre.exe に後で起動した monacoin-qt_0.10.2.2-Lyra2REv2-pre.exe が接続し、2クライアントでリグレッションテストのネットが形成されます。  

##マイニング
MonacoinprojectではLyra2REv2のrpcマイニングは[こちら](https://github.com/tpruvot/cpuminer-multi)のcpuminer-multiを用い、Ubuntu上にて動作を確認しています。  
0.8.7.1と異なり、ソロマイニングの際には自身のウォレットアドレスを指定する必要があります。

`例）./cpuminer -a Lyra2REv2 -o localhost:29402 -O user:pass  --coinbase-addr=mqg8XsampleaddressXXXmonacoinNfZnD`

bitcoin api `getwork`が廃止になっているので、使用するマイナーによっては`getwork`を無効にするオプションを指定する必要があるかもしれません。

