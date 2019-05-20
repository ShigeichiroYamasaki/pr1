■■　　授業資料URL
https://drive.google.com/drive/folders/0Bwts5UTHjM9EUS14V0w0OEMyUzQ?hl=ja

第9回：データ処理I

■排他的論理和

p 0^0
p 1^1
p 1^0
p 0^1

■メンバー判定の例

movies=["図書館戦争","ミニオンズ","君の名は","紅の豚"]
p movies.member?("君の名は")
p movies.member?("風立ちぬ")

■mapメソッドの実行例

p [1, 2, 3, 4].map{|x| x*2}

■mapメソッドの実行例2

p [1, 2, 3, 4].map{|x| 2**x}

■mapメソッドの実行例3

movies=["図書館戦争","ミニオンズ","君の名は","紅の豚"]
p1=["図書館戦争","君の名は"]
p movies.map{|m| p1.member?(m)}

■ブロック内でif文を使う

movies=["図書館戦争","ミニオンズ","君の名は","紅の豚"]
p1=["図書館戦争","君の名は"]
p movies.map{|m|
                if p1.member?(m)
                    1
                else
                    0
                end}

■人ごとに０/1の配列を出力するメソッド

movies=["図書館戦争","ミニオンズ","君の名は","紅の豚"]
p1=["図書館戦争","君の名は"]

def to_vector(movies,person)
  movies.map{|m| if person.member?(m) then
                    1
                 else
                    0
                 end}
end

p to_vector(movies,p1)

■複数の人のデータをまとめる

def to_vector(movies,person)
  movies.map{|m| if person.member?(m) then
                    1
                 else
                    0
                 end}
end

movies=["図書館戦争","ミニオンズ","君の名は","紅の豚"]
p1=["図書館戦争","君の名は"]
p2=["君の名は","紅の豚"]
p3=["図書館戦争","ミニオンズ","紅の豚"]

p [p1,p2,p3].map{|p| to_vector(movies,p)}

■transposeメソッドの実行例1

p [[1,1,1,1], [0,0,0,0]].transpose

■transposeメソッドの実行例2

p [[1,0,1,0], [0,0,1,1], [1,1,0,1]].transpose

■課題

人と人の距離を排他的論理和の和として計算するメソッドを作成してください

p1  = [1, 0, 1, 0]
p2  = [0, 0, 1, 1]

としてこの2人の距離を実際に計算してください


