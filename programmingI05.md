# プログラミングI 第5回

## 配列とハッシュ

■■　　授業資料URL
https://drive.google.com/drive/folders/0Bwts5UTHjM9EUS14V0w0OEMyUzQ?hl=ja

第5回：便利なオブジェクト　文字列、範囲、正規表現 


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



■前回の課題

weights=[71,54,58,52]
gokei=0
i=0
begin 
  gokei=gokei+weights[i]
  i=i+1
end until i> (weights.size-1)
puts gokei

■文字列

●文字列のインデックス

p "しかもかもしかもしかである"[0]
p "しかもかもしかもしかである"[1]
p "しかもかもしかもしかである"[2]
p "しかもかもしかもしかである"[3]

●インデックスによる文字列要素への代入

message="しかもかもしかもしかである"
message[2]="と"
p message

●文字列の文字数を得るメソッド

"しかもかもしかもしかである".size

■範囲(Range)

p (1..10)
p ("a".."z")

●範囲オブジェクトを配列にするメソッド

p (1..10).to_a
p ("a".."z").to_a

●配列のデータを範囲で取り出す

a=[2,4,6,8,10,12,24]
p a[(3..5)]
p a[3..5]

●文字列の部分を範囲で取り出す

"しかもかもしかもしかである"[3..6]

■正規表現
●正規表現と文字列の一致

p /しか/ =~ "しかもかもしかもしかである"
p /かもしか/ =~ "しかもかもしかもしかである"
p /もしも/ =~ "しかもかもしかもしかである"

●文字列の部分を全て置き換えるメソッド

p "しかもかもしかもしかである".gsub(/しか/,"鹿")

●文字列を置き換える順序による違い

message="しかしあしかはしかでない"
message=message.gsub(/しか/,"鹿")
message=message.gsub(/あしか/,"アシカ")
message=message.gsub(/しかし/,"然し")
puts message

message="しかしあしかはしかでない"
message=message.gsub(/あしか/,"アシカ")
message=message.gsub(/しかし/,"然し")
message=message.gsub(/しか/,"鹿")
puts message

■課題

●"しかもかもしかもしかであるしかしあしかはしかでない"
を
"鹿もカモシカも鹿である然しアシカは鹿でない"
に変換するプログラムを書いてください

●実際に実行した結果もコピーして付けてください


