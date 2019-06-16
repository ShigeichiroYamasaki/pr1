# プログラミングI 第10回
エラーとデバッグ

## 前回の課題

松岡修造のメッセージの細かい文字列の断片の配列 sentence2 を利用して
ランダムでできるだけ自然な内容をにつぶやく shuzo メソッドを作成してください

* 自分でselectメソッドやrejectメソッドを使って、文の生成に適したパターンを見つけてください
* 生成するメッセージの構成順序を考えて、より自然な文章にしてください

###  前回の課題への基本的アプローチ

* 松岡修造のメッセージからパターンを見つける
* 松岡修造のメッセージの断片をパターンごとに集める
* 例
	2. 〜よね|のか？
	3. 見てみろよ。
	2. でも〜
	3. 噴水｜サバ｜太陽｜脳｜松茸|雪だるま|紅葉|温泉|ゾウ|キホン
	4. みろ！／だよ。
	4. 大丈夫、|大切なんだ思うんだ。|応援する！|信じているんだ。
	
* パターンの要素をランダムに選んで、メッセージを構成する

```ruby
# 松岡修造の全メッセージの配列を一つの文字列に結合
all_sentences=message.join
# 改行記号(\n)で文字列を１行ごとの配列に分解する
sentences2=all_sentences.split("\n")

def shuzo(ss)
	yonenoka=ss.select{|x|x=~/よね。|のか？/}.shuffle[0]
	miroyo=ss.select{|x|x=~/見てみろよ。/}.shuffle[0]
	demo=ss.select{|x|x=~/でも、/}.shuffle[0]
	tatoe=ss.select do |x|
		x=~/噴水｜サバ｜太陽｜脳｜松茸|雪だるま|紅葉|温泉|ゾウ|キホン/
	end.shuffle[0..2]
	mirodayo=ss.select{|x|x=~/みろ！|だよ。/}.shuffle[0]
	nanda=ss.select{|x|x=~/大丈夫、|大切なんだ思うんだ。|応援する！|信じているんだ。/}.shuffle[0]
	return [yonenoka, miroyo ,demo,tatoe, mirodayo, nanda].join("\n")
end
puts shuzo( sentences2)
```

## エラーとデバッグ

### 基本的なエラー

基本的エラーについて意味を知っておきましょう。

|エラーのタイプ|意味|
|:--|:--|
| NameError |未定義のローカル変数や定数を使用したときに発生します。|
|NoMethodError|定義されていないメソッドの呼び出しが行われたときに発生します。 |
|SyntaxError |ソースコードに文法エラーがあったときに発生します。|

## NameError
未定義のローカル変数や定数を使用したときに発生します。

典型的には、変数名のタイプミスや全角文字の空白を入れた場合に発生します

```ruby
# 未定義の変数を評価してみる
namae
```

実行結果

```
Main.rb:1:in `<main>': undefined local variable or method `namae' for main:Object (NameError)
```
`namae'  という変数が未定義ですという意味

変数名を間違えた場合

```ruby
x=100
puts xx
```

```
Main.rb:2:in `<main>': undefined local variable or method `xx' for main:Object (NameError)
Did you mean?  x
```


#### メソッドの引数とメソッドの内の変数名が一致していない場合

```ruby
# メソッドの引数が sss なのに、間違って　ss という変数を使ってしまった
def sakasa(sss)
   return ss.reverrse
end

puts sakasa("abc")
```

実行結果（メソッド定義の段階ではエラーにならず、メソッド呼び出しの段階でエラーがでる）

```
Main.rb:2:in `sakasa': undefined local variable or method `ss' for main:Object (NameError)
Did you mean?  sss
	from Main.rb:5:in `<main>'
```

sakasa の中に ss という未定義の変数（またはメソッド）があります。(NameError)
これは sss じゃ無いですか？

```ruby
　x=100
puts x
```

#### 全角の空白文字によるエラーの例

例えば、このプログラムはなぜエラーになるのでしょうか？

```ruby
　x=100
puts x
```

実行結果

```
Main.rb:2:in `<main>': undefined local variable or method `x' for main:Object (NameError)
```

Rubyでは、全角は英語の小文字として扱われる
このケースでは、全角空白＋x が一つの小文字の文字列になっている

```ruby
　x=100
puts 　x
```
実行結果

```
100
```

### NameErrorへの対処方法

* エラーが発生している場所を見つける
* 未定義の変数を使っていないかチェックする
* エディタで見えない文字（全角空白）を見えるようにする

#### エラーが発生している場所を見つける

* エディターの行を表示させる
* エラーメッセージが示している行を確認する
* １行ずつコメントしてエラーメッセージの変化を確認する

 エディターの行を表示させる
	Show gutter: On

* エラーメッセージが示している行を確認する

エラーメッセージにはエラーが発生している行の番号が表示されています

例
以下のエラーメッセージでは、「Main.rb:2:i」で２行目にエラーがあることを示しています。

```
Main.rb:2:in `sakasa': undefined local variable or method `ss' for main:Object (NameError)
Did you mean?  sss
	from Main.rb:5:in `<main>'
```

* １行ずつコメントしてエラーメッセージの変化を確認する

このプログラムの２行目をコメントにするとエラーが消える
２行目にエラーの原因があることがわかる

```ruby
def sakasa(sss)
#   return ss.reverrse
end

puts sakasa("abc")
```

* エラーが発生するメソッドの内容を一旦すべてコメントにしておき
* コメントを外すとエラーが発生する場所を見つける

テストデータを作成する

```ruby
sentences2=[]
```

メソッドの処理内容をすべてコメントにする

```ruby
# テスト用データ
sentences2=[]
def shuzo(ss)
#	yone=ss.select{|x|x=~/よね。/}.shuffle[0]
#	demo=ss.select{|x|x=~/でも/}.shuffle[0]
#	msg=ss.select do |x|
#		x=~/噴水|サバ|太陽|脳|マツタケ|キホン/
#	end.shuffle[0..2]
#	dakarakoso=sss.select{|x|x=~/だからこそ/}.shuffle[0]
#	nanda=ss.select{|x|x=~/なんだ。/}.shuffle[0]
#	return [yone,demo,msg,dakarakoso,nanda].join("\n")
end
puts shuzo( sentences2)
```

エラーが出ないことを確認

コメントを一つはずず（一つの文単位）

```ruby
# テスト用データ
sentences2=[]
def shuzo(ss)
	yone=ss.select{|x|x=~/よね。/}.shuffle[0]
#	demo=ss.select{|x|x=~/でも/}.shuffle[0]
#	msg=ss.select do |x|
#		x=~/噴水|サバ|太陽|脳|マツタケ|キホン/
#	end.shuffle[0..2]
#	dakarakoso=sss.select{|x|x=~/だからこそ/}.shuffle[0]
#	nanda=ss.select{|x|x=~/なんだ。/}.shuffle[0]
#	return [yone,demo,msg,dakarakoso,nanda].join("\n")
end
puts shuzo( sentences2)
```

```ruby
# テスト用データ
sentences2=[]
def shuzo(ss)
	yone=ss.select{|x|x=~/よね。/}.shuffle[0]
	demo=ss.select{|x|x=~/でも/}.shuffle[0]
#	msg=ss.select do |x|
#		x=~/噴水|サバ|太陽|脳|マツタケ|キホン/
#	end.shuffle[0..2]
#	dakarakoso=sss.select{|x|x=~/だからこそ/}.shuffle[0]
#	nanda=ss.select{|x|x=~/なんだ。/}.shuffle[0]
#	return [yone,demo,msg,dakarakoso,nanda].join("\n")
end
puts shuzo( sentences2)
```

一つのブロックのコメントを外す

```ruby
# テスト用データ
sentences2=[]
def shuzo(ss)
	yone=ss.select{|x|x=~/よね。/}.shuffle[0]
	demo=ss.select{|x|x=~/でも/}.shuffle[0]
	msg=ss.select do |x|
		x=~/噴水|サバ|太陽|脳|マツタケ|キホン/
	end.shuffle[0..2]
#	dakarakoso=sss.select{|x|x=~/だからこそ/}.shuffle[0]
#	nanda=ss.select{|x|x=~/なんだ。/}.shuffle[0]
#	return [yone,demo,msg,dakarakoso,nanda].join("\n")
end
puts shuzo( sentences2)
```


```ruby
# テスト用データ
sentences2=[]
def shuzo(ss)
	yone=ss.select{|x|x=~/よね。/}.shuffle[0]
	demo=ss.select{|x|x=~/でも/}.shuffle[0]
	msg=ss.select do |x|
		x=~/噴水|サバ|太陽|脳|マツタケ|キホン/
	end.shuffle[0..2]
	dakarakoso=sss.select{|x|x=~/だからこそ/}.shuffle[0]
#	nanda=ss.select{|x|x=~/なんだ。/}.shuffle[0]
#	return [yone,demo,msg,dakarakoso,nanda].join("\n")
end
puts shuzo( sentences2)
```

エラーが出現する

```
Main.rb:9:in `shuzo': undefined local variable or method `sss' for main:Object (NameError)
Did you mean?  ss
	from Main.rb:13:in `<main>'
```


#### 未定義の変数を使っていないかチェックする

* 変数名のタイプミスをチェックする
* メソッドの引数名と変数名の一致をチェックする
* 全角の空白が入っていないかチェックする

#### エディタで見えない文字（全角空白）を見えるようにする

未定義変数が見つからない場合、空白文字が関係している可能性が高くなります

Paiza.io の設定例
	Theme : GitHub
	Show invisible: On
	
```ruby
# 全角の空白文字を英語の小文字として認識された場合
　x=100		# '全角空白x'
puts 　x		# '全角空白x'
# 全角の空白文字を含まずに半角の空白のみの場合
  x=200
puts x
```
実行結果

```
100
200
```

しかし、全角空白を見やすくする方法は無いので、全角モードにして文字を入力するときには、空白文字を入れないように注意しましょう

## NoMethodError

定義されていないメソッドの呼び出しが行われたときに発生します。

エラーが発生する例

* 文字列オブジェクトに max など数値オブジェクトに対するメソッドを適用した
* 数値オブジェクトに gsub など文字列オブジェクトに対するメソッドを適用した
* 文字列や数値に対して、sort などの配列オブジェクトに対するメソッドを適用した
* nil に対して何かメソッドを適用した


```ruby
p "abc" =~/efg/
```

```
nil
```

```ruby
# nil にメソッドを適用した場合
x =("abc" =~/efg/)   
# 文字列のパターンがマッチしないので、xは　nil　になっている
x>3
```

```
Main.rb:3:in `<main>': undefined method `>' for nil:NilClass (NoMethodError)
```

整数に対して配列のメソッド sort を適用した場合

```ruby
n=123
n.sort
```

```
Main.rb:2:in `<main>': undefined method `sort' for 123:Integer (NoMethodError)
```

```ruby
s="abc"
s.max
```

文字列に対して数値のメソッド max  を適用した場合

```
Main.rb:2:in `<main>': undefined method `max' for "abc":String (NoMethodError)
```

### NoMethodErrorへの対処方法

* エラーが発生している場所を見つける
* オブジェクトのクラスを確認する
* オブジェクトの


#### エラーが発生している場所を見つける

まずこれが基本です！
エラーの発生場所を見つける方法は、基本的にNoNameErrorと同じ

#### オブジェクトのクラスを確認する

エラー箇所をコメントにしたうえで、
class メソッドでオブジェクトのクラスを確認する

```ruby
x =("abc" =~/efg/)   
puts x.class
#x>3
```

```
NilClass
```

* 利用可能なメソッドの一覧を確認する

methods メソッドで、そのオブジェクトに対して利用可能なメソッドの一覧を確認する

```ruby
x=123
p x.methods
# x.gsub()
```
```ruby
[:-@, :**, :<=>, :upto, :<<, :<=, :>=, :==, :chr, :===, :>>, :[], :%, :&, :inspect, :+, :ord, :-, :/, :*, :size, :succ, :<, :>, :to_int, :coerce, :divmod, :to_s, :to_i, :fdiv, :modulo, :remainder, :abs, :magnitude, :integer?, :numerator, :denominator, :floor, :ceil, :round, :truncate, :lcm, :to_f, :^, :gcdlcm, :odd?, :even?, :allbits?, :anybits?, :nobits?, :downto, :times, :pred, :pow, :bit_length, :digits, :rationalize, :gcd, :to_r, :next, :div, :|, :~, :+@, :eql?, :singleton_method_added, :i, :real?, :zero?, :nonzero?, :finite?, :infinite?, :step, :positive?, :negative?, :rectangular, :arg, :real, :imaginary, :imag, :abs2, :angle, :phase, :conjugate, :conj, :to_c, :polar, :clone, :dup, :rect, :quo, :between?, :clamp, :instance_variable_set, :instance_variable_defined?, :remove_instance_variable, :instance_of?, :kind_of?, :is_a?, :tap, :instance_variable_get, :instance_variables, :method, :public_method, :singleton_method, :define_singleton_method, :public_send, :extend, :to_enum, :enum_for, :pp, :=~, :!~, :respond_to?, :freeze, :object_id, :send, :display, :nil?, :hash, :class, :singleton_class, :itself, :yield_self, :taint, :tainted?, :untrust, :untaint, :trust, :untrusted?, :methods, :frozen?, :protected_methods, :singleton_methods, :public_methods, :private_methods, :!, :equal?, :instance_eval, :instance_exec, :!=, :__send__, :__id__]
```

利用しているメソッドが利用可能なメソッドの一覧に含まれているか確認する

```ruby
x=123
p x.methods.member?('gsub')
# x.gsub()
```

```ruby
false
```

### SyntaxError
ソースコードに文法エラーがあったときに発生します。
典型的には、文字列の " が開始したまま終了していなかったときなど

```ruby
def hello(name)
	puts "こんにちは"+name+"さん
end
hello("やまさき")
```

```
Main.rb:4: syntax error, unexpected tIDENTIFIER, expecting keyword_end
hello("やまさき")
       ^~~~~~~~~~~~
Main.rb:4: unterminated string meets end of file
hello("やまさき")
                     ^
Main.rb:4: syntax error, unexpected end-of-input, expecting keyword_end
hello("やまさき")
                     ^
```               

if then else end の構文をミスして　iff と書いた場合

```ruby
iff true then 1 else 2 end
```

```
Main.rb:1: syntax error, unexpected keyword_then, expecting end-of-input
iff true then 1 else 2 end
         ^~~~
```

### SyntaxErrorへの対処方法

* エラーが発生している場所を見つける
* " " (ダブルクォーテーション）や ' ' （シングルクォーテーション）のマッチをチェックする
* def ~ end のマッチを確認する（インデントを利用する）
* ( ) 括弧のマッチを確認する
* {} 中括弧のマッチを確認する（インデントを利用する）
* do  ~ end のマッチを確認する（インデントを利用する）
* if ~ end のマッチを確認する（インデントを利用する）
* // のマッチを確認する

#### エラーが発生している場所を見つける

基本です！
エラーの発生場所を見つける方法は、基本的にNoNameErrorと同じ

#### " " (ダブルクォーテーション）や ' ' （シングルクォーテーション）のマッチをチェックする

```ruby
def hello(name)
    puts "こんにちは"+name+"さん
end
hello("やまさき")
```

## プログラム開発とデバッグの基本

プログラム開発のほとんどは仕様の作成とテストの実行とデバッグです。

### バグフィクス

エラーが発生したときにエラーを無くすことをバグフィックスといいます。
仕様どおりでない動きをしたときにそれを修正して正常な動きにすることもバグフィクスといいます。

### プログラムは小さく小さく分割して開発する

一度に全体を開発しようとしてはいけません

★授業資料をコピー／ペーストをして動作確認する場合も同じ！

### プログラム開発のステップ

1. 大まかな仕様を決める
	2. プログラムの機能と目的を決める
	3. 機能を分割して部品化する
	4. 部品ごとの仕様を決めていく
2. テストデータをつくる
	3. 部品ごと（単体といいます）のテストデータを作成
		4. 部品が１行の実行形式の場合
			5. メソッドチェーンがある場合は、さらにチェーンの段階ごとに分割します
		5. 部品がブロックの場合
		6. 部品がメソッドの場合
	4. 部品を全部まとめた結果、目的とするテストデータを作成します
3. 部品（単体）ごとのテストデータを実行した結果がどうなるかを定義します
5. 部品を全部まとめた結果の目的とするプログラムのテスト結果を定義します
4. これらの準備を行ったうえで、実際にプログラムをコーディングします
	5. コーディンして完成した部品ごとにテストを実施し
	6. テストデータを実行した結果が仕様どおりなら、部品の完成とします
	7. 部品を完成させていき、全部の機能をまとめたプログラムを作成します
	8. 部品を全部まとめた結果の目的とするプログラムのテスト結果が仕様どおちなら完成です
	

## プログラム開発とデバッグの実際

前回の課題をテストしながら開発してみる

### 開発するプログラムの目標

#### 入力

	行単位のメッセージの断片の配列

#### 出力
	松岡修造らしいメッセージをランダムに構成した文
	
#### 仕様を実現するための部品の機能

	* 入力メッセージの配列要素をパターンごとに分類する機能
		* 「よね。」（悩みなどへの共感）
		* 「でも、」　（自分の意見への話題の転換）
		* 例えるもの（噴水／サバ／太陽／脳／マツタケ／キホン／温泉）
		* 「だからこそ」 (例えるものが実現していること)
		* 「なんだ」（結論）
	* 分類したメッセージをランダムに選ぶ機能
	* 選んだメッセージを結合して一つの文字列にする機能

### 開発プログラムの機能分割

#### 入力メッセージをパターンごとに分類


		* 「よね。」（悩みなどへの共感）
		* 「でも、」　（自分の意見への話題の転換）
		* 例えるもの（噴水／サバ／太陽／脳／マツタケ／キホン／雪だるま／紅葉／温泉）
		* 「みろ！／だよ。」
		* （結論）(大丈夫、／大切なんだ。／思うんだ。／応援する！／信じているんだ。|るぞ！)

##### テストデータ

入力パターンを含む文字列の配列を人為的に作成する
テストデータの作成は、手間はかかりますが重要な作業です。

```ruby
testdata=[
"君はいつも、本当に頑張っているよね。", 
"でも、君の脳は「ＮＯ！」なんて言ってないはず。",
"噴水を見てみろよ。",
"サバを見てみろよ、",
"君を照らしてくれる太陽だって、",
"だったら、マツタケを見てみろよ。",
"それなら、基本って１０回言ってごらん、",
"自然の紅葉は一年に一度しか輝かない、",
"温泉のようなものじゃないかな。",
"すべてを出し切ってみろ！", 
"君の脳も、僕も、そう信じているんだ。",
"それが最高の見返りだと思うんだ。",
"時には「休む勇気」を持つことも大切なんだ。"
]
```

#### テストデータの確認

作成したテストデータに間違いがないか確認する

```ruby
n=testdata.size		# テストデータの配列の個数
# インデックス 0 から n までのテストデータを出力する
(0..n).each{|x|puts testdata[x]}
```

```
君はいつも、本当に頑張っているよね。
でも、君の脳は「ＮＯ！」なんて言ってないはず。
噴水を見てみろよ。
サバを見てみろよ、
君を照らしてくれる太陽だって、
だったら、マツタケを見てみろよ。
それなら、基本って１０回言ってごらん、
自然の紅葉は一年に一度しか輝かない、
温泉のようなものじゃないかな。
すべてを出し切ってみろ！
君の脳も、僕も、そう信じているんだ。
それが最高の見返りだと思うんだ。
時には「休む勇気」を持つことも大切なんだ。
```

#### 入力メッセージの配列要素をパターンごとに分類する機能

* 「よね。」（悩みなどへの共感）

仕様
	「よね。」を含む行が配列の要素として出力される。

```ruby
yone=testdata.select{|x|x=~/よね。/}
p yone
```

望ましい計算結果

```
 ["君はいつも、本当に頑張っているよね。"]
```

* 「でも、」　（自分の意見への話題の転換）

仕様
	「でも、」を含む行が配列の要素として出力される。

```ruby
demo=testdata.select{|x|x=~/でも、/}
p demo
```
望ましい計算結果

```
 ["でも、君の脳は「ＮＯ！」なんて言ってないはず。"]
```


* 例えるもの（噴水／サバ／太陽／脳／マツタケ／キホン／温泉）

仕様
	「噴水／サバ／太陽／脳／マツタケ／キホン／紅葉／温泉」を含む行が配列の要素として出力される。

```ruby
tatoe=testdata.select{|x|x=~/噴水|サバ|太陽|脳|マツタケ|キホン|紅葉|温泉/}
p tatoe
```

望ましい計算結果

```
["でも、君の脳は「ＮＯ！」なんて言ってないはず。", "噴水を見てみろよ。", "サバを見てみろよ、", "君を照らしてくれる太陽だって、", "だったら、マツタケを見てみろよ。", "自然の紅葉は一年に一度しか輝かない、", "温泉のようなものじゃないかな。"]
```

* 「みろ！／るんだ。」 (例えるものが実現していること)

仕様
	「みろ！／るんだ。」を含む行が配列の要素として出力される。

```ruby
mirorunda=testdata.select{|x|x=~/みろ！|るんだ。/}
p mirorunda
```

望ましい計算結果

```
["すべてを出し切ってみろ！", "君の脳も、僕も、そう信じているんだ。"]
```

* 「なんだ。」（結論）

仕様
	「なんだ。」を含む行が配列の要素として出力される。

```ruby
nanda=testdata.select{|x|x=~/なんだ。/}
p nanda
```

望ましい計算結果

```
 ["時には「休む勇気」を持つことも大切なんだ。"]
```

#### 分類したメッセージをランダムに選ぶ機能

パターンごとに分類した配列に対して、shuffle メソッドで配列要素を撹拌して、最初の要素を取り出す

```ruby
puts yone.shuffle[0]
puts demo.shuffle[0]
puts tatoe.shuffle[0]
puts nanda.shuffle[0]
```

望ましい計算結果

```
君はいつも、本当に頑張っているよね。
でも、君の脳は「ＮＯ！」なんて言ってないはず。
君を照らしてくれる太陽だって、
時には「休む勇気」を持つことも大切なんだ。
```

#### 選んだメッセージを結合して一つの文字列にする機能

構成する順序で文字列の配列を作成する
配列要素を join メソッドで連接して一つの文字列にする
join メソッドで連接するときに、改行記号(\n)を埋め込む

```ruby
puts [yone.shuffle[0], demo.shuffle[0], tatoe.shuffle[0], nanda.shuffle[0]].join("\n")
```
望ましい計算結果

```
君はいつも、本当に頑張っているよね。
でも、君の脳は「ＮＯ！」なんて言ってないはず。
サバを見てみろよ、
時には「休む勇気」を持つことも大切なんだ。
```
## 課題

「映画の視聴記録から映画名と映画名の対に対するtanimoto係数を２段階のハッシュ表にするプログラム」の仕様について

1. このプログラムの全体の仕様である２段階ハッシュを作成する機能のテストデータとその望ましい計算結果を作成してください
2. このプログラムの部品機能であるtanimoto係数を計算するメソッドのテストデータとその望ましい計算結果を作成してください



また、その仕様に基づく機能を確認するために必要なテストデータとの結果を作成してください。




