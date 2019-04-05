■■　　授業資料URL
https://drive.google.com/drive/folders/0Bwts5UTHjM9EUS14V0w0OEMyUzQ?hl=ja

第7回：条件判断

■if then elsif 文の例

#成績評価

def seiseki(score)
    if score >=90
    	puts "秀"
    elsif score >= 80
        puts "優"
    elsif score >=70
        puts "良"
    elseif score >= 60
        puts "可"
    else
		puts "不可"
    end
end

seiseki(95)
seiseki(81)
seiseki(59)


■case文の例

def omikuji
    kuji=["大吉","吉","中吉","小吉","凶","大凶"][rand(6)]
    case kuji
    when "大吉"
        puts "恋愛が成就します"
    when "吉"
        puts "あなたの人生において鍵となる人物と出会います"
    when "中吉"
        puts "失くしたもの見つかるかも"
    when "小吉"
        puts "仕事が見つかります"
    when "凶"
        puts "転居はしない方がいいでしょう"
    else
        puts "相場取引で大損をするでしょう"
    end
end

omikuji

■進級判定の例
●留年判定をメソッドにする

#留年判定メソッド

def ryunen(tanni, sinkyu_joken)
    if tanni < sinkyu_joken 
    then
        return "留年"
    else
        return "進級"
    end
end

# 印刷メソッドを付加してメソッドを呼び出す
puts  ryunen(40, 61) 
puts  ryunen(65, 61)


# 印刷メソッドを付加してメソッドを呼び出す
puts  ryunen(40, 61) 
puts  ryunen(65, 61)

●学年ごとの進級判定

def sinkyu(gakunen, tanni)
    case gakunen
    when 2
        puts ryunen(tanni, 61)
    when 3
        puts ryunen(tanni, 110)
    when 4
        puts ryunen(tanni, 124)
    end
end


sinkyu(2,59)     # 2年生で59単位
sinkyu(2,68)     # 2年生で68単位
sinkyu(3,100)   # 3年生で100単位
sinkyu(3,120)   # 3年生で120単位

●putsを外に書いてもよい

#進級要件単位数未満なら留年

def sinkyu(gakunen, tanni)
    case gakunen
    when 2
        return ryunen(tanni, 61)
    when 3
        return ryunen(tanni, 110)
    when 4
        return ryunen(tanni, 124)
    end
end

puts sinkyu(2,59)     # 2年生で59単位
puts sinkyu(2,68)     # 2年生で68単位
puts sinkyu(3,100)   # 3年生で100単位
puts sinkyu(3,120)   # 3年生で120単位

■夢の内容メソッド

def yumenonaiyo(msg)
    /(私|僕)の夢は/ =~ msg
    /になること/ =~ $'   # パターンの後半とマッチさせる
    $`                   # パターンの前半がメソッドの出力になる
end

puts yumenonaiyo('僕の夢は世界一のお金持ちになることです')



■松岡修造ボットの設計の例

def shuzo(msg)
   case msg
   when /(僕|私)の夢は/
        return yume(msg)            # 夢応答メソッド
    when /(頑張って|がんばって)/
        return ouen(msg)            # 応援応答メソッド
    when /松岡修造さんの(おかげで|言葉で)/
        return kansha(msg)         # 感謝応答メソッド
    end
end

puts shuzo("松岡修造さんのおかげで彼女ができました")

●応答メソッドを作成する

#夢応答メソッド
def yume(msg)

end

#応援応答メソッド
def ouen(msg)

end

#感謝応答メソッド
def kansya(msg)

end

