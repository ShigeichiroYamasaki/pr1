# プログラミングI 第4回

## メソッド定義, 制御構造

## メソッド定義の例

```ruby
def plus
	return(1+2)
end
```
## 定義したメソッドの実行

```ruby
def plus
	return(1+2)
end
puts plus
```
```
3
```

### return 文がメソッドの適用結果を決める

```ruby
def plus
	3+5
	return(5*8)
	2**3
end
```


### randメソッド

乱数を出力するメソッド

実行するたびに異なる結果になる


```ruby
puts rand(6)
puts rand(6)
puts rand(6)
puts rand(6)
```

### サイコロを模倣するメソッドの例

```ruby
def saikoro
	r=rand(6)
	s=r+1
	return(s)
end

puts saikoro
puts saikoro
puts saikoro
```

## 引数付きメソッド定義と適用

```ruby
def plus(x,y)
    return(x+y)
end
puts plus(3,7)
puts plus(2,6)
```

### 2点間の距離を求めるメソッド

```ruby
def kyori(x1,y1,x2,y2)
	dx=x2-x1
	dy=y2-y1
	d=(dx**2+dy**2)**0.5
	return d
end

puts kyori(0.0, 0.0, 1.0, 1.0)
```

## コメント

### コメントでプログラムが読みやすくなる

```ruby
name="竹書房"            # 対象の名前を指定する
message="おのれ#{name}"  # メッセージを作成する
puts message             # メッセージの出力
```

### 複数行のコメント

```ruby
=begin
kyoriは、平面上の2点p,q 間の距離を求めるメソッド
x1 は、点pのx座標の値
y1 は、点pのy座標の値
x2 は、点qのx座標の値
y2 は、点qのy座標の値
=end

def kyori(x1,y1,x2,y2)
	dx=x2-x1
	dy=y2-y1
	d=(dx**2+dy**2)**0.5
	return d
end

puts kyori(0.0, 0.0, 1.0, 1.0)
```

## ' (シングルクォート)' による文字列

```ruby
puts 'kindai'.class
puts 'kindai'.upcase
puts 'kindai'.reverse

```

## " " 文字列と ' ' 文字列の違い

```ruby
name="竹書房"
p 'おのれ#{name}!'
p "おのれ#{name}!"
```


## 逐次制御

```ruby
puts "サイコロ1回目#{rand(6)+1}"
puts "サイコロ2回目#{rand(6)+1}"
puts "サイコロ3回目#{rand(6)+1}"
```

## 条件文

```ruby
coin=rand(2)	# 0から1 をランダムに出力して 変数coin に代入
puts coin==0 	# 変数coinが0のときtrueとなる条件文
puts coin==1	# 変数coin が１のときにtrueとなる条件文
```

## if 文の例

```ruby
kyori = rand(20)
if kyori<10
then 	# 距離が10cm未満
 	puts "停止"
 else 	# 距離が10cm以上
 	puts "前進"
 end           	

```


## while文の例

```ruby
kyori=15			# 変数 kyori を１５として初期化
while kyori >= 10 do #距離が10cm 以上の間継続
	puts "前進"
	kyori=kyori-1	# 変数 kyori の内容を１減算して修正
end					# while の繰り返し制御の終了
puts "停止"
```

### 変数 kyori の内容も出力する

```ruby
kyori=15			# 変数 kyori を１５として初期化
while kyori >= 10 do	#距離が10cm 以上の間継続
	puts "前進 #{kyori}"
	kyori=kyori-1	# 変数 kyori の内容を１減算して修正
end					# while の繰り返し制御の終了
puts "停止 #{kyori}"
```

## until文の例

```ruby
kyori=15			# 変数 kyori を１５として初期化
begin 	
	puts "前進"
	kyori=kyori-1	# 変数 kyori の内容を１減算して修正
end	until kyori < 10	# 距離が10cm 未満なら停止
puts "停止"

```

## 小テスト

[https://forms.gle/aeE31iSFZv3j6abs7
](https://forms.gle/aeE31iSFZv3j6abs7
)

## 課題

nの階乗を計算するメソッドを作成してください

実際に100の階乗を実行し、その結果を書いてください
