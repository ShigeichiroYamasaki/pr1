■■　　授業資料URL
https://drive.google.com/drive/folders/0Bwts5UTHjM9EUS14V0w0OEMyUzQ?hl=ja

第8回：繰り返し

■数値の配列データの合計を計算するメソッドの作成

サンプルデータ
data=[63.5, 72.1, 59.1, 47.5, 83.9]

●for文による繰り返し制御

for i in (0..4) do
  puts 2**i 
end

●for文で注意すべきこと

data=[63.5, 72.1, 59.1, 47.5, 83.9]
for i in (0..(data.size-1)) do
  puts data[i] 
end

●for文による合計計算メソッド

def sum_by_for(data)
  sum=0
  for i in (0..(data.size-1)) do
     sum=sum+data[i]
  end
  return sum
end

data=[63.5, 72.1, 59.1, 47.5, 83.9]
puts sum_by_for(data)

●timesメソッドの例

5.times do
          puts "こんにちは" 
        end

●timesメソッドのブロック変数

5.times do |i| 
           puts 2**i 
        end

●中括弧によるtimesメソッドのブロック

5.times {|i|puts 2**i}

●メソッドチェーン

puts "かもしか".gsub(/しか/,"鹿").gsub(/かも/,"鴨")

●timesメソッドによる合計メソッド

def sum_by_times(data)
  sum=0
  data.size.times do |i|
     sum=sum+data[i]
  end
  return sum
end

data=[63.5, 72.1, 59.1, 47.5, 83.9]
puts sum_by_times(data)

●timesメソッドによる合計メソッド中括弧版

def sum_by_times(data)
  sum=0
  data.size.times {|i|sum=sum+data[i]}
  return sum
end

data=[63.5, 72.1, 59.1, 47.5, 83.9]
puts sum_by_times(data)


●eachメソッドの例

[0,1,2,3,4].each do |i|
                   puts 2**i 
                 end

●eachメソッドによる合計メソッド

def sum_by_each(data)
  sum=0
  data.each do |x|
     sum=sum+x
  end
  return sum
end

data=[63.5, 72.1, 59.1, 47.5, 83.9]
puts sum_by_each(data)

●eachメソッドによる合計メソッド中括弧版

def sum_by_each(data)
  sum=0
  data.each {|x|sum=sum+x}
  return sum
end

data=[63.5, 72.1, 59.1, 47.5, 83.9]
puts sum_by_each(data)

■課題

数値の配列データの平均値を計算するメソッドを
for文を使ったもの、timesメソッドを使ったもの、eachメソッドを使ったものをそれぞ作成してください
data=[63.5, 72.1, 59.1, 47.5, 83.9]
を使って、実際にそれぞれのメソッドで計算した実行文と実行結果も提出してください

