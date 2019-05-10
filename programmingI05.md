# プログラミングI 第5回
## 配列,ハッシュと制御構造

### p メソッド

```
puts "こんにちは"
p "こんにちは"
puts [1,2,3]
p [1,2,3]
```

### 配列 (Array)

```ruby
w=[71,54,58,52]
p w
```

#### 配列のインデックス（正順）

```ruby
w=[71,54,58,52]
puts w[0]
puts w[1]
puts w[2]
puts w[3]
```

#### 配列の逆順のインデックス

```ruby
w=[71,54,58,52]
puts w[-1]
puts w[-2]
puts w[-3]
puts w[-4]
```

#### インデックスによる配列要素の代入

```ruby
w=[71,54,58,52]
p w
w[2]=100000
p w
```
#### 配列データの個数を得るメソッド

```ruby
w=[71,54,58,52]
puts w.size
```

#### 配列の最初と最後の要素

```ruby
w=[71,54,58,52]
puts w.first
puts w.last
```

#### 配列と配列の連結

```ruby
w=[71,54,58,52]
t=[123,156,175]
p w + t
```

#### 配列への push とpop

```ruby
d=[1,2,3]
d.push(4)
p d
puts d.pop
p d
```

#### 配列へのshift

```ruby
d=[1,2,3]
puts d.shift
p d
puts d.shift
p d
puts d.shift
p d
puts d.shift
p d

```

#### 文字列を分割して配列にする

```ruby
s= "明治,大正,昭和,平成,令和"
p s.split(',')
```

#### 配列の配列

```ruby
m1=[1,0,0,1]
m2=[0,1,1,1]
m3=[1,0,1,0]
d=[m1,m2,m3]
p d
```

### ハッシュ(Hash)

```
seiseki = {"数学"=>95, "国語"=>70, "英語"=>90}
p seiseki
```

#### ハッシュのキーを使って値を取り出す

```
seiseki = {"数学"=>95, "国語"=>70, "英語"=>90}
puts seiseki["数学"]
puts seiseki["国語"]
puts seiseki["英語"]
```

#### ハッシュのキーを使って値を設定する

```
seiseki = {}			# 空のハッシュオブジェクト
seiseki["数学"]=100
p seiseki
seiseki["国語"]=67
p seiseki
seiseki["英語"]=85
p seiseki
```

#### ハッシュの配列

```
yamasaki={"数学"=>70, "国語"=>75, "英語"=>70}
terai={"数学"=>95, "国語"=>86, "英語"=>95}
takahashi={"数学"=>90, "国語"=>100, "英語"=>85}
data=[yamasaki, terai, takahashi]
p data
```

## シンボル

```
puts :age
puts :gender
puts :name
```

#### シンボルと文字列の違い

```
p "age".__id__
p "age".__id__
p :age.__id__
p :age.__id__
```

### シンボルをキーにしたハッシュ

```
yamasaki={:数学=>70, :国語=>75, :英語=>70}
p yamasaki[:数学]
p yamasaki[:国語]
p yamasaki[:英語]=61
p yamasaki
```

## 配列に対する繰り返し制御（while制御の場合）

```
a=[1,2,3,4]
s=0					# 合計を記録する変数
while  a !=[] do		# 配列が空でない間繰り返す
	h=a.shift		# 配列要素の取り出し
  	s=s+h			# 取り出した配列要素を合計に加算する
end
puts s
```

### 配列に対する繰り返し制御（until制御の場合）

```
a=[1,2,3,4]
s=0				# 合計を記録する変数
begin
	h=a.shift	# 配列要素の取り出し
	s=s+h		# 取り出した配列要素を合計に加算する
end until a ==[]	# 配列が空になるまで繰り返す
puts s
```

### 配列の要素の合計を計算するメソッド

```
def gokei(a)
	s=0				# 合計を記録する変数
	while  a !=[] do
		h=a.shift	# 配列要素の取り出し
		s=s+h		# 取り出した配列要素を合計に加算する
	end
	return s			# 合計を返す
end

puts gokei([1,2,3,4])
```

## 小テスト


## 課題


