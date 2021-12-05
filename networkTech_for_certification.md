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
<p>ネットワークはたくさんのネットワークが存在し、そこに色々な機器を接続していることで実現</p>
<p>主要プロトコル：「IP」「ICMP」「ARP」</p>
<p>「ルータ」：多数のネットワーク同士を接続してデータ転送を行う</p>  
<p>「ルーティング」：ルータによるネットワーク間のデータ転送</p> 
<p>「エンドツーエンド通信」：ネットワーク間のデータ転送</p>
</details>  

![title](https://lh3.googleusercontent.com/NUALJ9zvguvqvqg3xTXL9Fj8R6YpPYDCkm1qDNYlrwzq3tbBQpjUHKdYq7QMxEx9lUjVRwlQydFPLTt-QBOMhFYl3qmgmTTMdFtxcDc5v331cQ-GQ8gdVg8kqkJCiu_YjIn-nADNfKlaGkAo7wOm6GJcTii4wxtra9MteeWskDbvmSHh8K5PiibUyngKbMm15b-d13vOT8oi50AwL0y3AIVVCMKqxLFSv6-S96ODzYk8_-JYpP6Rkw2z3DMNflaX6UiMcqDa8YEkeyhgnm1AVix0Xm-UsAHjMGhUb5zekdrs7CRXUpCZYoWaXV5Q89OEiJpkGZRw1lou2QofotWl0c0TUafA3ybBxp_zUmwM18dSwDWljFkbWck6aEwIR4Kj-k1pcDnk_cliXDfJZwLxYfmCcADIo9HVyxTJngxl4p0B_xhnVEd7AZMonoItGK8r3yXV-xFQhdmGQRbFGBH5T31Y4aSI_sUgAEj_k140eVPpEPkeqt0ZfTCwmyyxo7ZTCt_282ilRPCueyetbGNKGcLi6ZjS1qwLgR6Qarrw8rzcOlwuTMDPmKtCqbZKldx2-gIveknhWX16uKR60QKM3ehbtB9IGiITBygoWruMxwfVpSeUWqkU6l91sNqy7Ue3LQpK_POsJJZxKTj6Q7dfl1h90X-6F4-_6IXEX7OgYEX5BrxZhHyu_4BN_axUGLVsKJWlt6UwrLGCge0T4wyV8wSn=w1900-h555-no?authuser=1"title")  
  
<details><summary>1層 ネットワークインターフェイス層</summary>   
<p>同一のネットワーク内でデータを転送する役割</p>
<p>例)ルータやレイヤ3スイッチで区切られる範囲 or レイヤ2スイッチで構成する範囲</p>
<p>主要プロトコル：有線の「Ethernet（イーサーネット）」, 無線LAN（Wi-Fi) , PPP</p>
</details>  
  
  ![title](https://lh3.googleusercontent.com/pw/AM-JKLX08uLLb2DG_aXSe5fO_O-aUjV7Y7_0aAObXf-P91-UdoY9stHlHp2r3OGSB2k0q4gwPmUeqmg8MisathJBJH_lFKpNGC3uU876UDqXy8C3qEa5-nM7bO7k8t1JgfziSmnmO_sBtegmsx5c5ZNUCzxZWhIjoaXW5OoJLHVnPOtjzk9KerO8nZjfDtQW2Z7G-JWyn9zZwefafAdn5pdH_CMO0-1x1P5mbcCme1Uk25XwybUtoVBPE--k-62SmtDWhUbmPMqMDCnSjeHQUdIL6aKUaMr8pNAKLCrZusdP_tVguY5Gset7oYMZbnZeH2xP5WcB_nVyT8iIoUkj0onf-xLLGksLya1r_z7D2Ifi3K-jLBWSNaUF_GMYilAkx6xGwhmih-BL5-S1jaba2cNr-x7DoedhWEJI_EAHoTllAZSmwEScFby0A8fKF_Yhlyx7l586WIbPuI6PkVUILbsgOsvQ0l7aUCLeFSCpArZqFtBFXpaUAaHU2Ss5kP2wldKyRUGHggOeH9D-dAy7FMIOaC7zUPZoqz-ZMt-sFtJ5Lz4IitElC4ssF--GSftKEpoNBHwah78GcrPYfYZ_22UfC2r4TjmabnZ5OeFf-q9sfUaId9sSX3egi3blBkp4JpOa0t-TJbsmreSIIJeohenQuKbzpwNuRwXo7_XSJJsrRLIrVIlCXek5kPBt2DFscfO-83FXVVO1839nnLPpiPXyWAo68uo7na7aLaERKormgRbfLQE=w2000-h664-no?authuser=1&authuser=1"title")  

## セッション  
