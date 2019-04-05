# プログラミングI 第３回

## 変数への代入

```
x=10
y=20
z=30
taiseki=x*y*z
p taiseki
```

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


