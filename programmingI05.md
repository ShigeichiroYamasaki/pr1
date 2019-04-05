■■　　授業資料URL
https://drive.google.com/drive/folders/0Bwts5UTHjM9EUS14V0w0OEMyUzQ?hl=ja

第5回：便利なオブジェクト　文字列、範囲、正規表現 


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


