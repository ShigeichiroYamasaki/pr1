# プログラミングI 第３回


## オブジェクトとメソッド、変数、代入と評価




### 文字列オブジェクトへのメソッド適用の例

#### upcase メソッド

```
puts "kindai".upcase
```

#### reverse メソッド

```
puts  "なすびとまとにんじん".reverse
```

#### sizeメソッド

```
puts "プログラミングIの授業資料".size
```

#### gsubメソッド

```
puts "しかもかもしかもしかである".gsub("しか","鹿")
```

### 整数オブジェクトへのメソッド適用の例

#### even? odd? メソッド

```
puts 8.odd?
puts 8.even?
```

#### gcd メソッド、 lcm メソッド

```
puts 56.gcd(32)
puts 56.lcm(32)
```

#### ２項演算形式とメソッド

```
puts 3+4
puts 3.+(4)
puts 3*4
puts 3.*(4)
puts 7/2
puts 7./(2)
puts 2**3
puts 2.**(3)
```

### 浮動小数点数オブジェクトのメソッド

```
puts 3.0+4.0
puts 3.0.+(4.0)
puts 3.0*4.0
puts 3.0.*(4.0)
puts 7.0/2.0
puts 7.0./(2.0)
puts 2.0**3.0
puts 2.0.**(3.0)
```

## オブジェクトID

### 文字列オブジェクトのオブジェクトID

```
puts "abc".__id__
puts "abc".__id__
```

## 変数への代入

```
wareki= "令和"
puts wareki
```

### 変数に代入し変数を対象にメソッドを適用する

```
name="yamasaki"
age=61
puts name.upcase
puts age.next
```

### 未定義変数エラー

```
kindai
```

### 利用可能なメソッドの一覧を確認する

```
print "kindai".methods

[:encode, :include?, :%, :*, :+, :count, :partition, :to_c, :sum, :next, :casecmp, :casecmp?, :insert, :bytesize, :match, :match?, :succ!, :<=>, :next!, :index, :rindex, :upto, :==, :===, :chr, :=~, :byteslice, :[], :[]=, :scrub!, :getbyte, :replace, :clear, :scrub, :empty?, :eql?, :-@, :downcase, :upcase, :dump, :setbyte, :swapcase, :+@, :capitalize, :capitalize!, :undump, :downcase!, :oct, :swapcase!, :lines, :bytes, :split, :codepoints, :freeze, :inspect, :reverse!, :grapheme_clusters, :reverse, :hex, :scan, :upcase!, :crypt, :ord, :chars, :prepend, :length, :size, :start_with?, :succ, :sub, :intern, :chop, :center, :<<, :concat, :strip, :lstrip, :end_with?, :delete_prefix, :to_str, :to_sym, :gsub!, :rstrip, :gsub, :delete_suffix, :to_s, :to_i, :rjust, :chomp!, :strip!, :lstrip!, :sub!, :chomp, :chop!, :ljust, :tr_s, :delete, :rstrip!, :delete_prefix!, :delete_suffix!, :tr, :squeeze!, :each_line, :to_f, :tr!, :tr_s!, :delete!, :slice, :slice!, :each_byte, :squeeze, :each_codepoint, :each_grapheme_cluster, :valid_encoding?, :ascii_only?, :rpartition, :encoding, :hash, :b, :unicode_normalize!, :unicode_normalized?, :to_r, :force_encoding, :each_char, :unicode_normalize, :encode!, :unpack, :unpack1, :<=, :>=, :between?, :<, :>, :clamp, :instance_variable_set, :instance_variable_defined?, :remove_instance_variable, :instance_of?, :kind_of?, :is_a?, :tap, :instance_variable_get, :instance_variables, :method, :public_method, :singleton_method, :define_singleton_method, :public_send, :extend, :to_enum, :enum_for, :pp, :!~, :respond_to?, :object_id, :send, :display, :nil?, :class, :singleton_class, :clone, :dup, :itself, :yield_self, :taint, :tainted?, :untrust, :untaint, :trust, :untrusted?, :methods, :frozen?, :protected_methods, :singleton_methods, :public_methods, :private_methods, :!, :equal?, :instance_eval, :instance_exec, :!=, :__send__, :__id__]
```

```
print "yamasaki".methods

[:encode, :include?, :%, :*, :+, :count, :partition, :to_c, :sum, :next, :casecmp, :casecmp?, :insert, :bytesize, :match, :match?, :succ!, :<=>, :next!, :index, :rindex, :upto, :==, :===, :chr, :=~, :byteslice, :[], :[]=, :scrub!, :getbyte, :replace, :clear, :scrub, :empty?, :eql?, :-@, :downcase, :upcase, :dump, :setbyte, :swapcase, :+@, :capitalize, :capitalize!, :undump, :downcase!, :oct, :swapcase!, :lines, :bytes, :split, :codepoints, :freeze, :inspect, :reverse!, :grapheme_clusters, :reverse, :hex, :scan, :upcase!, :crypt, :ord, :chars, :prepend, :length, :size, :start_with?, :succ, :sub, :intern, :chop, :center, :<<, :concat, :strip, :lstrip, :end_with?, :delete_prefix, :to_str, :to_sym, :gsub!, :rstrip, :gsub, :delete_suffix, :to_s, :to_i, :rjust, :chomp!, :strip!, :lstrip!, :sub!, :chomp, :chop!, :ljust, :tr_s, :delete, :rstrip!, :delete_prefix!, :delete_suffix!, :tr, :squeeze!, :each_line, :to_f, :tr!, :tr_s!, :delete!, :slice, :slice!, :each_byte, :squeeze, :each_codepoint, :each_grapheme_cluster, :valid_encoding?, :ascii_only?, :rpartition, :encoding, :hash, :b, :unicode_normalize!, :unicode_normalized?, :to_r, :force_encoding, :each_char, :unicode_normalize, :encode!, :unpack, :unpack1, :<=, :>=, :between?, :<, :>, :clamp, :instance_variable_set, :instance_variable_defined?, :remove_instance_variable, :instance_of?, :kind_of?, :is_a?, :tap, :instance_variable_get, :instance_variables, :method, :public_method, :singleton_method, :define_singleton_method, :public_send, :extend, :to_enum, :enum_for, :pp, :!~, :respond_to?, :object_id, :send, :display, :nil?, :class, :singleton_class, :clone, :dup, :itself, :yield_self, :taint, :tainted?, :untrust, :untaint, :trust, :untrusted?, :methods, :frozen?, :protected_methods, :singleton_methods, :public_methods, :private_methods, :!, :equal?, :instance_eval, :instance_exec, :!=, :__send__, :__id__]
```
#### 整数に対するメソッドの一覧

```
print 123.methods

[:-@, :**, :<=>, :upto, :<<, :<=, :>=, :==, :chr, :===, :>>, :[], :%, :&, :inspect, :+, :ord, :-, :/, :*, :size, :succ, :<, :>, :to_int, :coerce, :divmod, :to_s, :to_i, :fdiv, :modulo, :remainder, :abs, :magnitude, :integer?, :numerator, :denominator, :floor, :ceil, :round, :truncate, :lcm, :to_f, :^, :gcdlcm, :odd?, :even?, :allbits?, :anybits?, :nobits?, :downto, :times, :pred, :pow, :bit_length, :digits, :rationalize, :gcd, :to_r, :next, :div, :|, :~, :+@, :eql?, :singleton_method_added, :i, :real?, :zero?, :nonzero?, :finite?, :infinite?, :step, :positive?, :negative?, :rectangular, :arg, :real, :imaginary, :imag, :abs2, :angle, :phase, :conjugate, :conj, :to_c, :polar, :clone, :dup, :rect, :quo, :between?, :clamp, :instance_variable_set, :instance_variable_defined?, :remove_instance_variable, :instance_of?, :kind_of?, :is_a?, :tap, :instance_variable_get, :instance_variables, :method, :public_method, :singleton_method, :define_singleton_method, :public_send, :extend, :to_enum, :enum_for, :pp, :=~, :!~, :respond_to?, :freeze, :object_id, :send, :display, :nil?, :hash, :class, :singleton_class, :itself, :yield_self, :taint, :tainted?, :untrust, :untaint, :trust, :untrusted?, :methods, :frozen?, :protected_methods, :singleton_methods, :public_methods, :private_methods, :!, :equal?, :instance_eval, :instance_exec, :!=, :__send__, :__id__]
```

```
print 567.methods

[:-@, :**, :<=>, :upto, :<<, :<=, :>=, :==, :chr, :===, :>>, :[], :%, :&, :inspect, :+, :ord, :-, :/, :*, :size, :succ, :<, :>, :to_int, :coerce, :divmod, :to_s, :to_i, :fdiv, :modulo, :remainder, :abs, :magnitude, :integer?, :numerator, :denominator, :floor, :ceil, :round, :truncate, :lcm, :to_f, :^, :gcdlcm, :odd?, :even?, :allbits?, :anybits?, :nobits?, :downto, :times, :pred, :pow, :bit_length, :digits, :rationalize, :gcd, :to_r, :next, :div, :|, :~, :+@, :eql?, :singleton_method_added, :i, :real?, :zero?, :nonzero?, :finite?, :infinite?, :step, :positive?, :negative?, :rectangular, :arg, :real, :imaginary, :imag, :abs2, :angle, :phase, :conjugate, :conj, :to_c, :polar, :clone, :dup, :rect, :quo, :between?, :clamp, :instance_variable_set, :instance_variable_defined?, :remove_instance_variable, :instance_of?, :kind_of?, :is_a?, :tap, :instance_variable_get, :instance_variables, :method, :public_method, :singleton_method, :define_singleton_method, :public_send, :extend, :to_enum, :enum_for, :pp, :=~, :!~, :respond_to?, :freeze, :object_id, :send, :display, :nil?, :hash, :class, :singleton_class, :itself, :yield_self, :taint, :tainted?, :untrust, :untaint, :trust, :untrusted?, :methods, :frozen?, :protected_methods, :singleton_methods, :public_methods, :private_methods, :!, :equal?, :instance_eval, :instance_exec, :!=, :__send__, :__id__]
```


## オブジェクトのクラスを確認する

### class メソッド

```
puts "kindai".class
```

### 様々なオブジェクトのクラス

```
puts "kindai".class
puts 3.class
puts 3.14.class
```

### 代入した変数のクラスを確認する

```
job="kindai"
no=3
pi=3.14

puts job.class
puts no.class
puts pi.class
```

＃＃ '文字列'による文字列（String)オブジェクト

```
puts 'kindai'.class
puts 'kindai'.upcase
puts 'kindai'.reverse
```

### 文字列の中で変数を評価する方法

```
name="竹書房"
puts "おのれ#{name}"
```

## 2点間の距離を求める例

```
# 点pの座標
x1=2.0
y1=1.0
# 点qの座標
x2=5.5
y2=3.5
# pqの距離を求める
kyori=((x1-x2)**2 + (y1-y2)**2)**0.5
# 出力にｐとｑの距離であることを表示する
puts "pとqの距離は#{kyori}です"
```

## 小テスト

[https://forms.gle/vzpAeSg2pFUGwgM97
](https://forms.gle/vzpAeSg2pFUGwgM97
)


## 課題

p,q,r の３点の座標が次のとき

* p=(1.0, 2.0)
* q=(1.1, 4.5)
* r=(5.0, 1.0)

各２点間の距離をそれぞれ求めるプログラムを作成し、

その実行結果を求め、

わかりやすい文字列で出力してください
