## 1章：理解しやすいコード
**コードは他の人が最短時間で理解できるように書かなければならない**  
 - 理解するまでにかかる時間を短縮する  
　┗「理解する」：変更を加えたりバグを見つけることができる  
 - 遠い未来の自分が見た時にわかるように  
 - プロジェクトに途中参加したメンバーがわかるように  

**でもやるんだよ**  
 - 優秀なプログラマを目指して、バグの少ないコードを作り出そう

## 2章：名前に情報を詰め込む
### 明確な単語を選ぶ 

```php
//Bad
def GetPage(url) :    //インターネットからページを取得                        
……
```
→どこからページを取ってくる(Getしてくる)のかわからない(ローカルキャッシュ？データベース？)  


```php
//Good  
def FetchPage(url) :  //もしくはDownloadPage                          
……
```
 ※「 explode()とsplit() 」
→explode()は”何かを分割する”を伝えれるが、split()との違いは名前からはわからない  
2つの関数違い：区切り文字に正規表現を使えるか／使えないか
https://ameblo.jp/gonta3333/entry-10384282091.html

### 汎用的な名前を避ける
**エンティティの値や目的を表した名前で選ぶ**
```php
var euclidean_norm = function (v) {
      var retval = 0.0;
      for (var i = 0; i < v.length; i += 1) 
            retval += v[i] * v[i]; 
      return Math.sqrt(retval); 
}; 
```
⬇︎変数の目的や値を表すものがイイ(“vの２乗の合計”を表現する)
```php
var euclidean_norm = function (v) {
      var sum_squares = 0.0;
      for (var i = 0; i < v.length; i += 1) 
            sum_squares+= v[i] * v[i]; 
      return Math.sqrt(retval); 
}; 
```
※これならバグも見つけやすい！  
sum_squares += v[i];　　//合計する「square(2乗)」がない。バグだ! 

**しかし、汎用的な名前も使う場面はある!**  
tmp(情報の一時的な保管)  

```php
//Good
if (right < left) { 
    tmp = right;  
    right = left; 
    left = tmp; 
} 
```
※このような場合は、tmp という名前で「この変数 には他に役割がない」という明確な意味を伝えている。(生存期間は数行のみ)  


```php
//Bad
String tmp = user.name();
tmp += " " + user.phone_number(); tmp += " " + user.email();
...
template.set("user_info", tmp); 
```
※この変数にとって大切なことは「一時的な保管」ではない。  
わかりやすくするには、user_info のような名前に！


### ループとイテレータ( i・j・k・iter )
〜でも、これよりもイイ名前がある！〜  
例.クラブ所属のユーザを調べるループ
<font color="Red">X</font>悪い例
```php
for (int i = 0; i < clubs.size(); i++)
      for (int j = 0; j < clubs[i].members.size(); j++) 
            for (int k = 0; k < users.size(); k++) 
                  if (clubs[i].members[k] == users[j]) #バグ
                      cout << "user[" << j << "] is in club[" << i << "]" << endl;
```
※if文のmembers[]とusers[]のインデックスが逆になっとる  
⬇︎イテレータが複数ある時は、もっと明確な名前をつける！
```php
if (clubs[ci].members[ui] == users[mi])  #バグだ!最初の文字が違う
```
⬇︎
<font color="Red">◯</font>良い例
```php
if (clubs[ci].members[mi] == users[ui])
```

### 具体的な名前を使う
┗「ServerCanStart」を「CanListenPort」に  
　　　〜抽象的-　　　　　　〜具体的〜  
※任意のTCP/IPポートをサーバがリッスンできるか確認するメソッド

例. DISALLOW_EVIL_CONSTRUCTORS
 (メモリリワークなどの問題につながる”悪”のコンストラクタを許可しない規約)  
マクロの定義
```php
#define DISALLOW_EVIL_CONSTRUCTORS(ClassName) \ 
      ClassName(const ClassName&); \
      void operator=(const ClassName&); 
   
class ClassName { 
   private: 
      DISALLOW_EVIL_CONSTRUCTORS(ClassName); 
   public: ... 
}; 
```
※ 「EVIL(悪の)」 という言葉よりも、このマクロが「許可していないもの」を明確にするほうが大切(実際には operator=() メソッドも許可していない)  
↓あまり刺激的ではなく、より具体的な名前に変更
```php
#define DISALLOW_COPY_AND_ASSIGN(ClassName) ... 
```
### 名前に情報を追加する
〜名前は短いコメントのようなものだ！〜  
┗16進数の文字列を持つ変数だったら？→「hex_id」とする (IDフォーマット優先)  
値の単位・時間やバイト数のように計算できるものがあれば、変数名に単位を入れる  
<font color="Red">X</font>悪い例
```php
var start = (new Date()).getTime(); // ぺージの上部
...
var elapsed = (new Date()).getTime() - start; // ページの下部 
document.writeln(" 読み込み時間:" + elapsed + " 秒 "); 
```
※getTimeが秒ではなくミリ秒を返すため、このままだとうまく動かないので変数名に「 _ms 」を追加して、コードを修正  
<font color="Red">◯</font>良い例  
```php
var start_ms = (new Date()).getTime(); // ページの上部
...
var elapsed_ms = (new Date()).getTime() - start; // ページの下部 
document.writeln(" 読み込み時間:" + elapsed_ms / 1000 + " 秒 ");
```
|           関数の仮引数               | 単位を追加した仮引数   |
|:-----------------------------------|:--------------------|
| Start(int delay)                   | delay→delay_secs    |
| CerateCache(int size)              | size→size_mb        |
| ThrottleDownload(float limit)      | limit→max_kbps      |
| Rotate(float anple)                | angple→degrees_cm   |

重要な属性を追加する
|  状況  | 変数名   |  改善後  |
|:------|:--------|:----------|
| passwordはプレインテキストなので処理をする前に暗号化すべき| password|plaintext_passwoed|
| ユーザが入力したcommentは表示する前にスケープする必要がある| comment |unescaped_comment|
| htmlの文字コードをUTF-8に変えた | html | html_utf8 |
| 入力されたdataをURLエンコードした  | data | data_urlenc |

→セキュリティのバグのような深刻な被害が出るところに使おう！

※ハンガリアン記法は、使われなくなっている  
<変数名の最初や最後に目印（接頭辞・接尾辞）を付けることで、変数の意味を掴みやすくして間違いを減らす表記方法>  
https://www.agent-grow.com/self20percent/2017/12/13/thinking-about-hungarian-notation/  
https://wa3.i-3-i.info/word13959.html

### 名前の長さを決める
〜でも短ければ良いわけではない〜  
スコープが小さければ短い名前でもOK  
```php
if (debug) { 
    map<string,int> m; 
    LookUpNamesNumbers(&m); 
    Print(m); 
} 
```
※コードを理解するための情報(変数の型・初期値・破棄方法)が近くにあるので、mでも大丈夫

頭文字と省略形  
<font color="Red">◯</font>
```
evaluation→eval
document→doc
string→str
```
<font color="Red">X</font>  
```
BackEndManager→BEManager
```
ん？知らない。これは暗号？？

不要な単語を捨てる  
┗ ConvertToString()→ToString()  
　 DoServeLoop()　 →ServeLoop()




### 名前のフォーマットで情報を伝える
クラス名：CamelCase (キャメルケース)  
変数名：lower_separated (小文字をアンダースコアで区切る)
など..

その他のフォーマット規約  
『JavaScript: The Good Parts』(Douglas Crockford, O'Reilly, 2008)

**まとめ**  
 - 明確な単語を選ぶ。例えば、Get ではなく、状況に応じてFetchや Download などを使う。   
 - tmpやretvalなどの汎用的な名前を避ける。ただし、明確な理由があれば話は別だ。  
 - 具体的な名前を使って、物事を詳細に説明する。ServerCanStart() よりも CanListenOnPort() のほうが明確だ。  
 - 変数名に大切な情報を追加する。ミリ秒を表す変数名には、後ろに「ms」をつける。これからエスケープが必要な変数名には、前に 「raw」をつける。       
 - スコープの大きな変数には長い名前をつける。スコープが数画面に及ぶ 変数に 1 ~ 2 文字の短い暗号めいた名前をつけてはいけない。短い名前は スコープが数行の変数につけるべきだ。   
 - 大文字やアンダースコアなどに意味を含める。例えば、クラスのメンバ 変数にアンダースコアをつけて、ローカル変数と区別する。 

## 3章：誤解されやすい名前
〜「他の意味と間違えられることはないか？」と自問自答する〜

例① filter()
```php
results = Database.all_objects.filter("year <= 2011")
```
→filterは「選択する」or「除外する」のどちらかわからない  
┗「選択する」：select()  
　「除外する」：exclude()

例② Clip(text, length)  
<font color="Red">X</font>
```php
#textの最後を切り落として、「...」をつける 
def Clip(text, length):
... 
```
┗「最後からlength文字を削除する(remove)」  
　「最大length文字まで切り詰める(truncate)」のどっち？  
<font color="Red">◯</font>
```php
def Truncate(text, max_chars):
…
```
┗ 1.関数名をTruncate(text, length)に変更  
　 2. length を明確にする（今回は「文字列」を意味しているのでmax_chars）

### 限界値を含めるときはminとmaxを使う
<font color="Red">X</font>
```php
CART_TOO_BIG_LIMIT = 10
if shopping_cart.num_items() > CART_TOO_BIG_LIMIT:
    Error(" カートにある商品数が多すぎます。") 
``` 
┗「未満(限界値を含まない)」  
　「以上(限界値を含む)」のどちらかわからない  
<font color="Red">◯</font>
```php
MAX_ITEMS_IN_CART= 10
if shopping_cart.num_items() > MAX_ITEMS_IN_CART:
    Error(" カートにある商品数が多すぎます。")
```
### 範囲を指定するときは first と last を使う
<font color="Red">X</font>  
```
print integer_range(start=2, stop=4)
```
┗ これが示すのは、「2,3」or「2,3,4」のどっち？(あるいはその他？)  
<font color="Red">◯</font>  
```
set.PrintKeys(first=”Bart”, last=”Maggie”)
```
┗ 終端を範囲に含めるのなら、firstとlastを使うべし！


### 包含 / 排他的範囲にはbeginとendを使う

例. 10月16日に開催されたイベントを全て印字したい  
```
PrintEventsInRange("OCT 16 12:00am", "OCT 17 12:00am") 
                      〜begin〜           〜 end 〜
```
### ブール値の名前
・ブール値の変数やブール値を返す関数の名前を選ぶときはtrueとfalseの意味を明確にしなければならない！  
<font color="Red">X</font>  
```
bool read_password = true;
```
┗「パスワードをこれから読み取る必要がある」  
　「パスワードをすでに読み取っている」のどちらなのか不明  
<font color="Red">◯</font>  
```
bool need_password = true;   

bool user_is_authenticated = true;
```
・ブール値の変数名は、頭に is・has・can・should などをつけてわかりやすくする  
・名前を肯定系にしたほうが短くて、声に出して読みいやすい！

### ユーザの期待に合わせる
例. get*()  
getで始まるメソッドは「軽量アクセサ」であるという規約 
```php
public double getMean() { 
         // 全てのサンプルをイテレートして、total / num_samplesを返す。
}  
   ... 
} 
```
もしget*()の規約を知らない場合は、コストが高いと知らずに呼び出してしまうかもしれない  
→コストの高さが事前にわかるように computeMean() などの名前に変えるべき
(もしくは、コストの高くない実装に変えるべき） 

### 複数の名前を検討する
例)webサイトの実験用設定ファイル
```php
experiment_id: 101
the_other_experiment_id_I_want_to_reuse:100
[ 以下、変更が必要な情報だけ書き換える ]
```
では「the_other_experiment_id_I_want_to_reuse」の名前はどうするか？  
4つから選ぶ  
┗1.template  
　2.reuse  
　3.copy  
　4.inherit  



***よし、Copy でいこう！***
```
experiment_id: 101 
copy: 100 
... 
```
しかし、copy: 100だけでは、
「この実験を100回コピーする」 or「これは100回目のコピーだ」
のどちらかわからない  
→他の実験を参照している言葉だということを明確にするには、copy_experiment という名前に変えるとイイ


## 4章：美しさ
①適切な改行  
②複数のコードブロックで同じようなことをしていたら、シルエットも同じようにする  
③コードの「列」を整理すれば、概要が把握しやすくなる
④ある場所でA・B・Cのように並んでいたものを、他の場所でB・C・Aのように並べてはいけない！  
→意味のある順番を選んで、常にその順番を守る  
⑤空行を使って大きなブロックを論理的な「段落」に分ける

### 一貫性のある簡潔な改行位置とクラス
※適切な改行を入れ、繰り返されたコメントは簡潔にする(仮引数を一行で書く)

### メソッドを使った整列
〜ヘルパーメソッドを使ってみる〜  
<font color="Red">X</font>   
```php
DatabaseConnection database_connection;
string error;
assert(ExpandFullName(database_connection, "Doug Adams", &error) == "Mr. Douglas Adams");
assert(error == "");
assert(ExpandFullName(database_connection, " Jake Brown ", &error) == "Mr. Jacob Brown III");
assert(error == "");
assert(ExpandFullName(database_connection, "No Such Guy", &error) == ""); 
assert(error == "no match found"); 
assert(ExpandFullName(database_connection, "John", &error) == ""); 
assert(error == "more than one result"); 
```
⬇︎  
<font color="Red">◯</font>  
```php
CheckFullName("Doug Adams", "Mr. Douglas Adams", ""); 
CheckFullName(" Jake Brown ", "Mr. Jacob Brown III", ""); 
CheckFullName("No Such Guy", "", "no match found"); 
CheckFullName("John", "", "more than one result"); 

void CheckFullName(string partial_name, 
                   string expected_full_name, 
                   string expected_error) {
// database_connectionはクラスのメンバになっている。 
string error;
string full_name = ExpandFullName(database_connection, partial_name, &error); 
assert(error == expected_error);
assert(full_name == expected_full_name); 
} 
```
※これによって良い副産物が得られる  
・重複を排除したことでコードが簡潔に！  
・テストケースの大切な部分(名前やエラー文字列)が見やすくなった  
・テストの追加が簡単になった  

### 縦の線を真っ直ぐにする
<font color="Red">X</font>  
```php
CheckFullName("Doug Adams", "Mr. Douglas Adams", ""); 
CheckFullName(" Jake Brown ", "Mr. Jacob Brown III", ""); 
CheckFullName("No Such Guy", "", "no match found"); 
CheckFullName("John", "", "more than one result"); 
```
<font color="Red">◯</font>  
```php
CheckFullName("Doug Adams" , "Mr. Douglas Adams"  , ""); 
CheckFullName("Jake Brown" , "Mr. Jacob Brown III", ""); 
CheckFullName("No Such Guy", ""                   , "no match found"); 
CheckFullName("John"       , ""                   , "more than one result"); 
```
※縦の線を揃えることで流し読みが楽にできる(「似ているコードは似ているように見せる」)


### 一貫性と意味のある並び
コードの並びがコードの正しさに影響を及ぼすことは少ない  
ただし....  
できれば意味のある順番に並べる！  
・対応するHTMLフォームの<inputフィールド>と同じ並び順にする  
・「最重要」なものから重要度順に！  
・アルファベット順に並べる  

### コードを「段落」に分割する
・似ている考えをグループにまとめて、他の考えと分けるため  
・視覚的な「踏み石」を提供できる  
・段落単位で移動できるようになる  

<font color="Red">X</font>
```php
#ユーザのメール帳をインポートして、システムのユーザと照合する。 
#そして、まだ友達になっていないユーザの一覧を表示する。 
def suggest_new_friends(user, email_password):
    friends = user.friends()
    friend_emails = set(f.email for f in friends)
    contacts = import_contacts(user.email, email_password) contact_emails = set(c.email for c in contacts)
    non_friend_emails = contact_emails - friend_emails
    suggested_friends = User.objects.select(email__in=non_friend_emails) 
    display['user'] = user
    display['friends'] = friends
    display['suggested_friends'] = suggested_friends
    return render("suggested_friends.html", display) 
```
<font color="Red">◯</font>
```php
def suggest_new_friends(user, email_password): 
    #ユーザの友達のメールアドレスを取得する。 
    friends = user.friends()
    friend_emails = set(f.email for f in friends) 
    
    #ユーザのメールアカウントからすべてのメールアドレスをインポートする。 
    contacts = import_contacts(user.email, email_password)
    contact_emails = set(c.email for c in contacts) 

    #まだ友達になっていないユーザを探す。
    non_friend_emails = contact_emails - friend_emails
    suggested_friends = User.objects.select(email__in=non_friend_emails) 

    #それをページに表示する。
    display['user'] = user
    display['friends'] = friends 
    display['suggested_friends'] = suggested_friends 

    return render("suggested_friends.html", display)
```

## 5章：コメントすべきことを知る
〜コメントの目的は、書き手の意図を読み手に知らせることである〜  
**まとめ**
#### コメントすべきではないこと
 - コードからすぐに抽出できること  
 - ひどいコードを補う「補助的コメント」  
  →コメントの前にコードを修正！  
#### 記録すべき自分の考え  
 - なぜコードがこうなっているのか(監督コメンタリー)  
 - コードの欠陥をTODO:やXXX:などの記法を使って示す  
 - 定数の値にまつわる「背景」  
#### 読み手の立場になって考える  
 - コードを読んだ人が「えっ!?」と思いそうな箇所を予想してコメントをつける  
 - 平均的な読み手が驚くような動作は文書化しておく  
 - ファイルやクラスには「全体像」のコメントを書く  
 - 読み手が細部に囚われないようにコードブロックにコメントをつけて概要をまとめる
 

### コメントのためのコメントをしない！
<font color="Red">X</font>  
```php
// 与えられた subtree に含まれる name と depth に合致した Node を見つける。 
Node* FindNodeInSubtree(Node* subtree, string name, int depth); 
```
※ これは「価値のないコメント」である(関数宣言と同じ)  
　ひどい名前の場合は、コメントではなく名前を変えよう！


### 自分の考えを記録する
〜 監督のコメンタリー 〜  
```
// このデータだとハッシュテーブルよりもバイナリツールの方が40%速かった
// 左右の比較よりもハッシュの計算コストの方が高いようだ
```
### コードの欠陥にコメントを付ける
```
// TODO: もっと高速なアルゴリズムを使う
// TODO: JPEG以外のフォーマットに対応する
```
その他↓


### 定数にコメントを付ける
```
NUM_THREADS = 8  # 値は「>= 2 * num_processors」で十分
```
→これなら値の決め方がわかる(1 だと小さすぎて、50 だと大きすぎる)。 

### ハマりそうな罠を告知する
```
// メールを送信する外部サービスを呼び出している(1分でタイムアウト) 
void SendEmail(string to, string subject, string body); 
```
→「実装の詳細」についてコメントを書くことで不幸を未然に防ぐ  
※この関数の実装では、外部のメールサービスに接続している。その接続には1秒以上かかり、このことを知らないウェブアプリケーション開発者が、HTTPリクエストの処理中に誤ってこの関数を呼び出してしまうかもしれない  
(メールサービスが ダウンしていると、ウェブアプリケーションが「ハング」してしまう) 
# <font color="Red">【 重要 】</font>ライターズブロックを乗り越えろ！
〜とりあえず書いてみよう(そこから詳細な言葉に置き換える)〜

**手順**  
① 頭の中にあるコメントをとにかく書き出す  
②コメントを読んで改善が必要なものを見つける  
③改善する

## 6章：コメントは正確で解決に  
〜小さな領域にできるだけ多くの情報を詰め込んだコメントを書く〜  

****まとめ****
 - 複数のものを指す可能性がある代名詞(それ,これ)を避ける  
 - 関数の動作はできるだけ正確に説明する  
 - コメントに含める入出力の実例を慎重に選ぶ  
 - コードの意図は高レベルで記述する  
 - よくわからない引数には**インラインコメント**を使う  
 - 多くの意味が詰め込まれた言葉や表現を使って、コメントを簡潔に保つ
 
### コメントを簡潔に！
```
// intはCategoryType。                         
// pairの最初のfloatは’score’。    
// 2つ目は’weight’
```
↓もっと簡潔にできる!
```
//CategoryType -> (score, weight)
```

### 曖昧な代名詞を避ける  
<font color="Red">X</font>  
```
//データをキャッシュに入れる。ただし、先にそのサイズをチェックする
```
→ ん？「その」ってどれのこと？データorキャッシュ？

<font color="Red">◯</font>
```
//データをキャッシュに入れる。ただし、先にデータのサイズをチェックする

//データが十分に小さければ、それをキャッシュに入れる
```

### 歯切れのイイ文章にする
<font color="Red">X</font>
```
#これまでにクロールした URL かどうかによって優先度を変える。 
```
<font color="Red">◯</font>
```
#これまでにクロールしていない URL の優先度を高くする。 
```
→より単純で、短くて、直接的  
「クロールしていないURLの優先度が高い」という情報も含まれている

### 関数の動作を正確に記述する
<font color="Red">X</font>
```
// このファイルに含まれる行数を返す。 
int CountLines(string filename) { ... } 
```
「行」にはさまざまな意味があるため正確ではない！  
　┗ ””(空のファイル)は、0行or1行?  
　　 ”hello”は、0行or1行?  
　　 “hello\n”は、1行or2行?  
　　 “hello\n world”は、1行or2行?  
　　 “hello\n\r cruel\n world\r”は、2行or3行or4行?  

<font color="Red">◯</font>
```
// このファイルに含まれる改行文字(‘\n’)を返す。 
int CountLines(string filename) { ... }
```
※「改行がない時、0を返す」と「キャリッジリターン(\r)が無視される」が伝わる

### 入出力のコーナーケースに実例を使う
〜慎重に選んだ入出力の実例をコメントに書いておけば、それは千の言葉に等しい〜
<font color="Red">X</font>
```
// 'src' の先頭や末尾にある 'chars' を除去する。 
String Strip(String src, String chars) { ... } 
```
→あまり正確ではない  
┗ chars は、除去する文字列なのか、順序のない文字集合なのか？  
　 src の末尾に複数の chars があったらどうなるのか？  

<font color="Red">◯</font>
```
// 実例: Strip(“abba/a/ba”, ”ab”)は”/a/”を返す　 
String Strip(String src, String chars) { ... } 
```

### コードの意図を書く
〜コメントとコードとの矛盾や冗長検査の役割を担う〜  
<font color="Red">X</font>
```php
// listを逆順にイテレートする
for (list<Product>::reverse_iterator it = products.rbegin(); it != products.rend(); 
++it) 
DisplayPrice(it->price); 
...
```
<font color="Red">◯</font>
```php
// 値段の高い順に表示する
for (list<Product>::reverse_iterator it = products.rbegin(); it != products.rend(); 
++it) 
DisplayPrice(it->price); 
...
```
→プログラムの動作を高いレベルから説明している


### 「名前付き引数」コメント
<font color="Red">X</font>
```
Connect(10, false); 
```
┗ 数値とブール値が渡されているけどコメントがないので、なんだかよくわからない

<font color="Red">◯</font>
```
// 引数にコメントをつけて関数を呼び出す
Connect(/* timeout_ms = */ 10, /* use_encryption = */ false);
``` 
→インラインコメントを使って、関数を呼び出す  
　┗本来は仮引数の名前を timeout_ms に変更すべきだがもし変更できないのであれば  
　このようにして名前を「改善」できる  
【重要】ブール型の引数では、値の前に /* name = */ を置く

### 情報密度の高い言葉を使う
〜繰り返し登場する問題や解決策を”パターンやイディオムを説明するための言葉”を使うことでコメントを簡潔にする〜  
例①
```
// このクラスには大量のメンバがある。同じ情報はデータベースにも保管されている。ただし、
// 速度の面からここにも保管しておく。このクラスを読み込むときには、メンバが存在してい 
// るかどうかを先に確認する。もし存在していれば、そのまま返す。存在しなければ、データベー
// スから読み込んで、次回のためにデータをフィールドに保管する。 
```
⬇︎  
```
// このクラスの役割は、データベースのキャッシ層である。
```

例②)  
```
// 所在地から余分な空白を除去する。それから「Avenue」を「Ave.」にするなどの整形を施す。 
// こうすれば、表記がわずかに違う所在地でも同じものであると判別できる
```
⬇︎
```
// 所在地を正規化する (例: “Avenue” -> “Ave.”)。
```
