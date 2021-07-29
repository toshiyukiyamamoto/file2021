## 1章：理解しやすいコード
読みやすさの基本定理
〜コードは他の人が最短時間で理解できるように書かなければならない〜
・理解するまでにかかる時間を短縮する
　┗「理解する」：変更を加えたりバグを見つけることができる
　　　　　　　　　他のコードと連携する方法の理解
・遠い未来の自分が見た時にわかるように
・プロジェクトに途中参加したメンバーがわかるように
〜でもやるんだよ〜
優秀なプログラマを目指して、バグの少ないコードを作り出そう

## 2章：名前に情報を詰め込む
### 2.1 明確な単語を選ぶ
例「get」
```
❌  
//インターネットからページを取得
def GetPage(url) :                            
…….　　　　  　 
→どこからページを取ってくるの？ローカルキャッシュ？データベース？
⭕️
//インターネットからページを取得  
def FetchPage(url) :  //もしくはDownloadPage                          
…….　　　　     
```
 ※「 explode()とsplit() 」
→explode()は”何かを分割する”を伝えれるが、split()との違いは名前からはわからない
2つの関数違い：区切り文字に正規表現を使えるか／使えないか
https://ameblo.jp/gonta3333/entry-10384282091.html
### 2.2 汎用的な名前を避ける
〜エンティティの値や目的を表した名前で選ぶ〜
```
var euclidean_norm = function (v) {
      var retval = 0.0;
      for (var i = 0; i < v.length; i += 1) 
            retval += v[i] * v[i]; 
      return Math.sqrt(retval); 
}; 
⬇︎変数の目的や値を表すものがイイ(“vの２乗の合計”を表現する)
var euclidean_norm = function (v) {
      var sum_squares = 0.0;
      for (var i = 0; i < v.length; i += 1) 
            sum_squares+= v[i] * v[i]; 
      return Math.sqrt(retval); 
}; 
```
※これならバグも見つけやすい！
sum_squares += v[i]; 　// 合計する「square(2乗)」がない。バグだ! 

But 汎用的な名前も使う場面はある
```
tmp(情報の一時的な保管)
⭕️
if (right < left) { 
    tmp = right;  
    right = left; 
    left = tmp; 
} 
※このような場合は、tmp という名前で「この変数 には他に役割がない」という明確な意味を伝えている。(生存期間は数行のみ)
❌
String tmp = user.name();
tmp += " " + user.phone_number(); tmp += " " + user.email();
...
template.set("user_info", tmp); 
```
※この変数にとって大切なことは「一時的な保管」ではない。
　わかりやすくするには、user_info のような名前に！


ループとイテレータ( i・j・k・iter )
〜でも、これよりもイイ名前がある！〜
例.クラブ所属のユーザを調べるループ
```
❌
for (int i = 0; i < clubs.size(); i++)
      for (int j = 0; j < clubs[i].members.size(); j++) 
            for (int k = 0; k < users.size(); k++) 
                  if (clubs[i].members[k] == users[j]) ⬅︎バグ
                      cout << "user[" << j << "] is in club[" << i << "]" << endl;
※if文のmembers[]とusers[]のインデックスが逆になっとる
⬇︎イテレータが複数ある時は、もっと明確な名前をつける！
if (clubs[ci].members[ui] == users[mi])  #バグだ!最初の文字が違う
⬇︎
⭕️
if (clubs[ci].members[mi] == users[ui])
```

### 2.3 具体的な名前を使う
┗「ServerCanStart」を「CanListenPort」に
         〜抽象的〜                 〜具体的〜
※任意のTCP/IPポートをサーバがリッスンできるか確認するメソッド

例. DISALLOW_EVIL_CONSTRUCTORS
 (メモリリワークなどの問題につながる”悪”のコンストラクタを許可しない規約)
マクロの定義
```
#define DISALLOW_EVIL_CONSTRUCTORS(ClassName) \ 
      ClassName(const ClassName&); \
      void operator=(const ClassName&); 
   
class ClassName { 
   private: 
      DISALLOW_EVIL_CONSTRUCTORS(ClassName); 
   public: ... 
}; 
```
※ 「EVIL(悪の)」 という言葉よりも、このマクロが「許可していないもの」を明確にするほうが　　　大切(実際には operator=() メ ソッドも許可していない)
　　　　↓あまり刺激的ではなく、より具体的な名前に変更
```
#define DISALLOW_COPY_AND_ASSIGN(ClassName) ... 
```
### 2.4 名前に情報を追加する
〜名前は短いコメントのようなものだ！〜
┗16進数の文字列を持つ変数だったら？→「hex_id」とする (IDフォーマット優先)
値の単位
時間やバイト数のように計算できるものがあれば、変数名に単位を入れる
例) 
❌
var start = (new Date()).getTime(); // ぺージの上部
...
var elapsed = (new Date()).getTime() - start; // ページの下部 
document.writeln(" 読み込み時間:" + elapsed + " 秒 "); 
※getTimeが秒ではなくミリ秒を返すため、このままだとうまく動かない💦
⬇︎変数名に「 _ms 」を追加して、コードを修正
⭕️
var start_ms = (new Date()).getTime(); // ページの上部
...
var elapsed_ms = (new Date()).getTime() - start; // ページの下部 
document.writeln(" 読み込み時間:" + elapsed_ms / 1000 + " 秒 ");

その他↓




その他の重要な属性を追加する

 →セキュリティのバグのような深刻な被害が出るところに使おう！

※ハンガリアン記法は、使われなくなっている
( 変数名の最初や最後に目印（接頭辞・接尾辞）を付けることで、変数の意味を掴みやすくして間違いを減らす表記方法 )
https://www.agent-grow.com/self20percent/2017/12/13/thinking-about-hungarian-notation/
https://wa3.i-3-i.info/word13959.html

### 2.5 名前の長さを決める
〜でも短ければ良いわけではない(　ﾟдﾟ)〜
スコープが小さければ短い名前でもOK
if (debug) { 
    map<string,int> m; 
    LookUpNamesNumbers(&m); 
    Print(m); 
} 
※コードを理解するための情報(変数の型・初期値・破棄方法)が近くにあるので、
　mでも大丈夫

頭文字と省略形
⭕️
evaluation→eval
document→doc
string　　→str
❌
BackEndManager→BEManager
ん？知らない💦暗号？？

不要な単語を捨てる
┗ ConvertToString()→ToString()
     DoServeLoop()    →ServeLoop()




### 2.6 名前のフォーマットで情報を伝える
クラス名：CamelCase (キャメルケース)
変数名　：lower_separated (小文字をアンダースコアで区切る)
など..

その他のフォーマット規約↓
『JavaScript: The Good Parts』(Douglas Crockford, O'Reilly, 2008)

まとめ










## 3章：誤解されやすい名前
〜「他の意味と間違えられることはないか？」と自問自答する〜

例① filter()
results = Database.all_objects.filter("year <= 2011")
→filterは「選択する」or「除外する」のどちらかわからない💦
　　　　↓
「選択する」：select()
「除外する」：exclude()

例② Clip(text, length)
❌
textの最後を切り落として、「...」をつける 
def Clip(text, length):
... 
┗「最後からlength文字を削除する(remove)」と
　「最大length文字まで切り詰める(truncate)」のどっち？💦
⭕️
def Truncate(text, max_chars):
…　　 
┗ 1.関数名をTruncate(text, length)に変更
　 2. length を明確にする（今回は「文字列」を意味しているのでmax_chars）

### 3.3 限界値を含めるときはminとmaxを使う
❌
CART_TOO_BIG_LIMIT = 10
if shopping_cart.num_items() > CART_TOO_BIG_LIMIT:
    Error(" カートにある商品数が多すぎます。")  
┗「未満(限界値を含まない)」
　「以上(限界値を含む)」　のどちらかわからない💦
⭕️
MAX_ITEMS_IN_CART= 10
if shopping_cart.num_items() > MAX_ITEMS_IN_CART:
    Error(" カートにある商品数が多すぎます。")
### 3.4 範囲を指定するときは first と last を使う
❌
print integer_range(start=2, stop=4)
┗これが示すのは、「2,3」or「2,3,4」のどっち？(あるいはその他？)
⭕️　　
set.PrintKeys(first=”Bart”, last=”Maggie”)
┗終端を範囲に含めるのなら、firstとlastを使うべし！


### 3.5 包含 / 排他的範囲にはbeginとendを使う

例. 10月16日に開催されたイベントを全て印字したい
PrintEventsInRange("OCT 16 12:00am", "OCT 17 12:00am") 
                                    〜begin〜                 〜 end 〜

### 3.6 ブール値の名前
・ブール値の変数やブール値を返す関数の名前を選ぶときは
　trueとfalseの意味を明確にしなければならない！
❌
bool read_password = true;
┗「パスワードをこれから読み取る必要がある」
　「パスワードをすでに読み取っている」　　　のどちらなのか不明💦
⭕️
bool need_password = true;   
もしくは
bool user_is_authenticated = true;
・ブール値の変数名は、頭に is・has・can・should などをつけてわかりやすくする
・名前を肯定系にしたほうが短くて、声に出して読みいやすい！

### 3.7 ユーザの期待に合わせる
例. get*()　〜getで始まるメソッドは「軽量アクセサ」であるという規約〜
　public double getMean() { 
         // 全てのサンプルをイテレートして、total / num_samplesを返す。
　}  
   ... 
} 
もしget*()の規約を知らない場合は、コストが高いと知らずに呼び出してしまうかもしれない
→コストの高さが事前にわかるように computeMean() などの名前に変えるべき
　(もしくは、コストの高くない実装に変えるべき） 

3.8 複数の名前を検討する
例)webサイトの実験用設定ファイル

　　↓既存の設定ファイルを他の実験でも使えるように...
experiment_id: 101
the_other_experiment_id_I_want_to_reuse:100
[以下、変更が必要な情報だけ書き換える]
　　↓では「the_other_experiment_id_I_want_to_reuse」の名前はどうするか？
4つから選ぶ
┗1.template
   2.reuse
   3.copy
   4.inherit



Copy でいこう！

experiment_id: 101 
copy: 100 
... 
しかし、copy: 100だけでは、
「この実験を100回コピーする」 or「これは100回目のコピーだ」
のどちらかわからない
→他の実験を参照してい る言葉だということを明確にするには、copy_experiment という
　名前に変えるとイイ


## 4章：美しさ
①適切な改行
②複数のコードブロックで同じようなことをしていたら、シルエットも同じようにする
③コードの「列」を整理すれば、概要が把握しやすくなる
④ある場所でA・B・Cのように並んでいたものを、他の場所でB・C・Aのように並べては　いけない！意味のある順番を選んで、常にその順番を守る
⑤空行を使って大きなブロックを論理的な「段落」に分ける

### 4.2 一貫性のある簡潔な改行位置とクラス

※適切な改行を入れ、繰り返されたコメントは簡潔にする(仮引数を一行で書く)

### 4.3 メソッドを使った整列
〜ヘルパーメソッドを使ってみる〜
❌
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
⬇︎
⭕️
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
※これによって良い副産物が得られる
・重複を排除したことでコードが簡潔に！
・テストケースの大切な部分(名前やエラー文字列)が見やすくなった
・テストの追加が簡単になった




### 4.4 縦の線を真っ直ぐにする
例
❌
CheckFullName("Doug Adams", "Mr. Douglas Adams", ""); 
CheckFullName(" Jake Brown ", "Mr. Jacob Brown III", ""); 
CheckFullName("No Such Guy", "", "no match found"); 
CheckFullName("John", "", "more than one result"); 

⭕️
CheckFullName("Doug Adams", "Mr. Douglas Adams", ""); 
CheckFullName(" Jake Brown ", "Mr. Jacob Brown III", ""); 
CheckFullName("No Such Guy", ""                            , "no match found"); 
CheckFullName("John"            , ""                            , "more than one result"); 
※縦の線を揃えることで流し読みが楽にできる(「似ているコードは似ているように見せる」)


### 4.5 一貫性と意味のある並び
コードの並びがコードの正しさに影響を及ぼすことは少ない
ただし....
できれば意味のある順番に並べる！
・対応するHTMLフォームの<input>フィールドと同じ並び順にする
・「最重要」なものから重要度順に！
・アルファベット順に並べる


### 4.6 宣言をブロックにまとめる











### 4.7 コードを「段落」に分割する
┗・似ている考えをグループにまとめて、他の考えと分けるため
　・視覚的な「踏み石」を提供できる
　・段落単位で移動できるようになる

例)


















## 5章：コメントすべきことを知る
〜コメントの目的は、書き手の意図を読み手に知らせることである〜


 

### コメントのためのコメントをしない！
例)
❌
// 与えられた subtree に含まれる name と depth に合致した Node を見つける。 
Node* FindNodeInSubtree(Node* subtree, string name, int depth); 
※これは「価値のないコメント」である(関数宣言と同じ)
　ひどい名前の場合は、コメントではなく名前を変えよう！






### 5.2 自分の考えを記録する
〜 監督のコメンタリー 〜
例)
// このデータだとハッシュテーブルよりもバイナリツールの方が40%速かった
// 左右の比較よりもハッシュの計算コストの方が高いようだ

コードの欠陥にコメントを付ける
例)
// TODO: もっと高速なアルゴリズムを使う
// TODO: JPEG以外のフォーマットに対応する

その他↓


### 定数にコメントを付ける
例)
NUM_THREADS = 8  # 値は「>= 2 * num_processors」で十分
→これなら値の決め方がわかる(1 だと小さすぎて、50 だと大きすぎる)。 

### ハマりそうな罠を告知する
例)
// メールを送信する外部サービスを呼び出している(1分でタイムアウト) 
void SendEmail(string to, string subject, string body); 
→「実装の詳細」についてコメントを書くことで不幸を未然に防ぐ
※この関数の実装では、外部のメールサービスに接続している。その接続には 1 秒 以上かかり、　このことを知らないウェブアプリケーション開発者が、HTTPリクエストの処理中に誤ってこの関数を呼び出してしまうかもしれない
(メールサービスが ダウンしていると、ウェブアプリケーションが「ハング」してしまう) 
# 　【 重要 】ライターズブロックを乗り越える！　
〜とりあえず書いてみよう(そこから詳細な言葉に置き換える)〜

手順




## 6章：コメントは正確で解決に
〜小さな領域にできるだけ多くの情報を詰め込んだコメントを書く〜

 


### 6.1 コメントを簡潔に！
例)
// intはCategoryType。                          //CategoryType -> (score, weight)
// pairの最初のfloatは’score’。    ➡︎　
// 2つ目は’weight’




### 6.2 曖昧な代名詞を避ける
例)
❌
//データをキャッシュに入れる。ただし、先にそのサイズをチェックする
┗＞ ん？「その」ってどれのこと？　データorキャッシュ？

⭕️
//データをキャッシュに入れる。ただし、先にデータのサイズをチェックする
もしくは...
//データが十分に小さければ、それをキャッシュに入れる


### 6.3 歯切れのイイ文章にする
例)
❌
#これまでにクロールした URL かどうかによって優先度を変える。 

⭕️
#これまでにクロールしていない URL の優先度を高くする。 
┗＞ より単純で、短くて、直接的
       「クロールしていないURLの優先度が高い」という情報も含まれている

### 6.4 関数の動作を正確に記述する
例)
❌
// このファイルに含まれる行数を返す。 
int CountLines(string filename) { ... } 
→「行」にはさまざまな意味があるため正確ではない！
　┗ ””(空のファイル)は、0行or1行?
　　 ”hello”は、0行or1行?
　　 “hello\n”は、1行or2行?
       “hello\n world”は、1行or2行?
       “hello\n\r cruel\n world\r”は、2行or3行or4行?
⭕️
// このファイルに含まれる改行文字(‘\n’)を返す。 
int CountLines(string filename) { ... }
※「改行がない時、0を返す」と
　「キャリッジリターン(\r)が無視される」が伝わる

### 6.5 入出力のコーナーケースに実例を使う
〜慎重に選んだ入出力の実例をコメントに書いておけば、それは千の言葉に等しい〜
例)
❌
// 'src' の先頭や末尾にある 'chars' を除去する。 
String Strip(String src, String chars) { ... } 
→あまり正確ではない
┗ chars は、除去する文字列なのか、順序のない文字集合なのか？
　 src の末尾に複数の chars があったらどうなるのか？

⭕️
// 実例: Strip(“abba/a/ba”, ”ab”)は”/a/”を返す　 
String Strip(String src, String chars) { ... } 


### 6.6 コードの意図を書く
〜コメントとコードとの矛盾や冗長検査の役割を担う〜
例)
❌
// listを逆順にイテレートする
for (list<Product>::reverse_iterator it = products.rbegin(); it != products.rend(); 
++it) 
DisplayPrice(it->price); 
...


⭕️
// 値段の高い順に表示する
for (list<Product>::reverse_iterator it = products.rbegin(); it != products.rend(); 
++it) 
DisplayPrice(it->price); 
...
→プログラムの動作を高いレベルから説明している


### 6.7 「名前付き引数」コメント
例)
❌
Connect(10, false); 
┗ 数値とブール値が渡されているけど、コメントがないので、なんだかよくわからない

⭕️
// 引数にコメントをつけて関数を呼び出す
Connect(/* timeout_ms = */ 10, /* use_encryption = */ false); 
→インラインコメントを使って、関数を呼び出す
　┗本来は仮引数の名前を timeout_ms に変更すべきだがもし変更できないのであれば
　　このようにして名前を「改善」できる
【重要】ブール型の引数では、値の前に /* name = */ を置く











### 6.8 情報密度の高い言葉を使う
〜繰り返し登場する問題や解決策を”パターンやイディオムを説明するための言葉”を
　使うことでコメントを簡潔にする〜
例①)
// このクラスには大量のメンバがある。同じ情報はデータベースにも保管されている。ただし、
// 速度の面からここにも保管しておく。このクラスを読み込むときには、メンバが存在してい 
// るかどうかを先に確認する。もし存在していれば、そのまま返す。存在しなければ、データベー
// スから読み込んで、次回のためにデータをフィールドに保管する。 
　　　　⬇︎
// このクラスの役割は、データベースのキャッシ層である。


例②)
// 所在地から余分な空白を除去する。それから「Avenue」を「Ave.」にするなどの整形を施す。 
// こうすれば、表記がわずかに違う所在地でも同じものであると判別できる
　　　  ⬇︎
// 所在地を正規化する (例: “Avenue” -> “Ave.”)。

















Ⅱ部. ループとロジックの単純化

### if/else ブロックの並び順


### 三項演算子
〜行数を短くするよりも、他人が理解するのにかかる時間を短くする〜
❌ 
return exponent >= 0 ? mantissa * (1 << exponent) : mantissa / (1 << -exponent); 
⭕️ 
if (exponent >= 0) {
    return mantissa * (1 << exponent); 
} else {
    return mantissa / (1 << -exponent); 
}
※基本的には if/else文 を使う。三項演算子は簡潔になる時だけ！

### 7.4 do/whileループを避ける
〜コードブロックを再実行する条件が下にあるから、　わかりにくい！　〜
❌ 
do {　 
　　continue; 
} while (false); 
→ん？永久ループ？💦

### 7.5 関数から早く返す



