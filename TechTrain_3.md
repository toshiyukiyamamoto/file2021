## 技術研修第3部　「環境作成」  

#### 【目標】
Dockerにて開発環境が作れる  
開発を始めるための知識・環境が作れるようになっている  

#### 【目安日程】  
part1 4日  
part2 4日  
  

### ゴール1  
以下要件のDockerfileの作成
※ベースイメージは CentOS7系 latest

・WEBサーバーコンテナ構築（Apache）※webページ表示されることを確認  
・PHP（7.4系）  

【やること】  
・Dockerコマンドの習得 → docker のコマンド調べる  
・1-1 Apacheとphpを第2部で立ち上げたコンテナへ素の状態でインストールしてみる  
※phpinfo(); の表示もできればしてみてください  
・1-2 上記構成を Dockerfile でまとめる  
（Dockerfileの仕様を調査、Dockerfile の理解 公式サイトにて）  
・1-3 docker buildをして試してみる  
・1-4 自作の Dockerfile でコンテナを立ち上げ  

