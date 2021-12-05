# 認証を支えるネットワーク技術
![title](https://media0.giphy.com/media/10PNyg7YOcaBQA/giphy.gif?cid=ecf05e47syqs9c3autgdgvctxy7v777ntrvbn6s9eniqw8ld&rid=giphy.gif&ct=g"title")
### 目次  
 - TCP/IP  
 - セッション  
 - cookie/Webstorage  

参考：  
本「Webを支える技術」6章  

## はじめに
<details><summary>認証とは？</summary>   
<p>通信の相手が誰（何）であるかを確認すること</p></details>  

## TCP/IP
<details><summary>TCP/IPとは？</summary>   
<p>コンピュータネットワークにおいて、世界標準的に利用されている通信規則。機器やOSが異なっても共通のプロトコルを用いて通信を成立させるもの</p></details>  
<details><summary>TCP(Transmission Control Protocol)</summary>
<p>送ったデータが相手に届いたか、その都度確認しながら通信するやり方</p>
<p>正確な信号を送信する通信の規格を定めたもの</p>
</details>  
<details><summary>IP(Internet Protocol)</summary>
<p>IPアドレスと呼ばれる数値を付与しその数字を用いて通信先の指定及び呼び出しを行いネットワーク通信を行うこと</p>
</details>  
  
### TCP/IPプロトコル通信のネットワークアーキテクチャ
![title](https://lh3.googleusercontent.com/4YIXyjxwY4Il3nySinfU_LfFs3V74kANNarB1Wz0bh7vo4Wjk4Lzo7CnDKW4012vnD9PQEqEvY4IkP2qjRUmKEOsiCevSkkyLfoCWH0EX3Ha73Bg3RetxKXlc0j0Kg3JtuAzxKihcFauWq881QUyMHh7HPzi3IO66pnQtboyDcqTrKElwr7SpULOMnYsA4EZe2qyI-b5VKfRvJ22aR1XdeBuSfU0FX3q4G39bqzg4iGmdwoMKKouMAtQuB7KdOD__Kd_SeaSD3wJ7TheUuGac54REWDqRKa66vzzYB21cbKraOCHV67IUZpT8D323OLXuSPJ3s6tGbltWNxSkAUrYLrR2_mXoTWi8z39kPZuMY5KMWzZAhPshEwFUagklFUorA9fQFwZ5hw1VH6tsZi1MfB_7q-Pq30Y7DUC7wng8zjIYlMgpmrT70j4SOvVeQC0dG-PARyWMSJAjw_CvjQLKbzSzzj4zRj5ctZ_kuwsnzoKuqRHz7fQr8qW1m0WshesheE3cCTREM1lROGgqa_36xFqrdNvsZ11zG-t7qcZyh32c9cuhwwgtIXijzzzm6v8VfohN2JTJUNoCrDcZWCZjOHcLvqK5p1X1p3HdMUm64VdAgs4a9lHmK3xiNkTeAglBuxbielZQZxtdD_8xxFUHK84djj8G56Pn0vYK35Za7W88W9ZImqAMdvpQpIfaKkGuBZeVffkm3P7FsQ8VUwCCA1v=w1961-h653-no?authuser=1"title")
  
<details><summary>4層 アプリケーション層</summary>   
<p>アプリケーションで扱うデータのフォーマットや手順を決める役割</p>
<p>アプリケーションは基本的には人間が扱うため、文字や画像など人間が認識できるようにデータを表現</p>
<p>主要プロトコル：「HTTP」「SMTP」「POP3」「IMAP4」「DHCP」「DNS」</p>
</details>  
<details><summary>3層 トランスポート層</summary>   
<p>データを適切なアプリケーションに振り分ける役割</p>
<p>最下層からトランスポート層まで正しく機能すると、送信元と宛先のアプリケーション間でデータの送受信ができるようになる</p>
<p>主要プロトコル：TCP , UDP</p>
</details>  
<details><summary>2層 インターネット層</summary>   
<p>複数のネットワーク間のデータ転送を行う役割</p>
<p>ネットワークはたくさんのネットワークが存在し、そこに色々な機器を接続していることで実現</p>
<p>主要プロトコル：「IP」「ICMP」「ARP」</p>
<p>「ルータ」：多数のネットワーク同士を接続してデータ転送を行う</p>  
<p>「ルーティング」：ルータによるネットワーク間のデータ転送</p> 
<p>「エンドツーエンド通信」：ネットワーク間のデータ転送</p>
</details>  

![title](https://lh3.googleusercontent.com/OjHnbXemVc_VxqA7c-Vwht66uW0kuF3UXSV2zcCovKvmSEzP0UKZJzLcp5WXMasrws2xvxSVNvrV-sqaoWS8PfV8pRFR-Mk7vTQ76Lsf6yp-jZoQqV38JzbWLnNYWO49WmFCrKQRPR6pDDk9L6HIumoEGl4JauV61SBtr6WCx-3T-I5ZmSw1xq-knwrOxcaIV3AL7Irys5CQpppv_INOYkHsUl_2YIj3zm0k6MxH4cJq02r5_3Ja9i8UYUdFye65RXkibNi3Xffro-Tf1EkMrXqyKq2iLkcdWDXZnb4vFyvwR1ga-qMpDhi5bmMGepjc_kB1lNWKCFA1aFYXhuDRbbxfECRvB_6BrGMq-Xep3wDHTR95R-8FJsDsSU-DHps1O-HIwoeY19pN4ovMUUUpyMFpfAQf-A0kvGR6q9QQ57soYVwDU-U5QgYzabrUcXVZGsWwu-R53Ohjgkt_wsF5NATaIogjWzNCmQaJg1Ti3aaYNqiFczR1QQHAAOCzOJRaINP7eicHgpcJanmwQ1xBEa_I7keFzdMzTInyZDbg2urPIb4uf7fxP1-OFfWiG-YXNTjlyMlTVUoDl4aYNSTPSUSxGx4OXDNEac4O7eE2SAe8GQg-aq-yIrHmmotES6xdZAkld8tAdkYRh7iLjdytVP_cCMDSef340v1gaJzXJtCl_vKie6uBZjbAG1Dvg127EQ0Fl7-y4Lt2vpv-evv4lfjF=w1900-h555-no?authuser=1"title")  
  
<details><summary>1層 ネットワークインターフェイス層</summary>   
<p>同一のネットワーク内でデータを転送する役割</p>
<p>例)ルータやレイヤ3スイッチで区切られる範囲 or レイヤ2スイッチで構成する範囲</p>
<p>主要プロトコル：有線の「Ethernet（イーサーネット）」, 無線LAN（Wi-Fi) , PPP</p>
</details>  
  
  ![title](https://lh3.googleusercontent.com/eh0KnFTywly7n5foTa_brEjtVV2L7yvfEuI-LDUPb5UU8j4G_oP52T_x4Vu86IJLAHnhjhFRmbolYy7q_sn11xhdxS3wV1ljIM4_kpUI38dc4cUpTn28tl06osx1Q9CRjL638i_ZBw-v2c_TwLjt53H-gcjHw7i3-a5iGRa6k66ZnGicOBfzvkz2Uy06aYgqm3T_2lu22K4YTinCNCkNWTVjpZRTwNysBjwcSIRW0XLR0M2ZGsmjRuZgJcCNIyBHf_SaESIN4Sl5nGZu0hNtEAMbUr3RoPH1Twgz3S3QV0GPfoL9oNgi-njVkvTOqkYebNdAeDTfbn3IFSrALidmArVy68sRDdWpqzMvkXL7Q1PcSviiHCimU81srJmmc-QHH9ZynGx2mjtjxLZo7gvO4ihiY8ivmfXUq5uaxMBGVdoE6gCN561czjv9mrVTVgDIo6EwkXgNGR7UA4B-F3TkvyNRj0OYT0IRlfuPLHZ_emffwhAVLe_THcKcc55Wu81IRXEskp-J4lILj_5qkg3t-h27izaJLRkZvH2bAm2C2LlHGnT-cnxjJWJDHU4s_yRQEroe79vMy3mxGIvaXOih5mYFc65BRiaVZJAGNtJ2RoBRNTi58Z6idt1EukJYz7kUAm8wnh76kfmyMnIk8ar6T5WsjNxte3vtjzMLkGKhgq1qQnyy0Mg2Pw66B0PE0KZSmAPeAQYIIrvZLzAfgiIdxpz3=w2000-h664-no?authuser=1"title")  

## セッション  
https://www.ipa.go.jp/security/awareness/administrator/secure-web/chap6/6_session-1.html  
https://qiita.com/7968/items/ce03feb17c8eaa6e4672

 - Cookieに一意の値を入れ、リクエストするときにCookieにある値も一緒に送ってもらうことで、識別可能になり、一連の処理として扱えるようになる  
 - Cookieを利用することで、セッション管理が行える  

## Cookie（クッキー）  
<details><summary>Cookieとは？</summary>   
<p>WebサーバアプリケーションがWebブラウザに対し特定の情報を保持させておく仕組み</p>
</details>  

 - Cookieによって各ユーザが閲覧するWebページの内容をカスタマイズすることなどが出来る.  
 - WebブラウザでWebサービスにアクセスをする際にログインをして利用する場合がありますが、事前にログインをしているときとログインが必要な場合があるが、これはサーバがログイン情報を記憶しているのではなくクライアントマシンのWebブラウザのCookieに記憶されており、以前にログインしたことあるサイトであればIDとパスワードの情報を同時に送信しているので自動的にログインが出来ていることなる.  
 - CookieはHTTPリクエストヘッダに格納されておりサーバに送信されます.  
  
## Web Storage API
https://developer.mozilla.org/ja/docs/Web/API/Web_Storage_API

