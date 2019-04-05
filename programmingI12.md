■■　　授業資料URL
https://drive.google.com/drive/folders/0Bwts5UTHjM9EUS14V0w0OEMyUzQ?hl=ja

第12回：変数と定数

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


