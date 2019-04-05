■■　　授業資料URL
https://drive.google.com/drive/folders/0Bwts5UTHjM9EUS14V0w0OEMyUzQ?hl=ja

第14回：クラスとインスタンス

■課題の回答案

t={}
t[:日本]={}
t[:ポーランド]={}
t[:セネガル]={}
t[:コロンビア]={}
t[:日本][:ポーランド]=[0,1]
t[:日本][:セネガル]=[2,2]
t[:日本][:コロンビア]=[2,1]
t[:ポーランド][:セネガル]=[1,2]
t[:ポーランド][:コロンビア]=[0,3]
t[:セネガル][:コロンビア]=[0,1]

def complete(t)
  teams=t.keys
  teams.each do |team|
    teams.each do |aite|
      if team==aite || t[team][aite]!=nil then
      else
        v=t[aite][team]
        t[team][aite]=[v[1],v[0]]
      end
    end
  end
  return t
end

complete(t)
=> {:日本=>{:ポーランド=>[0, 1], :セネガル=>[2, 2], :コロンビア=>[2, 1]}, :ポーランド=>{:セネガル=>[1, 2], :コロンビア=>[0, 3], :日本=>[1, 0]}, :セネガル=>{:コロンビア=>[0, 1], :日本=>[2, 2], :ポーランド=>[2, 1]}, :コロンビア=>{:日本=>[1, 2], :ポーランド=>[3, 0], :セネガル=>[1, 0]}}

●各国の勝ち点を計算するメソッド

t={}
t[:日本]={}
t[:ポーランド]={}
t[:セネガル]={}
t[:コロンビア]={}
t[:日本][:ポーランド]=[0,1]
t[:日本][:セネガル]=[2,2]
t[:日本][:コロンビア]=[2,1]
t[:ポーランド][:セネガル]=[1,2]
t[:ポーランド][:コロンビア]=[0,3]
t[:セネガル][:コロンビア]=[0,1]

def complete(t)
  teams=t.keys
  teams.each do |team|
    teams.each do |aite|
      if team==aite || t[team][aite]!=nil then
      else
        v=t[aite][team]
        t[team][aite]=[v[1],v[0]]
      end
    end
  end
  return t
end

t=complete(t)

def kachiten(t,team)
  point=0
  t[team].each do |k,v|
    if v[0] > v[1] then point=point+3
    elsif v[0]==v[1] then point=point+1
    end
  end
  return point
end

p kachiten(t,:日本)
=> 4

p kachiten(t,:ポーランド)
=> 3

p kachiten(t,:コロンビア)
=> 6

p kachiten(t,:セネガル)
=> 4


■クラスとは

p "あいうえお".class
=> String
p 123.class
=> Integer
p 3.14.class
=> Float
p [1,2].class

■newメソッド

# 新しい配列のインスタンスオブジェクトを作成する
p Array.new
=> []

# 新しいハッシュのインスタンスオブジェクトを作成する
p Hash.new
=> {}

■インスタンスはオブジェクト

# 新しい配列のインスタンスを作成する
hairetu =Array.new    # 新しい配列にa という名前をつける
p hairetu
=> []

# 新しいハッシュのインスタンスを作成する
hashu =Hash.new     # 新しいハッシュにhashu という名前をつける
p hashu
=> {}


■自作のクラスのインスタンス生成

# 猫クラスの定義
class Cat
end
# 猫（タマ）のインスタンスを作成する
tama=Cat.new
# 猫（ミケ）のインスタンスを作成する
mike=Cat.new

■インスタンスメソッドの定義

# 猫クラスの定義
class Cat
  def naderu       # インスタンスメソッド定義
    puts "にゃあ"
  end
end


■インスタンスメソッドの実行

# 猫クラスの定義
class Cat
  def naderu       # インスタンスメソッド
    puts "にゃあ"
  end
end

mike=Cat.naderu    # インスタンスメソッドの実行
mike.pat
=> にゃあ

■newメソッドとinitializeメソッド

class Cat
  def initialize
  end
end

tama=Cat.new
mike=Cat.new

■インスタンスとインスタンス変数

class Cat
  def initialize(name)
    @name=name          # インスタンス変数の初期化
  end
  def naderu
    puts "わたしは#{@name}にゃあ"
  end
end

tama=Cat.new("タマ")
mike=Cat.new("ミケ")
tama.naderu
=> わたしはタマにゃあ
mike.naderu
=> わたしはミケにゃあ


■methodsメソッド

class Cat
  def initialize(name)
    @name=name          # インスタンス変数の初期化
  end
  def naderu
    puts "わたしは#{@name}にゃあ"
  end
end

tama=Cat.new("タマ")
mike=Cat.new("ミケ")

p tama.methods
 

■インスタンス変数による状態の保持1

class Omikuji
  def initialize
    @kuji=["吉","大凶","大吉","凶","中吉"]
  end
  def hiku
	return @kuji.pop    # インスタンス変数の内容を取り出していく
  end
end

omikuji=Omikuji.new
p omikuji.hiku
p omikuji.hiku
p omikuji.hiku
p omikuji.hiku
p omikuji.hiku

■インスタンス変数による状態の保持2

class Matsuoka
  def initialize
    @state="感謝"
  end
  def talk
    case @state
    when "感謝" then 
         puts "ありがとうと言ってごらん"
         @state="本気"                    # 状態を更新する
    when "本気" then
         puts "今日から君は噴水だ"
    end
  end
end

shuzo=Matsuoka.new
shuzo.talk
shuzo.talk


■クラスとインスタンスの例


class User   # Userクラスの定義
   def initialize(userID, password)  # 初期化メソッド
     @userID=userID                  # ユーザIDの設定
     @password=password              # 初期パスワードの設定
   end
   def login(userID, password)       # パスワードの変更メソッド
     if userID==@userID and @password==password then
       return true
     else
       return false
     end         
   end
end

user=User.new("yamasaki","imOmugisoba56")
user.login("yamasaki","imOmugisoba56")


■課題

次のようなユーザを意味する User クラスを作成してください
    インスタンス変数
        ユーザID, パスワード, 性別, メールアドレス
    Userクラスのインスタンス生成で設定すること
        ユーザID、パスワード、性別、メールアドレス
    Userオブジェクトへのメソッド
        ログイン, 性別の確認, メールアドレスの確認, パスワードの変更
実際にユーザを作成し、全メソッドを実行してください
    ログイン, 性別の確認, メールアドレスの確認, パスワードの変更

