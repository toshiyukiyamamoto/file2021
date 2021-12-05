# 認証を支えるネットワーク技術

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
<p>最下層からトランスポート層まで正しく機能すると、送信元と宛先のアプリケーション間でデータの送受信ができるようになる</p>
<p>主要プロトコル：「IP」「ICMP」「ARP」</p>
</details>