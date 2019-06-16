# プログラミングI 第11回
正規表現と分岐制御

## 前回の課題

松岡修造のメッセージの細かい文字列の断片の配列 sentence2 を利用して
ランダムでできるだけ自然な内容をにつぶやく shuzo メソッドを作成してください

* 自分でselectメソッドやrejectメソッドを使って、文の生成に適したパターンを見つけてください
* 生成するメッセージの構成順序を考えて、より自然な文章にしてください

###  前回への基本的アプローチ

* パターンを見つける
* メッセージを構成する
	2. 〜よね
	2. でも〜
	3. 噴水｜サバ｜太陽｜脳｜松茸
	3. だからこそ〜
	4. 〜なんだ
	

```ruby
# 松岡修造の全メッセージの配列を一つの文字列に結合
all_sentences=message.join
# 改行記号(\n)で文字列を１行ごとの配列に分解する
sentences2=all_sentences.split("\n")

yone=sentences2.select{|x|x=~/よね。/}.shuffle[0]
demo=sentences2.select{|x|x=~/でも/}.shuffle[0]
dakarakoso=sentences2.select{|x|x=~/だからこそ/}.shuffle[0]
nanda=sentences2.select{|x|x=~/なんだ。/}.shuffle[0]
msg=sentences2.select do |x|
   x=~/噴水|サバ|太陽|脳| マツタケ |キホン/
end.shuffle[0..2]
```

```ruby
# 松岡修造の全メッセージの配列を一つの文字列に結合
all_sentences=message.join
# 改行記号(\n)で文字列を１行ごとの配列に分解する
sentences2=all_sentences.split("\n")

def shuzo(ss)
	yone=ss.select{|x|x=~/よね。/}.shuffle[0]
	demo=ss.select{|x|x=~/でも/}.shuffle[0]
	msg=ss.select do |x|
		x=~/噴水|サバ|太陽|脳|マツタケ|キホン/
	end.shuffle[0..2]
	dakarakoso=ss.select{|x|x=~/だからこそ/}.shuffle[0]
	nanda=ss.select{|x|x=~/なんだ。/}.shuffle[0]
	return [yone,demo,msg,dakarakoso,nanda].join("\n")
end
puts shuzo( sentences2)
```

## エラーとデバッグ

### 未定義変数エラー (NameError)

```
Main.rb:144:in `shuzo': undefined local variable or method `ss' for main:Object (NameError)
Did you mean?  sss
```


## 正規表現

文字列のパターンを表現する方法

| 記号 | 説明 |
|:--:| :-- |
|*| 直前の文字の0回以上の繰り返し|
|+| 直前の文字の1回以上の繰り返し|
|?| 直前の文字は省略可能|
|.|任意の1文字|
|[ ]| 中のどれか1文字|
|( \| )| 区切られたどれかの文字列とマッチする|
|^|	行の先頭|
|$|	行の末尾|

### 直前の文字の0回以上の繰り返し: *

直前の文字の0回以上の繰り返し

```ryby
p /Goo*gl/=~"Gogl"
p /Goo*gl/=~"Googl"
p /Goo*gl/=~"Gooooooogl"
```

### 直前の文字の1回以上の繰り返し: +

直前の文字の1回以上の繰り返し

```ruby
p /Goo+gl/=~"Gogl"
p /Goo+gl/=~"Googl"
p /Goo+gl/=~"Gooooooogl"
```

### 直前の文字は省略可能: ?

直前の文字は省略可能

```ruby
p /Goo?gl/=~"Gogl"
p /Goo?gl/=~"Googl"
p /Goo?gl/=~"Gooogl"
```

### 任意の1文字

```ruby
p /私は.です/=~"私は神です"
p /私は.です/=~"私は人間です"
p /私は..です/=~"私は人間です"
p /私は.+です/=~"私はホモ・サピエンスです"
```

### [] 中のどれか1文字

```ruby
p /私は[鰻肉鮨]を食べたい/=~"私は鰻を食べたい"
p /私は[鰻肉鮨]を食べたい/=~"私は肉を食べたい"
p /私は[鰻肉鮨]を食べたい/=~"私は鮨を食べたい"
p /私は[鰻肉鮨]を食べたい/=~"私は米を食べたい"
```

### | で区切られたどれかの文字列とマッチする

```ruby
p /私は(ステーキ|寿司)を食べたい/=~"私はステーキを食べたい"
p /私は(ステーキ|寿司)を食べたい/=~"私は寿司を食べたい"
p /私は(ステーキ|寿司)を食べたい/=~"私はいくらを食べたい"
```

###  ^ 文字列の先頭のときだけマッチする

```ruby
p /^カモシカ/ =~ "鹿もカモシカも鹿である"
p /^カモシカ/ =~ "カモシカは鹿である"
```

### $ 文字列の最後のときだけマッチする

```ruby
p /ですか$/ =~ "あなたは大学教授ですか"
p /ですか$/ =~ "ああ大学教授ですか、ご愁傷さまです"
```

### メタ文字のエスケープ

```ruby
p /www.kindai.ac.jp/=~"http://www=kindai-ac+jp"
p /www\.kindai\.ac\.jp/=~"http://www=kindai-ac+jp"
p /www\.kindai\.ac\.jp/=~"http://www.kindai.ac.jp"
```

## 標準入力と標準出力

OSの機能とプログラムの接点

### 標準出力

OSがプログラムの出力をコンピュータの装置に出すインターフェースのこと


* 画面出力
* ネットへの出力

```ruby
puts "せかいさんこんにちは"
```

### 標準入力

OSが外部からのデータをプログラムに渡すインターフェスのこと

* キーボード入力
* ネットからの入力

```ruby
name=gets
puts name+"さんこんにちは"
```

余計な改行が入る

### chomp メソッド

行末の改行を削除するメソッド

```ruby
name=gets.chomp
puts name+"さんこんにちは"
```

### Paiza.io の標準入力と標準出力


## 対話プログラム

標準入力からのメッセージに反応し
標準出力からメッセージを返すプログラム



## 分岐制御

### if then else end

### if then elsif ... end

### case when



##  対話松岡修造ボット

def shuzo(msg)
  if /(どうしても|何度やっても|なかなか)/ =~ msg 
  then
    puts "今日からお前は、富士山だ！"
    puts "富士山みたいに日本一になるんだ！"
  end
  if /(悩んで|難し|挫折しそう|わからない|苦手)/ =~ msg 
  then
    puts "今日から君は噴水だ!!"
    puts "噴水を見てみろよ。噴水は、喜びも悲しみも、楽しさも悔しさも、すべてを一所懸命出し切っている。"
    puts "だから、あれほどキラキラと輝いているんだよ"
    puts "君も噴水になってみろ。"
  end
end

shuzo("どうしてもプログラミングがうまくなりません")
shuzo("プログラミングに挫折しそうです")

■課題
正規表現によるパターンマッチを利用して、できるだけ自然な会話をする美輪明宏ボットのプログラムを作成してください

例
miwasan("私のオーラは何色ですか")
=> あなたのオーラの色は紫ね

miwasan("私の前世は何ですか")
=> あなたの前世はピカチューね

miwasan("どうしてわかるんですか")
=> 見えるのよ



