# プログラミングI 第5回
## 配列,ハッシュと制御構造

### 配列 (Array)

```
w=[71,54,58,52]
print w
```

#### 配列のインデックス（正順）

```
w=[71,54,58,52]
puts w[0]
puts w[1]
puts w[2]
```

#### 配列の逆順のインデックス

```
weights=[71,54,58,52]
puts weights[-1]
puts weights[-2]
puts weights[-3]
puts weights[-4]
```

#### インデックスによる配列要素の代入

```
weights=[71,54,58,52]
puts weights
weights[2]=100
puts weights
```
#### 配列データの個数を得るメソッド

```
weights=[71,54,58,52]
puts weights.size
```

### 配列を正順に見たときの最後の要素のインデックス

```
weights=[71,54,58,52]
i=weights.size-1
puts weights[i] 
```

### ハッシュ(Hash)

```
yamasaki={"age"=> 60, "name"=> '山崎', "gender"=>'男'}
puts yamasaki
```

#### ハッシュのキーを使って値を取り出す

```
yamasaki={"age"=> 60, "name"=> '山崎', "gender"=>'男'}
puts yamasaki["age"]
puts yamasaki["name"]
puts yamasaki["gender"]
```

#### ハッシュのキーを使って値を設定する

```
yamasaki={}
yamasaki["age"]=60
puts yamasaki
yamasaki["name"]='山崎'
puts yamasaki
yamasaki["gender"]='男'
puts yamasaki
```

#### ハッシュの配列

```
yamasaki={"age"=> 60, "name"=> '山崎', "gender"=>'男'}
terai={"age"> 40, "name"=> '寺井', "gender"=>'男'}
takahashi={"age"=> 45, "name"=> '高橋', "gender"=>'男'}
data=[yamasaki, terai, takahashi]
puts data
```

## シンボル

```
puts :age
puts :gender
puts :name
```

#### シンボルと文字列の違い

```
puts "age".object_id
puts "age".object_id
puts :age.object_id
puts :age.object_id
```

### シンボルをキーにしたハッシュ

```
yamasaki={:age=> 60, :name=> '山崎', :gender=>'男'}
puts yamasaki
puts yamasaki[:age]
yamasaki[:age]=61
puts yamasaki[:age]
```

## 配列に対する繰り返し制御（while制御の場合）

```
weights=[71,54,58,52]
i=0
while i<=(weights.size-1) do
  puts weights[i]
  i=i+1
end
```

### 配列に対する繰り返し制御（until制御の場合）

```
weights=[71,54,58,52]
i=0
begin 
  puts weights[i]
  i=i+1
end until i> (weights.size-1)
```

### 配列の要素の合計を計算する

```
weights=[71,54,58,52]
gokei=0
i=0
while i<=(weights.size-1) do
  puts weights[i]
  gokei=gokei+weights[i]
  i=i+1
end
puts gokei
```
## 範囲(Range)

```
puts (1..10)
puts ("a".."z")
```
### 範囲オブジェクトを配列にするメソッド

```
puts (1..10).to_a
puts ("a".."z").to_a
```

### 配列のデータを範囲で取り出す

```
a=[2,4,6,8,10,12,24]
puts a[(3..5)]
puts a[3..5]
```


## 小テスト

## 課題

