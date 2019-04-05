■■　　授業資料URL
https://drive.google.com/drive/folders/0Bwts5UTHjM9EUS14V0w0OEMyUzQ?hl=ja

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


