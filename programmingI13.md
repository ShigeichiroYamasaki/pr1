■■　　授業資料URL
https://drive.google.com/drive/folders/0Bwts5UTHjM9EUS14V0w0OEMyUzQ?hl=ja

第12回：　分岐制御　変数と定数


## 分岐制御

* 複数の条件による分岐制御

### if then elsif ... end

* 条件文を繰り返す
* 2分木：条件文のtrue/false で２つに分かれる木


### case when

* 複数の条件で分岐する



■課題の回答案

def osusume(movies,eiga_v,index)
  e0=eiga_v[index]
  return eiga_v.map.with_index{|e,i|[tanimoto(e0,e),movies[i]]}.sort[-5..-1]
end

p osusume(movies,eiga_v,2)

■適当な文字列を「評価」してみる

abc

■ローカル変数
●#{   } は「評価」するという意味

def hello(name)
   "こんにちは#{name}さん"
end

 p hello("新垣結衣")

●メソッドの中は独立した変数の世界

def hello(name)
   "こんにちは#{name}さん"
end

def aisatu(name)
   "ごきげんよう#{name}さん"
end

●ローカル変数は外側の変数に影響しない

name = "竹内涼真"
p hello(name)
p aisatu("新垣結衣")
p name

●ブロック変数

(1..3).each{|i| puts(i)}

●ブロック変数とローカル変数の衝突

i=5000
(1..3).each{|i| puts(i)}
p i

●ブロック内で計算するための変数

(1..3).each{|i| s=s+i}

●ブロック内でのローカル変数の利用

s=0
(1..3).each{|i| s=s+i}
p s

●1からnまでの和の計算

n=10
s=0
(1..n).each{|i| s=s+i}
p s

●1からnまでの和を計算するメソッド

def goukei(n)
  s=0
  (1..n).each{|i| s=s+i}
  return s
end

p goukei(8)

●メソッド内のローカル変数は外側の変数辞書を書き換えない

s=10000

def goukei(n)
  s=0
  (1..n).each{|i| s=s+i}
  return s
end

p goukei(8)
p s

●メソッドとブロックの変数環境の構造の違い

n=10000

def goukei(n)
  s=0
  (1..n).each{|i| s=s+i}
  return s
end

p n

●グローバル変数はメソッド内でもブロック内でも書き換えられる

$s=10000

def goukei(n)
  $s=0
  (1..n).each{|i| $s=$s+i}
  return $s
end

p goukei(8)
p $s

●グローバル変数は危険

def ikemen()
   "#{$name}さんイケメン"
end

def kawaii()
   "#{$name}さんかわいい"
end

$name="竹内涼真"
kawaii()
$name="新垣結衣"
ikemen()

●定数の適切な使い方

# 円周率
Pi=3.14
# 消費税
TaxRate=0.08

# 円の面積
def en(r)
   return Pi*r**2
end

# 税込み価格
def zeikomi(zeinuki)
   return zeinuki*(1.0+TaxRate)
end

p en(10)
p zeikomi(1000)

●代入と評価の発展的な話題

x="(2+3)*10"
y="x"
# 変数yを評価する
p y
# 変数yを評価した結果をさらに評価する
p eval(y)
# 変数yを評価結果の評価結果を評価する
p eval(eval(y))

●代入と評価の発展的な話題

a=[1,2]
# pushメソッドは配列aに最後の要素を追加する
a.push(3)
p a

# pushメソッドで自分自身を追加したら
a.push(a)
p a
p a[3]


■課題
下のデータは、性別と体重の配列です。
性別ごとの体重の平均値を計算し、その結果を男と女の配列として出力するメソッド taiju を作成してください.

data=[["女", 30], ["女", 45], ["女", 68], ["女", 47], ["女", 56], ["男", 48], ["男", 31], ["女", 45], ["女", 32], ["男", 35], ["男", 54], ["男", 46], ["女", 54], ["女", 72], ["女", 41], ["男", 40], ["男", 77], ["女", 36], ["男", 55], ["男", 52]]

# 処理例
p taiju(data)
# => [48.666666666666664, 47.81818181818182]

# また、以下のプログラムによって生成されるデータでも実行してください

data=(1..100).map{|x|[['男','女'][rand(2)],rand(50)+35]}



■■　　授業資料URL
https://drive.google.com/drive/folders/0Bwts5UTHjM9EUS14V0w0OEMyUzQ?hl=ja

第13回：ハッシュ

■課題の回答案

data=[["女", 30], ["女", 45], ["女", 68], ["女", 47], ["女", 56], ["男", 48], ["男", 31], ["女", 45], ["女", 32], ["男", 35], ["男", 54], ["男", 46], ["女", 54], ["女", 72], ["女", 41], ["男", 40], ["男", 77], ["女", 36], ["男", 55], ["男", 52]]


def taiju(data)
  sum_of_men=0
  sum_of_women=0
  num_of_men=0
  num_of_women=0
  data.each do |d|
    if d[0]=="男" then
      sum_of_men=sum_of_men+d[1]
      num_of_men=num_of_men+1
    else
      sum_of_women=sum_of_women+d[1]
      num_of_women=num_of_women+1
    end
  end
  return [sum_of_men.to_f/num_of_men, sum_of_men.to_f/num_of_men]
end

処理例
p taiju(data)
=> [48.666666666666664, 47.81818181818182]

また、以下のプログラムによって生成されるデータでも実行してください
data=(1..100).map{|x|[['男','女'][rand(2)],rand(50)+35]}


■ハッシュの例

h={"年齢"=>60,:性別=>"男", 0=>[1,2,3]}
p h


■ハッシュの値取り出しの例

h={"年齢"=>60,:性別=>"男", 0=>[1,2,3]}
p h["年齢"]
p h[:性別]
p h[0]

■ハッシュの作成方法

h={}
# キーと値の登録
h["年齢"]=60
h[:名前]="山崎"
# ハッシュオブジェクトの確認
p h

■未定義のキーの返り値

h={}
h["年齢"]=60
h[:名前]="山崎"
# 未定義のキーでアクセス
p h[:abcd]

■シンボルによるハッシュの作成方法

h={}
h[:名前]="山崎"
h[:年齢]=60
p h

■シンボルをキーにしたハッシュの簡略表現

h={名前: "山崎", 年齢: 60}
# Ruby言語の内部では => 表記になっている
p h

■ハッシュに対するメソッド

h={"名前"=>"山崎", "年齢"=>60}
p h.keys

■ハッシュに対するメソッド

h={"名前"=>"山崎", "年齢"=>60}
p h.values

■ハッシュに対するメソッド

h={"名前"=>"山崎", "年齢"=>60}
p h.key?("名前")
p h.key?("住所")

■ハッシュに対するメソッド

h={"名前"=>"山崎", "年齢"=>60}
h.each{|k,v| p k}
h.each{|k,v| p v}

■ハッシュに対するメソッド

h={"名前"=>"山崎", "年齢"=>60}
p h.map{|k,v| [k,v]}

■ハッシュで表をつくる

movies={}   # 最初に空のハッシュを作成する
movies[:君の名は]=  {高橋: 1,藤尾: 0, 寺井: 0, 羽太: 1}
movies[:シンゴジラ]={高橋: 1,藤尾: 1, 寺井: 0, 羽太: 0}
movies[:ジョーズ]=  {高橋: 1,藤尾: 0, 寺井: 0, 羽太: 1}
movies[:ピンポン]=  {高橋: 0,藤尾: 1, 寺井: 1, 羽太: 1}

p movies

■ハッシュの表を参照する

#加えて
p movies[:シンゴジラ]
p movies[:シンゴジラ][:羽太]

■ハッシュの表を参照する
#加えて
p movies[:君の名は]
p movies[:君の名は][:高橋]

■ハッシュの表の内容で計算する
#加えて
s=0
movies[:シンゴジラ].each{|k,v|s=s+v}
p s

■ハッシュの表の例２

t={}
t[:日本]={}
t[:ポーランド]={}
t[:セネガル]={}
t[:コロンビア]={}
t[:日本][:ポーランド]=[0,1]
t[:日本][:セネガル]=[2,2]
t[:日本][:コロンビア]=[2,1]
t[:ポーランド][:セネガル]=[1,2]
t[:ポーランド][:コロンビア]=[0,3]
t[:セネガル][:コロンビア]=[0,1]

■ハッシュの表の例２

# 上に加えて

p t[:日本][:ポーランド]

def kachiten(c )
    point=0
    t[c].each do |k,v|
                    if v[0] > v[1] then point=point+3
                    elsif v[0]==v[1] then point=point+1
                    end
                  end
    return point
end


■ハッシュを使った木構造

tree={a: {c: 1, d: 2}, b: {e: 3}}
p tree[:a][:d]   # 葉にアクセス

p tree[:b] 

■課題

次の表の完成形をハッシュで表現してください
各国の勝ち点を計算してください
勝ち点：勝利=3点、引き分け=1点、敗戦=0点

