# プログラミングI 第13回

クラスとインスタンス

## 前回の課題

映画視聴履歴のCSVデータを利用

* CSV形式のファイルを csv ライブラリを使ってreadして、配列の配列に変換してください
* 数値部分を文字列から整数に変換してください
* 個人ごとの視聴履歴の配列を利用して
* 人と人とのtanimoto係数を、２段階ハッシュ表にしてください
* 最初の配列要素（映画名の一覧）は無視してください
* person_id というカラムを人のIDとして利用してください
(配列のインデックスを人のIDとして利用してください)

### 課題への方針

#### 修正前の課題の場合

* 配列のインデックスを人のIDにする方法の例
	* 各配列の最初の要素としてインデックスを入れる

```ruby
# テストデータ 4個の配列の配列
test=[[0,1,1,0,0,0],[0,0,1,0,1,0],[0,0,1,0,0,1],[0,1,1,0,1,1]]
```

これが以下のようにインデックス0に配列のインデックスが入るようにすればよい

```ruby
# テストデータ 4個の配列の配列
data=[[0,0,1,1,0,0,0],[1,0,0,1,0,1,0],[2,0,0,1,0,0,1],[3,0,1,1,0,1,1]]
```

* プログラムの例（for文を使った例）
	* Rangeを使ってインデックスをつくり配列に埋め込む


```ruby
data=[]
for i in (0..3) do
  data[i]=[i]+test[i]
end
p data
```

実行結果

```ruby
[[0, 0, 1, 1, 0, 0, 0], [1, 0, 0, 1, 0, 1, 0], [2, 0, 0, 1, 0, 0, 1], [3, 0, 1, 1, 0, 1, 1]]
```

### 修正版の課題へのアプローチ

* CSVファイルを読み込む
* 映画名など余分な要素を取り除く
* 数値の文字列を整数に変換する
* 人に関するtanimoto係数の表を２段ハッシュとして作成する


```ruby
require 'csv'
d=CSV.read('File3','r')
d2=d[1..-1]
# インデックス0が人のIDの整数の配列の配列をdataにする
data=d2.map do |x|
        x.map do |y|
            if /\d+/=~y then	 # 数値の文字列の場合
                y.to_i         # 文字列を整数に変換
            else
                y
            end
        end
    end
# tanimoto係数メソッド
def tanimoto(x,y)
	nxy=x.zip(y).reduce(0.0){|s,p|s+(p[0]*p[1])}
	return nxy/(x.sum+y.sum-nxy)
end
# ２段階ハッシュ表の作成メソッド
def tanimoto_table(data)
	table={}
	data.each do |x|
		table[x[0]]={}
		data.each do |y|
			table[x[0]][y[0]]=tanimoto(x[1..-1],y[1..-1])
		end
	end
	return table
end
p tanimoto_table(data)
```

## クラスの例

```ruby
p "あいうえお".class
p 123.class
p [1,2,3,4].class
```

## newメソッド

```ruby
# Array クラスから新しい配列のインスタンスを生成
p Array.new

# Hashクラスから、新しいハッシュのインスタンスを生成
p Hash.new

# Stringクラスから新しい文字列を生成
p String.new

```

## 自作のクラスのインスタンスを生成する

```ruby
# 猫クラスの定義
class Cat
end
# Catクラスのインスタンスを生成する
p Cat.new
```

## インスタンス(オブジェクト）に名前をつける

```ruby
# 猫クラスの定義
class Cat
end

# 猫（タマ）のインスタンスを作成する
tama=Cat.new
# 猫（ミケ）のインスタンスを作成する
mike=Cat.new
```

## インスタンスメソッドの実行

```ruby
# 猫クラスの定義
class Cat
  def naderu       # インスタンスメソッド
    return "にゃあ"
  end
end

tama=Cat.new          # インスタンスの生成
puts tama.naderu      # インスタンスメソッドの実行

```

## インスタンス変数による状態の表現

```ruby
class Omikuji
  def initialize
    @kuji=["大吉","吉","中吉","凶","大凶"]
  end
  def try
	return @kuji.pop 
  end
end

omikuji=Omikuji.new
puts omikuji.try
puts omikuji.try
puts omikuji.try
puts omikuji.try
puts omikuji.try
```

## くじの出方をランダムにする方法

```ruby
class Omikuji
  def initialize
    @kuji=["大吉","吉","中吉","凶","大凶"].shuffle
  end
  def try
	return @kuji.pop 
  end
end

omikuji=Omikuji.new
puts omikuji.try
puts omikuji.try
puts omikuji.try
puts omikuji.try
puts omikuji.try
```

## 配列の掛け算と足し算について

p メソッドを利用するには、曖昧性を無くすために( ) をつけてあげる必要がある
```ruby
p (["大吉"]*3)
p (["大吉"]*3 + ["吉"]*4)
```

## メソッドの() の省略ができない場合

```ruby
p([1,2,3]*3)
p [1,2,3]*3   # エラーになる
```

## くじの種類ごとの個数を変える例

```ruby
class Omikuji
  def initialize
    kuji=(["大吉"]+["吉"]*4+["中吉"]*6+["凶"]*4+["大凶"])
    @kuji=kuji.shuffle
  end
  def try
	return @kuji.pop 
  end
end

```

## newメソッドの引数でインスタンスを初期化

```ruby
class Cat
  def initialize(sex)
    @sex=sex              # インスタンス変数の初期化
  end
  def naderu
	if @sex=="オス" then
    	return "ぎゃあ"    # オスの場合の反応
	else
		return "にゃあ"    # メスの場合の反応
	end
  end
end

tama = Cat.new("オス")
mike = Cat.new("メス")

p tama.naderu
p mike.naderu
```

## ユーザのクラスとインスタンスの例

```ruby
class User   # Userクラスの定義
   def initialize(mail, password)
     @mail=mail               # メールアドレス設定
     @password=password       # パスワード設定
   end

   def show_pw                # パスワード確認メソッド
     return @password
   end

   def change_pw(password)    # パスワードの変更メソッド
     @password=password
   end
end


u1=User.new('yamasaki@fuk.kindai.ac.jp','himitu111')
# パスワードを参照する
puts u1.show_pw
# パスワードを変更する
u1.change_pw('naisyo000')
# 再びパスワードを参照する
puts u1.show_pw

```

## 課題

次のような Omikuji クラス（おみくじ）を作成してください

* newメソッドの引数で種類ごとのくじの数を指定できるようにする

例：　Omikuji.new(10,40,60,40,10) とすると
	大吉 10個、吉 40個、中吉 60個、凶 ４0個、大凶 10個

* くじの出方はランダムになるようにしてください
* 実際に実験をしてみてください
* おみくじの"大吉","吉","中吉","凶","大凶"の比率を 1:4:6:4:1
* おみくじの全個数を16000枚に設定
* 100回程度の実験でくじの出現頻度を調べてみてください

