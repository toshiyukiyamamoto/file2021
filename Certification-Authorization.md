
  <style>
    summary {
        display: block;
    }
    summary::-webkit-details-marker {
        display: none;
    }
  </style>

 ![title](https://media3.giphy.com/media/dP0WAyNyTKSNqNm6zn/giphy.gif?cid=ecf05e47vit498dvz0uxn91drn9zqfyuhrfob40os8etnypw&rid=giphy.gif&ct=g"title")

**認証と認可**  
①認証フロー -認証ってなんなの?-  
・認証とは「通信の相手が誰（何）であるかを確認すること」  
認証の3要素
コンピュータの世界も含め、現実世界で「認証」を行うための要素には以下の3つ  
<details><summary>WHAT YOU ARE (inherence factor)</summary> 
顔貌、声、指紋、署名など、その人自身を提示して、相手にアイデンティティを確認させる方法です。小さなコミュニティでは、お互いの顔や声を相互に知っているため、面と向かえば相手が誰かはわかりますね。認証が完了する、ということです.</details> 
<details><summary>WHAT YOU HAVE (possession factor)</summary>  
身分証、携帯電話等、その人だけが持っているものを提示することによって認証をします。ある程度コミュニティが大きくなってくると、お互いの特徴を覚えきれなくなります。そんな場合は身分証明書を提示して、相手を認証すると思います。
また、その身分証には顔写真がプリントしてあることも多く、結果として WYA に依存するものも少なくありません.</details>   
<details><summary>WHAT YOU KNOW (knowledge factor)</summary>   
パスワード、秘密の質問等、その人だけが知っていることを提示して認証をします。コンピュータの世界で最も多く使われるファクターでしょう。
一般的に、上記3つのうちいずれか1つを満たすことで、認証が完了することが多いです。しかし、より確実な認証を行いたい場合は、Multi-Factor Authentication (MFA) という考え方で、複数のファクターを確認することもあります。  </details>  

②認証系の攻撃とその対策について  
<details><summary>辞書攻撃</summary>  
ユーザーが一般的な単語と短いパスワードを使用する傾向があるという事実を利用する攻撃。ハッカーは一般的な単語のリスト(辞書)を使用して、多くの場合、単語の前後に数字を付けて、企業のアカウントに対してユーザー名ごとにそれらの攻撃を試みます。(ユーザー名は一般的に社員の名前に基づいているため、判別するのは非常に簡単です。)</details>
<details><summary>総当たり攻撃</summary>   
プログラムを使用して、ありそうなパスワードまたはランダムな文字セットを生成します。この攻撃は、Password123のようなわかりやすい脆弱なパスワードから始まり、被害はそこから広まります。このような攻撃を実行するプログラムは、通常、大文字と小文字のバリエーションも含めて試みます。</details>
<details><summary>トラフィック妨害</summary>   
この攻撃では、サイバー犯はパケットスニファなどのソフトウェアを使用して、ネットワークトラフィックを監視し、通過したパスワードをキャプチャします。電話回線の盗聴や傍受と同様に、ソフトウェアで重要な情報を監視およびキャプチャします。パスワードなどの情報が暗号化されていない場合、このタスクが簡単になるのは明らかです。ただし、使用する暗号化方式の強度によっては、暗号化された情報であっても解読できる場合があります。</details>
<details><summary>中間者攻撃</summary>   
この攻撃では、ハッカーのプログラムは、渡される情報を監視するだけでなく、通常はWebサイトまたはアプリになりすまして、通信している両者の間に積極的に割り込みます。これにより、プログラムはユーザーの信用情報や口座番号、社会保障番号といった機密情報を取得できるようになります。中間者(MITM)攻撃は、ユーザーを偽のサイトに誘導するソーシャルエンジニアリング攻撃によってしばしば悪用されます。</details>
<details><summary>キーロガー攻撃</summary>  
サイバー犯は、ユーザーのキーストロークを追跡するソフトウェアをインストールして、アカウントのユーザー名やパスワードだけでなく、ユーザーが認証情報でログインしていたWebサイトまたはアプリを正確に収集できるようにします。このタイプの攻撃では通常、最初に悪意のあるキーロガーソフトウェアをユーザーのマシンにインストールさせる別の攻撃の餌食になります。</details>
<details><summary>ソーシャルエンジニアリング攻撃</summary>   
ユーザーから情報を取得するための幅広い方法.  
<p>使用される戦術</p>
フィッシング
信用情報の提供、悪意のあるソフトウェアをインストールするためのリンクのクリック、または偽のWebサイトへのアクセスをユーザーに促すメールやテキストなど。  
スピアフィッシング  
フィッシングに似ているが、ユーザーについて既に収集された情報に依存する、より巧みに作成された、カスタマイズされたメール/テキストを使用します。たとえば、ハッカーは、ユーザーが特定の種類の保険口座を持っていることを把握してそれをメールで参照したり、企業のロゴやレイアウトを使用して正当なメールを装います。  
ベイティング  
攻撃者は、感染したUSBまたはその他のデバイスを、社員が拾って使用するよう、公共または雇用主の場所に置きます。
Quid pro quo -サイバー犯は、ヘルプデスクの社員などになりすまし、ユーザーから情報を取得する必要がある方法でユーザーと通信します.</details>  

**パスワード攻撃の阻止**
 - 強力なパスワードを設定  
覚えやすい/推測しにくいパスワードを推奨. 大文字と小文字、数字、特殊文字の適切な組み合わせが役立つ. できれば、一般的な単語や一般的なフレーズの使用は避ける. サイト固有の単語(パスワードでログインしているアプリの名前など)は絶対に避けてください. (既知の脆弱なパスワードの辞書に含まれていないか、パスワードをチェックすることを推奨)

 - 社員の教育  
ソーシャルエンジニアリングの戦術に対する最善の防御策の1つは、ハッカーが使用する技術とその認識方法をユーザーに伝えること  
しかし、強力なパスワードや教育だけでは十分ではない！  
サイバー犯は、コンピューティング能力を使用することで、高度なプログラムを実行し、膨大な数の信用情報を取得または試行することができる. 企業はシングルサインオン(SSO)や多要素認証(MFA)などのツール(2要素認証とも呼ばれる)を採用する必要がある  

 - SSOは、従業員が1組の信用情報ですべてのアプリとサイトにログインできるようにすることで、パスワードを排除(ユーザーに必要なことは、強力なパスワードを1つ覚えるだけ). MFAでは、OneLogin Protectなどのアプリケーションによって生成されたPINや指紋認証など、ユーザーがログインするときに追加の情報が必要. (※この追加情報により、サイバー犯がユーザーになりすますことは、はるかに困難になる)  