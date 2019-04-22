■■　　授業資料URL
https://drive.google.com/drive/folders/0Bwts5UTHjM9EUS14V0w0OEMyUzQ?hl=ja


## 変数の評価

```
name="竹書房"
p name
```

## 文字列の中で変数を評価する方法

```
name="竹書房"
p "おのれ#{name}!"
```

## " " 文字列と ' ' 文字列の違い

```
name="竹書房"
p 'おのれ#{name}!'
p "おのれ#{name}!"
```



## メソッド定義の例

```
def popco(name)
    p "おのれ#{name}!"
end
```

## 定義したメソッドの実行

```
def popco(name)
    p "おのれ#{name}!"
end

popco("竹書房")
popco("山崎")
```

## 逐次制御

```
tate=10                     # tateに10を代入
yoko=20                     # yokoに20を代入
takasa=30                   # takasaに30を代入   
taiseki=tate*yoko*takasa    # 体積を計算
print taiseki               # 体積を出力
```

## randメソッド

```
p rand(2)
p rand(2)
p rand(2)
p rand(2)
p rand(2)
p rand(2)
```

## if then end 

```
def toss        # コインを投げる
  coin=rand(2)  # 乱数生成（0か1)を出力
  if coin==1    # 条件文 乱数出力が1
  then          # 条件文がtrueのとき
    puts "表"   # 表と印刷する
  end           # if文の終わり
end
toss
toss
toss
```

## if文による制御の例

```
def toss        # コインを投げる
  coin=rand(2)  # 乱数生成（0か1)を出力
  if coin==1    # 条件文 乱数出力が1
  then          # 条件文がtrueのとき
    puts "表"   # 表と印刷する
  end           # if文の終わり
end
toss
toss
toss
```

## if文による制御の例

```
def toss        # コインを投げる
  coin=rand(2)  # 乱数生成（0か1)を出力
  if coin==1    # 条件文 乱数出力が1
  then          # 条件文がtrueのとき
    puts "表"   # 表と印刷する
  else          # 条件文がfalseのとき
    puts "裏"   # 裏と印刷する
  end           # if文の終わり
end
toss
toss
toss
```

## while文の例

```
i=1         # 変数iに1を代入する（初期化といいます）
while i<=5  # 条件文（変数iの値が５以下）がtrueのとき
  puts i    # iを評価した結果を印刷する
  i=i+1     # i+1 を変数iに代入する（iの再定義）
end         # while文の終わり
```


## until文の例

```
i=1             # 変数iに1を代入する
begin           # until文の開始
  puts i        # iを評価した結果を印刷する
  i=i+1         # i+1を変数iに代入する
end until i>5   # until文の終わり、条件文で終了条件
```


■オブジェクトID

"kindai".object_id

●全てのオブジェクトにオブジェクトIDがある

p "こんにちは".object_id
p 3.0.object_id
p 3.object_id
p true.object_id

●同じに見えるが異なるオブジェクト

p "こんにちは".object_id
p "こんにちは".object_id

■配列 (Array)

weights=[71,54,58,52]
p weights

●配列のインデックス（正順）

weights=[71,54,58,52]
p weights[0]
p weights[1]
p weights[2]
p weights[3]

●配列の逆順のインデックス

weights=[71,54,58,52]
p weights[-1]
p weights[-2]
p weights[-3]
p weights[-4]

●インデックスによる配列要素の代入

weights=[71,54,58,52]
p weights
weights[2]=100
p weights

●配列データの個数を得るメソッド

weights=[71,54,58,52]
p weights.size

●配列を正順に見たときの最後の要素のインデックス

weights=[71,54,58,52]
i=weights.size-1
p weights[i] 

■ハッシュ(Hash)

yamasaki={"age"=> 60, "name"=> '山崎', "gender"=>'男'}
p yamasaki

●ハッシュのキーを使って値を取り出す

yamasaki={"age"=> 60, "name"=> '山崎', "gender"=>'男'}
p yamasaki["age"]
p yamasaki["name"]
p yamasaki["gender"]

●ハッシュのキーを使って値を設定する

yamasaki={}
yamasaki["age"]=60
p yamasaki
yamasaki["name"]='山崎'
p yamasaki
yamasaki["gender"]='男'
p yamasaki

●ハッシュの配列

yamasaki={"age"=> 60, "name"=> '山崎', "gender"=>'男'}
terai={"age"> 40, "name"=> '寺井', "gender"=>'男'}
takahashi={"age"=> 45, "name"=> '高橋', "gender"=>'男'}
data=[yamasaki, terai, takahashi]
p data

■シンボル

p :age
p :gender
p :name

●シンボルと文字列の違い

p "age".object_id
p "age".object_id
p :age.object_id
p :age.object_id

●シンボルをキーにしたハッシュ

yamasaki={:age=> 60, :name=> '山崎', :gender=>'男'}
p yamasaki
p yamasaki[:age]
yamasaki[:age]=61
p yamasaki[:age]

■配列に対する繰り返し制御（while制御の場合）

weights=[71,54,58,52]
i=0
while i<=(weights.size-1) do
  puts weights[i]
  i=i+1
end

■配列に対する繰り返し制御（until制御の場合）

weights=[71,54,58,52]
i=0
begin 
  puts weights[i]
  i=i+1
end until i> (weights.size-1)

■配列の要素の合計を計算する

weights=[71,54,58,52]
gokei=0
i=0
while i<=(weights.size-1) do
  puts weights[i]
  gokei=gokei+weights[i]
  i=i+1
end
puts gokei


