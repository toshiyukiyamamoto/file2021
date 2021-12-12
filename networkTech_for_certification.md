# 認証を支えるネットワーク技術
![title](./pic_certification/giphybetworkgif.gif)  

### 目次  
 - TCP/IP  
 - cookie
 - セッション  
 - Webstorage  

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
![title](./pic_certification/pic1.jpg)  

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

![title](./pic_certification/pic2.jpg)  

<details><summary>1層 ネットワークインターフェイス層</summary>   
<p>同一のネットワーク内でデータを転送する役割</p>
<p>例)ルータやレイヤ3スイッチで区切られる範囲 or レイヤ2スイッチで構成する範囲</p>
<p>主要プロトコル：有線の「Ethernet（イーサーネット）」, 無線LAN（Wi-Fi) , PPP</p>
</details>  
  
![title](./pic_certification/pic3.jpg)  

## Cookie（クッキー）  
<details><summary>Cookieとは？</summary>   
<p>正式名称：HTTP Cookie</p>
<p>WebサーバアプリケーションがWebブラウザに対し特定の情報を保持させておく仕組み</p>
</details>  

### Cookieの役割  
HTTPは一往復(リクエストし→レスポンスする)で通信が切断される  

<img src="./pic_certification/pic4.jpg" width="30%">  

そのため、サーバーは以前の状態を全く覚えていない!(前のページからの続き？/関連したアクセス? etc..) => ステートレス(stateless)  
しかし、以前の状態を覚えていないとネットショッピングのような商品を購入できるWebサイトは作れない  
>ネットショッピングをするのにログインし、商品をカートに入れ、購入します</p>
ページ遷移するたびに通信は切断されている.サーバーは、誰がカートに入れ、購入したのかを全く覚えていない</p>
これでは、非常に困る💦  

状態を保持する(ステートフル)ために**Cookie**を使用し、サーバーがクライアントに対して識別できる一意の値を渡し、クライアントはリクエストする時にその値を教えてあげれば、サーバー側で識別できるようになり、それぞれの状態を覚えることができる  

サーバーからのレスポンスメッセージに「Cookieを保存してください」という指示があれば、クライアントは指示に従いCookieを保存する  
クライアントにCookieが保存されていれば、クライアントは常にリクエストメッセージに「このようなCookieがあります」とサーバーに教える仕組みになっている  

<img src="./pic_certification/pic5.jpg" width="30%">  
  
サーバーは、レスポンスメッセージに**Set-Cookie**ヘッダを付与することで、クライアントに対して「Cookieを保存してください」と指示することが可能  
**Set-Cookie**ヘッダには、Cookieの有効期限やCookieを送るドメイン、有効パスなどの各属性があり「 ; 」で区切って記述することで設定が可能  
```
// レスポンスメッセージ（Set-Cookieヘッダの構文）
Set-Cookie: 名前=値;[expires=有効期間(日時)];[Path=URL相対パス];[Domain=ドメイン名];[secure];[httponly]
```  
```
// レスポンスメッセージ（Set-Cookieヘッダの記述例）
Set-Cookie: a=b; expires=Mon, 15-Aug-2016 12:00:00 GMT; path=/; domain=xxxx.com; secure; httponly
```
 - Cookieによって各ユーザが閲覧するWebページの内容をカスタマイズすることなどが出来る.  
 - WebブラウザでWebサービスにアクセスをする際にログインをして利用する場合がありますが、事前にログインをしているときとログインが必要な場合があるが、これはサーバがログイン情報を記憶しているのではなくクライアントマシンのWebブラウザのCookieに記憶されており、以前にログインしたことあるサイトであればIDとパスワードの情報を同時に送信しているので自動的にログインが出来ていることなる.  
 - CookieはHTTPリクエストヘッダに格納されておりサーバに送信されます.  
  
## セッション  
https://www.ipa.go.jp/security/awareness/administrator/secure-web/chap6/6_session-1.html  
https://qiita.com/7968/items/ce03feb17c8eaa6e4672

 - Cookieに一意の値を入れ、リクエストするときにCookieにある値も一緒に送ってもらうことで、識別可能になり、一連の処理として扱えるようになる  
 - Cookieを利用することで、セッション管理が行える  

## Web Storage API
https://developer.mozilla.org/ja/docs/Web/API/Web_Storage_API

