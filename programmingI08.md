# プログラミングI 第8回

map, filter, reduceによるデータ処理

## 前回の課題

映画の視聴履歴のデータが以下のようなものであるとき、

```ruby
["君の名は", 0, 1, 0, 0, 0, 1, 1, 1, 1, 1, 1, 1, 1, 0, 1]
["プレデターズ", 1, 0, 0, 1, 0, 1, 0, 0, 1, 0, 0, 0, 1, 0, 0]
["聲の形", 0, 0, 0, 1, 0, 0, 1, 0, 1, 0, 1, 1, 1, 0, 1]
["少林サッカー", 0, 1, 0, 1, 0, 1, 0, 0, 1, 0, 1, 0, 1, 0, 1]
["シンゴジラ", 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 0, 0, 1, 0, 0]
["アナと雪の女王", 0, 0, 0, 1, 1, 0, 1, 1, 1, 1, 1, 1, 1, 1, 1]
```

* 映画 "君の名は" と他の映画との間の tanimoto係数を計算するプログラムを作成して、それぞれの係数を計算してください
* また、計算の結果、この中で映画 "君の名は"に最も近い映画は何ですか？

### 課題への基本的なアプローチ

* 視聴履歴データ全体を配列の配列にする
* 配列要素になる2つのデータの配列[(1..-1)] についてtanimoto係数を計算するメソッドをmapメソッドで適用
* その結果を得る
* 最も類似度が高いものを見つける

```ruby
# データにms という名前をつける（変数に代入する）
ms=[
["君の名は", 0, 1, 0, 0, 0, 1, 1, 1, 1, 1, 1, 1, 1, 0, 1],
["プレデターズ", 1, 0, 0, 1, 0, 1, 0, 0, 1, 0, 0, 0, 1, 0, 0],
["聲の形", 0, 0, 0, 1, 0, 0, 1, 0, 1, 0, 1, 1, 1, 0, 1],
["少林サッカー", 0, 1, 0, 1, 0, 1, 0, 0, 1, 0, 1, 0, 1, 0, 1],
["シンゴジラ", 1, 0, 0, 0, 0, 0, 1, 1, 1, 0, 0, 0, 1, 0, 0],
["アナと雪の女王", 0, 0, 0, 1, 1, 0, 1, 1, 1, 1, 1, 1, 1, 1, 1]
]

# tanimoto係数メソッド(引数に文字列を含めず、数値の配列だけの比較をする)
# 例　tanimoto([1,0,0], [0,1,1])

def tanimoto(a,b)
	na=a.sum							# aの１の数
	nb=b.sum							# bの１の数
	azb=a.zip(b) 						# aとbをzipした配列
	ab=azb.map{|x|if x==[1,1] then 1 else 0 end}
	nab=ab.sum						# aとbの共通集合の数
	return nab/(na+nb-nab).to_f		# tanimoto係数
end

# msの要素 0 と 1 映画に対するtanimoto係数の計算
puts tanimoto(ms[0][1..-1], ms[1][1..-1])

# ms の要素と　ms の要素0 とのtanimoto係数を mapメソッドで配列として出力
p ms.map{|x|tanimoto(ms[0][1..-1],x[1..-1])}

# 映画名を含める（配列の配列にする）
# 映画名は、各配列要素の0番目の要素
p ms.map{|x|[x[0], tanimoto(ms[0][1..-1],x[1..-1])]}
```

## 映画視聴アンケートの全データ

実際のアンケート結果は以下のとおり。


# 映画視聴アンケートの全データ

[https://github.com/ShigeichiroYamasaki/programming-I/blob/master/movies.rb](https://github.com/ShigeichiroYamasaki/programming-I/blob/master/movies.rb)


## 映画視聴アンケートの全データに対する調査

### その映画を何人が観ているか?

```ruby
# 映画ごとの１の数を合計する（視聴者数）
result=movies.map{|x|x[1..-1].sum}
p result
```

```ruby
#　アンケートをとった全映画の本数
puts result.size
```

計算結果からわかること

* 視聴者数０の（誰も観ていない）映画は無い
* 視聴者数 80 (全員が観ている) 映画も無い

###  配列内の数値の最大値と最小値

#### max メソッド

最大値を見つけるメソッド

```ruby
puts [4,1,2,9,3,5,6,8].max
```

```ruby
puts result.max
```

#### min メソッド

最小値を見つけるメソッド

```ruby
puts [4,1,2,9,3,5,6,8].min
```

```ruby
puts result.min
```

### 映画名の一覧

x[0] 映画名

```ruby
names=movies.map{|x|x[0]}
p names
```

## 配列の内容をいろいろな条件でフィルターする

配列の内容をフィルターするメソッド

### select メソッド

mapメソッドのように配列を出力するイテレータ
配列に対して、条件がtrue になる要素だけを配列として出力するメソッド

```ruby
# 1人だけしかみていない映画は何本あるか
p result.select{|x| x==1}

# 2人だけ観ている映画は何本あるか
p result.select{|x| x==2}

# 60人以上観ている映画は何本あるか
p result.select{|x| x>60}
```

### rejectメソッド

mapメソッドのように配列を出力するイテレータ
配列に対して、条件がfalse になる要素だけを配列として出力するメソッド


```ruby
# 観ている人の数が50人未満の映画は除く
p result.reject{|x| x<50}

# 観ている人の数が3人を超える映画は除く
p result.reject{|x| x>3}

# 観ている人の数が3人以上の映画は除く
p result.reject{|x| x>=3}
```

### 範囲オブジェクトを利用した映画の分布

```ruby
puts result.select{|x|(60..70).member?(x)}.size
puts result.select{|x|(50..60).member?(x)}.size
puts result.select{|x|(40..50).member?(x)}.size
puts result.select{|x|(30..40).member?(x)}.size
puts result.select{|x|(20..30).member?(x)}.size
puts result.select{|x|(10..20).member?(x)}.size
puts result.select{|x| (0..10).member?(x)}.size
```

### 具体的な映画名も知りたい

数値だけでなく、映画名と数値の配列で出力すればよい

```ruby
# 映画名と映画ごとの１の数を合計する
# x[0] 映画名
# x[1..-1].sum 映画を観た人数
result2=movies.map{|x|[x[0], x[1..-1].sum]}
p result2
```

### 観ている人が少ない映画

フィルターで選択する

result2 の要素は、[映画名, 人数]
ブロック変数がｘとすると、
    映画名は、　x[0]
    人数は、　   x[1]    

```ruby
# 人数でセレクトする
p result2.select{|x|x[1]==1}
p result2.select{|x|x[1]==2}
p result2.select{|x|x[1]==3}
```

### 観ている人が多い映画

```ruby
# 人数の範囲でセレクトする
p result2.select{|x|x[1]>60}
p result2.select{|x|(50..60).member?(x[1])}
p result2.select{|x|(40..50).member?(x[1])}
p result2.select{|x|(30..40).member?(x[1])}
```

### 配列要素の整列

ソート(sort)：配列の要素を順に並べること

#### sortメソッド

```ruby
p [4,1,2,9,3,5,6,8].sort
```

#### sort_byメソッド

配列要素の参照する場所を決めてソートできる

```ruby
# 配列要素のインデックス１の要素でソートする
[["a",6], ["b",3], ["c",1], ["d", 7]].sort_by{|x|x[1]}
```
映画の視聴者数でソートする

```ruby
p result2.sort_by{|x|x[1]}
```

###  reverse メソッド

配列の順序を逆転させる

```ruby
p [1,2,3,4,5,6].reverse
```

## 映画視聴アンケート全データのtanimoto係数

### tanimoto係数

```ruby
def tanimoto(a,b)
	na=a.sum						# aの１の数
	nb=b.sum						# bの１の数
	azb=a.zip(b) 					# aとbをzipした配列
	ab=azb.map{|x|if x==[1,1] then 1 else 0 end}
	nab=ab.sum						# aとbの共通集合の数
	return nab/(na+nb-nab).to_f		# tanimoto係数
end
```

### "聲の形" と他の映画との間のtanimoto係数

movies[19] 　が　"聲の形"

```ruby
# "聲の形"
koenokatachi=movies[19]
p koenokatachi

# "聲の形"と他の映画とのtanimoto係数の計算
name=koenokatachi[0]            # 聲の形の映画名
data=koenokatachi[1..-1]        # 聲の形の視聴データ
result3=movies.map{|x|[name,x[0],tanimoto(data,x[1..-1])]} 
# 計算結果の配列
p result3
``` 

### "聲の形" に視聴履歴が近い映画の順にソートする

sort_by メソッドを利用する

```ruby
p result3.sort_by{|x|x[2]}
```

逆順にする

```ruby
p result3.sort_by{|x|x[2]}.reverse
```

最も似ている３つを取り出す

```ruby
p result3.sort_by{|x|x[2]}.reverse[1..3]
```

```ruby
[["聲の形", "君の名は", 0.5606060606060606], ["聲の形", "トイ・ストーリー", 0.5507246376811594], ["聲の形", "ミニオンズ", 0.5263157894736842]]
```

## 全映画の組み合わせのtanomoto係数

映画と映画のtanimoto係数の表をつくる

カラムと行に名前がついている表

|                  |ジョーズ|紅の豚|サマーウォーズ|
|-------------|:---:|:---:|:---:|
|**ジョーズ**|1.0|0.2666|0.3125|
|**紅の豚**|0.2666|1.0|0.657|
|**サマーウォーズ**|0.3125|0.657|1.0|

## ハッシュの復習

### ハッシュの中にハッシュを入れる

```ruby
table={}
table["聲の形"]={}
p table["聲の形"]
```

```ruby
table={}
table["聲の形"]={"君の名は"=>0.5606060606060606}
p table["聲の形"]
```

#### 2段階のハッシュの値へのアクセス

```ruby
table={}
table["聲の形"]={"君の名は"=>0.5606060606060606}
p table["聲の形"]["君の名は"]
```

###  ２段階のハッシュを使って表を作成する

* ハッシュの値がまたハッシュになっている

```ruby
table={"ジョーズ"=>{"ジョーズ"=>1.0, "紅の豚"=>0.2666, "サマーウォーズ"=>0.3125}, "紅の豚"=>{"ジョーズ"=>0.2666, "紅の豚"=>1.0, "サマーウォーズ"=>0.657}, "サマーウォーズ"=>{"ジョーズ"=>0.3125, "紅の豚"=>0.657, "サマーウォーズ"=>1.0}}
```

* １段階目のハッシュ値へのアクセス

```ruby
p table["ジョーズ"]
```

```ruby
{"ジョーズ"=>1.0, "紅の豚"=>0.2666, "サマーウォーズ"=>0.3125}
```

* 2段階目のハッシュ値へのアクセス

```ruby
p table["ジョーズ"]["紅の豚"]
```

```ruby
 0.2666
```

## ハッシュオブジェクトのマージ(統合)

### mergeメソッド

２つのハッシュオブジェクトを１つにまとめる
同じキーが衝突している場合は、引数のハッシュのものに上書きされる


```ruby
h1={"a"=>1}
h2={"b"=>2}
p h1.merge(h2)
```

```ruby
{"a"=>1, "b"=>2}
```

## 2段階のイテレータ

イテレータの中でイテレータを実施する

### eachメソッドのブロックの中でeachメソッドを実行する

```ruby
a=[1,2,3]
b=["a","b"]

a.each do|x| 
    b.each do |y|
		p [x,y]
    end 
end
```

```ruby
key=["ジョーズ","紅の豚","サマーウォーズ"]
value=[1.0, 0.2666, 0.3125]
```

```ruby
# まず１段階目のイテレータ
key.each do|k| 
    puts k
end
```

```ruby
# ２段階目だけのイテレーション
value.each do |v|
     puts v
end
```

```ruby
# 1段階目の中に２段階目が埋め込まれたイテレーション
key.each do |k| 
    value.each do |v| 
        p [k,v]
    end
end
```

### for文のブロックの中でfor文を実行する

```ruby
key=["ジョーズ","紅の豚","サマーウォーズ"]
value=[1.0, 0.2666, 0.3125]
```

```ruby
# 1段階目だけのイテレーション
for k in key do
  puts k
end
```

```ruby
# 2段階目だけのイテレーション
for v in value do
  puts v
end
```

```ruby
# 1段階目の中に２段階目が埋め込まれたイテレーション
for k in key do
  for v in value do
    p [k,v]
  end
end
```

### 表を配列の中の配列として表現する


|1.0|0.2666|0.3125|
|:---:|:---:|:---:|
|0.2666|1.0|0.657|
|0.3125|0.657|1.0|

```ruby
[[1.0,0.2666, 0.3125], [0.2666, 1.0, 0.3125], [0.3125,0.2666, 1.0]]
```

### カラム名（キー）付きの表を配列の中の配列として表現する


|ジョーズ|紅の豚|サマーウォーズ|
|:---:|:---:|:---:|
|1.0|0.2666|0.3125|
|0.2666|1.0|0.657|
|0.3125|0.657|1.0|


```ruby
[["a", [1, 2, 3]], ["b", [1, 2, 3]], ["c", [1, 2, 3]]]
```
### map メソッドの中でmapメソッドを実行する

配列の中に配列を入れる自然な方法
    
```ruby
key=["ジョーズ","紅の豚","サマーウォーズ"]

# 1段階目の中に２段階目が埋め込まれたイテレーション
tbl=key.map do |k1| 
        key.map do |k2|
            [k1,k2]
        end
end
p tbl
```

## 2段ハッシュを使った表の作成

カラム名と行名の両方がついた表をつくる


|                  |ジョーズ|紅の豚|サマーウォーズ|
|-------------|:---:|:---:|:---:|
|**ジョーズ**|1.0|0.2666|0.3125|
|**紅の豚**|0.2666|1.0|0.657|
|**サマーウォーズ**|0.3125|0.657|1.0|

### 2段ハッシュで映画と映画のtanomoto係数の表をつくる

#### まず1段目のハッシュを作成する

```ruby
row={}           #メモ変数rowを空のハッシュで初期化
movies.each do |x| 
    row[x[0]]={} #メモ変数に映画名をキーとして登録
                 # 値は空のハッシュ
end

p row
```

### 各ハッシュの値にtanomoto係数を値とするハッシュを埋め込んでいく

```ruby
def tanimoto(a,b)
    na=a.sum                            # aの１の数
    nb=b.sum                            # bの１の数
    azb=a.zip(b)                        # aとbをzipした配列
    ab=azb.map{|x|if x==[1,1] then 1 else 0 end}
    nab=ab.sum                      # aとbの共通集合の数
    return nab/(na+nb-nab).to_f     # tanimoto係数
end

table={}
movies.each do |x|			# 行のキー
	table[x[0]]={}
   movies.each do |y| 		# 列のキー
		 table[x[0]][y[0]]=tanimoto(x[1..-1],y[1..-1])
   end
end

p table
```

### 各ハッシュの値にtanomoto係数を値とするハッシュを埋め込んでいく（for文版）

```ruby
table={}
for x in movies do		    # 行のキー
    table[x[0]]={}
    for y in movies do	     # 列のキー
        table[x[0]][y[0]]=tanimoto(x[1..-1],y[1..-1])
   end
end

p table
```

## reduceによる表の作成

mergeメソッドを使っていることに注意

```ruby
table=movies.reduce({}) do |t,x|
	column=movies.reduce({}) do |c,y|
		c.merge({[y[0]]=>tanimoto(x[1..-1],y[1..-1])})
	end
	t.merge({x[0]=>column})
end

p table

```

#### もっとコンパクトにも書けます

```ruby
table=movies.reduce({}) {|t,x|
	 t.merge({x[0]=>movies.reduce({}){|c,y|
		c.merge({[y[0]]=>tanimoto(x[1..-1],y[1..-1])})}})}
		
p table
```

```ruby
table["舟を編む"]["プラダを着た悪魔"]
```

## この映画を観ている人はこの映画も観ている

その映画自身とのtanimoto係数は、1.0 でその次の映画が最も近いと言える

「舟を編む」を観ている人はどんな映画を観ているか？
 
 ```ruby
 p table["舟を編む"].sort_by{|x|x[1]}.reverse[1..3]
 ```

```ruby
["言の葉の庭", 0.5833333333333334]
```

```ruby
def miteiru(t, name)
   t[name].sort_by{|x|x[1]}.reverse[1..3]
end
```

```ruby
p miteiru(table,"言の葉の庭")
```
## 課題

映画の視聴記録から２段階のハッシュ表を作成するプログラムを以下の方法で作成してください

* eachメソッドを使う方法
* for文を使う方法

作成した表を使って、以下の映画のそれぞれについて

類似度が高い順に５つ取り出し、さらにその５つの中から類似度が0.4に満たないものは reject メソッドを使って除いた結果を表示してください

* 未来のミライ
* バタフライ・エフェクト
* グレイテストショーマン
* フォレストガンプ
* シェイプオブウォーター
* アオハライド

