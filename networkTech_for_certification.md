# 認証を支えるネットワーク技術
![title](https://lh3.googleusercontent.com/ABJ7UeKVb5f0VUHD1wP5gqRK7KsrHJB6FvwZEeEdWSlePesS2aoREnv-IrJbnCY1iMfQ6ia6cjFcxwyrfC0owq8JL_FJdJIlK3kT50ZFzh6HeHluMi6q0PtueGHjsdNT_MU4k7Eu8fRcI2KBoK4ss3k1vD5DX_N-dW4zLUnEcM-L02AzThkQMTavNKxa0icwHu8Jn8jnPcIDpyeaKBuFirh8Ti3I5t6LBNaM2ulW_hP-JYBFxhvN4Uq8vr0sYOjpgYLINSGbMH0vX_OVUlWPk2xxx35qcxYrDzrkUlm75ZGO8pwpe1KUCYrviRplXKcd-71yzZ6O2v51TGZR0cdRUf-mA1fFGhflo9DpZVWP73Wm7tpDFO0Uv5whHTQa-YSHr0iztHPlhq74YVTIcpEpuKRMB9Q_FKbi6XC2zWVFTisYVBYl-uZURXlO3WN1V9IVPoEbGwNik3Gb0rwV2WnfMebCWknlifQ7SMqNhBapxyY1N5PxaUg1ri2_4q6BjfkmXbX3kk0ioE6J_F2cttS1otZhAYK3kwlaMAEywer0beVuhDcE6fOhawU05ynGr-6Vphq-2cS3dtwZUZvxa226e_32-2SvUQs90cgMgbTvJ8Pp7egLUuxB3lI-mH4ooVEhvsVytIjV9_sHOl3Jo0n-5lOwiLd9p9riqn-_t2i3gzn1eWHJ1FT30OtiMawvIzsQqPud_-gmLTQMKbInRlLdPT6c=w324-h183-no?authuser=1"title")  

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
![title](https://lh3.googleusercontent.com/MgUn3RNHfEBiIHemqjrAzlCmnsoNs2xtXaWC0KfLxa1odpB5cNhXALxLMQoZ__RxaOvuucNOGvw_UYZ8k_Jn-6kxuV9iagNqxZJXdmdmKZcgNDZsjvJyxPFyLkq0f58VcE-OVY5Ful4CMHBnn8PrkHMWBxbySlogUqgFPRK0bfNUWJQMkF3CnjvGxOY5Dkq9nzdfXxHYRNccxdQKkoYTjV5SFN71qaRXDk3nVzyxwQrHosDdh1RV_Va-GZ-DSU1RAEmk6mK5qzHqt-aE6nmOSdkbo3pO-EHN0MzLwmxY7a68W716ZGBh--0YlNde_qW5fkZlq9ouZP7mnpFp8Bk7AlX1v8ybri9DLeXRoliotIJ76PUhEZFH6AHVO_H_imqDwdj8sI6YsdSLIuxv9KKmOJzOb8qfw_FaCqq3btAiXFvVThH8ZTtxFTg_848n0KVoEA5isrtzjg2NjbLQoqL6zh6vf2uZr02aGhFymgn9RCSSs0X-VdXUTKG7gs0AkHfdPpIPJ0UT2V2_Ae_Wr2CwqxdeVK_jXrOtbkjuIfalhtumlie5-D2tN_HicnkMxW39k3WfjCFMqp-ajwbbYETxhTgJ1szJx2jExO3r8tbOU1tncy6ARNw_ctS6s9MpHMYtIujctyhy-6p7Fv4LzUDsjpXzwyUS15oSekAhDq2aAhsGskoSiU2V_7mWMM9bC4TNboFWCPg8AkqnFHRJT2scl8XE=w1961-h653-no?authuser=1"title")
  
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

![title](https://lh3.googleusercontent.com/vRh2PqTyxvePeXglZrxwn73JX8jyy2W4m8oT5okff1R1SyM-iAykWsMVblTq7fZ7gMl_IQz2_ouuoXFLFYfinxql-T-Tj0KLQ4p_ldcjDjnPgnNcwvSW9rSdYBrstGa93kSpM9AAaIa6XdlYq6dm2LkEOdq8MId36OI-lOKKyZqNal-vVyUvUUJR1xRX7ynY0GePHiWKx1Zsz4MFnziioe5ss7SW5t2m8rqoRMhJzcuq74v-2bJ5AR1p6SnLvkpvrApuESDYSA-yuZfEztIVQf-4GchZhs64kSaPuy40Mv0fKXySkim38y8oUQ1O-v9TM8sd8IhucMn1yUAUr2qum2FJkNUsqLI_3LjWjVcuAKJeN6r13vDmSYiiPuzXG-fZerN_AvQAfwWh2zsAGenS8MgWRDcFylfx8eCOFDPZfALNJjihj8FdJT1TPv5qSxmpZLhpnS6iBoBvZinX2Ugy3s-J9FxvAstOAHp1V2HVdCm6_1UjrB5a5oWJ9dhoSlGIYaWbt6qpSwgp80krRT0-YDGlpeb_DhUkbk64nSbCo0l7ZTdavy3vfJJLlcnM-YYUPDmtmy3DHsn5WCyZfWQgLdjflgAJu3tnTGWK8m1sMnPp_j7UyYPD5V2agx3RAURRWTUdTcBi4SGBi-f0uvd9fLIGctet200PyjuN8eqmSL3rxZyKWt2VTN93QTq_Lm1qUmizpt0AVMR3d4leA33-WZfA=w1900-h555-no?authuser=1"title")  
  
<details><summary>1層 ネットワークインターフェイス層</summary>   
<p>同一のネットワーク内でデータを転送する役割</p>
<p>例)ルータやレイヤ3スイッチで区切られる範囲 or レイヤ2スイッチで構成する範囲</p>
<p>主要プロトコル：有線の「Ethernet（イーサーネット）」, 無線LAN（Wi-Fi) , PPP</p>
</details>  
  
  ![title](https://lh3.googleusercontent.com/1ZHSq6tXMJa4l3daH_UyCvW3MavxsOJR6lnilMuHcAegzoTe4oTZKp15mlnQ6ATo39v7pdnbz1C8L_VBVIdEGI7bfyxyQJsMa0g_ypY4sgFzk65jMNy5vjjp5linvM4co2KXqoIvgRWP4edidN0hgsFYOgYjNMi9Df-KQbQEpPBx-HaUmFTA7wsygeeAUt3BTOksVaYwJgpsoOqXh5uTY81gpliL5VfICv7vJ0if1Pkr_WFK6L6XqpgI2DKWYW1JjW7osdRs4rmyNKtxpeVTxzKCc1QogZwfaXPbChdJIvvhJIoal8dyFsLR68BLBDf0xx2mYTYWejO07PiGTRv-4SVLuhUa6nVe-1av4_Gm4FiR8nMWBTY5BmvZEaMJiQ3lclUYlT__QxsjZEFI24nGaOA5Dlk9Tnl9JHjLwFrPDl0SyuIl_q-QZsfgWW7AQNmW7kwYWtgem7oVhU2wa3eSCN1O-ApvOZ6GHaCjqaop6QpvuKyW-SoFloDjEWe4GBrWw4vGNPPoXqF62wbCvklKLNhe_v5iy4pmzZY15rtkqLtL1uTeycct61zLWVGoqkTWxA6_qCl0uOfAgXBT1yA2aA0v9UgjFT7NMz7iOykQMIqk-3I_7xTCxfXRxcJ6FZDKboVmDtDvCsVY1QDVY9VUHUxsA59pAKelZ8BH-QkEp100nbE6ctqpF9JLLTJ-vXSNIj_Y-Q5__AAE4YxIWthoD6w5=w2000-h664-no?authuser=1"title")  

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

