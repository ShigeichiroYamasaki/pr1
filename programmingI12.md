# プログラミングI 第12回

入力と出力、ライブラリの利用、ネットワークの利用

## 前回の課題

ユーザIDのフォーマットを

「6文字のアルファベット　＋　３桁の数字」とします。

例："abcdef123"

正規表現を使って入力したユーザIDの文字列がこのフォーマットであることを検証し、
正しいフォーマットの場合に true そうでない場合に flase を返すメソッド valid_id を作成してください


### 課題への方針

* ６文字のアルファベットで始まる文字列の正規表現の作成
* ３文字の数字で終わる文字列の正規表現の作成
* メソッド化する

#### アルファベット文字列の正規表現

アルファベットの１文字を表すメタ文字

```
[a-zA-Z]
```

アルファベット6文字の正規表現

```ruby
/[a-zA-Z]{6}/=~"abcdAB"
/[a-zA-Z]{6}/=~"abcdA"
/[a-zA-Z]{6}/=~"abcdABC"
```

行頭がアルファベット6文字の正規表現

#### 数値文字列の正規表現

数字１文字のメタ文字

```
\d
```

または

```
[0-9]
```

数値3文字の正規表現

```
/\d{3}/=~"123"
/\d{3}/=~"12"
/\d{3}/=~"1234"
```

#### ６文字のアルファベットで始まり３文字の数値で終わる正規表現

```
/^[a-zA-Z]{6}\d{3}$/
```

```
/^[a-zA-Z]{6}\d{3}$/=~"abcdef123"
/^[a-zA-Z]{6}\d{3}$/=~"abcdefg123"
/^[a-zA-Z]{6}\d{3}$/=~"abcdef1234"
/^[a-zA-Z]{6}\d{3}$/=~"1bcdef123"
/^[a-zA-Z]{6}\d{3}$/=~"abcdef1b3"
```

#### メソッド化

```ruby
def valid_id(s)
	if /^[a-zA-Z]{6}\d{3}$/=~s then
		return true
	else
		return false
	end
end
```

#### テストデータと望ましい結果

```ruby
t1="abcdef123" 
t2="abcdefg123"
t3="a12cdef123"
t4="abcdef1234"
```

```ruby
valid_id(t1)
valid_id(t2)
valid_id(t3)
valid_id(t4)
```
```ruby
true
false
false
false
```

## 入力と出力

### 標準入力と標準出力

* (Linux系) OSの入出力機能
* Linux系 OS とは、Linux だけでなくMacOSXも含まれる
* Windows OS にも標準入力と標準出力の機能が備わっている

### 標準出力

####  (Linux系) OSがプログラムの出力をコンピュータの装置に出すインターフェースのこと

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

### Paiza.io の標準入力と標準出力



### chomp メソッド

行末の改行を削除するメソッド

```ruby
name=gets.chomp
puts name+"さんこんにちは"
```


## CSV データ

```ruby
require 'csv'
raw= CSV.read('File1')
data=raw.map do |r|
        r.map do |c| 
                if /\d+/=~c then       # 数値の文字列
                        c.to_i         # 文字列を整数に変換
                else 
                        c 
                end
            end
        end
    
p data
```


