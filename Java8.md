## Java8新機能
##### 最新IT情報勉強会
***
### 目次
- Lambda
- Stream
- Optional
- Date and Time
- defaultメソッド
***
#### About Java
Javaとは1990年代に**SunMicrosystems**が開発・発表したオブジェクト指向言語です.  
2010年に**Oracle**が買収しOracle製品の一つとなります.  
  
Javaの特長というと、**ガベージコレクション**等の機能を搭載し  
メモリの管理をほぼ意識しなくてもよい言語となりました.  
どのポインタにも指されないメモリを自動的に回収します.  
（名前が誰にも覚えられない人は死ぬという感じ）  
  
2017年9月にリリースされたJava9が現在のJavaの最新バージョンです.（2018年3月現在）  
  
##### バージョン履歴
JDK 1.0（1996年1月23日）  
JDK 1.1（1997年2月19日）  
J2SE 1.2（1998年12月8日）  
J2SE 1.3（2000年5月8日）  
J2SE 1.4（2002年2月6日）  
J2SE 5.0（2004年9月30日）  
Java SE 6（2006年12月11日）  
Java SE 7（2011年7月28日）  
**Java SE 8（2014年3月18日）**  
Java SE 9（2017年9月21日）  
  
#### Lambda　ラムダ式
ラムダ式とは一言でいうと、「**メソッド定義を式として扱える機能**」のことです.  
~~~ java
インターフェース名 オブジェクト名 = (引数1, 引数2, ・・・) -> {return 処理内容};
~~~
関数型インターフェースを実装するための記述を簡潔に書けるメリットがあります.  
Java7：
~~~ java
List<String> names = Arrays.asList("peter", "anna", "mike", "xenia");

Collections.sort(names, new Comparator<String>() {
    @Override
    public int compare(String a, String b) {
        return b.compareTo(a);
    }
});
~~~
Java8：
~~~ java
Collections.sort(names, (String a, String b) -> {
    return b.compareTo(a);
});
~~~

~~~ java
Collections.sort(names, (String a, String b) -> b.compareTo(a));
~~~

~~~ java
Collections.sort(names, (a, b) -> b.compareTo(a));
~~~


#### Stream API
よく使うと思われるStream APIについて表にまとめました.  

|Stream API|説明|記述例|
|:--|:--|:--|
|map|四則演算などの一時的な処理|list.stream().map(x -> x * 2)|
|filter|条件を満たす場合だけの処理|list.stream().filter(x -> x >= 2)|
|sorted|順番に並べる処理|list.stream().sorted()|
|distinct|重複する値を排除する処理|list.stream().distinct()|
|limit|扱うデータ件数を制限する処理|list.stream().limit(3)|

プログラムが簡潔でわかりやすくなっています.  
~~~ java
List<String> stringCollection = new ArrayList<>();
stringCollection.add("ddd2");
stringCollection.add("aaa2");
stringCollection.add("bbb1");
stringCollection.add("aaa1");
stringCollection.add("bbb3");
stringCollection.add("ccc");
stringCollection.add("bbb2");
stringCollection.add("ddd1");
~~~

~~~ java
stringCollection
.stream()
.filter((s) -> s.startsWith("a"))
.map(String::toUpperCase)
.sorted((a, b) -> b.compareTo(a))
.forEach(System.out::println);

// "AAA2", "AAA1"
~~~

#### Optional
値のない状態を「null」と言いますが、開発中はnullが原因で意図していないエラーが起こることが多いです.  
**NullPointerEception**  
そのため、エラーを未然に防ぐためにnullチェックの処理を書く必要がありました.  
一般的にはif文を使って変数内の値がnullかどうかを確認します.  
このOptionalを使うと、値がnullであるかどうかを簡潔に書くことができます.

~~~ java
String str = null;
Optional<String> value = Optional.ofNullable(str);
value.ifPresent(System.out::println);
~~~

#### 日付時刻API
元々Java7までの日付、時間の扱いはとても面倒くさいものでした.  
DateやCalenderクラスを扱うのは面倒で機能も乏しいです.  
これに対して、Java8では日時クラスの機能が強化されいろいろな処理ができるようになりました.  

|日付時刻API|説明|記述例|
|:--|:--|:--|
|Instant |日時（エポック秒）|Instant now = Instant.now()|
|LocalDateTime|タイムゾーンなし日時|LocalDateTime now = LocalDateTime.now()|
|ZonedDateTime|タイムゾーンあり日時|ZonedDateTime now = ZonedDateTime.now(ZoneId.of("Asia/Tokyo"))|

#### defaultメソッド
Java7まで、interfaceが実装を持つことはできませんでしたが、  
Java8からはデフォルト実装をもつdefaultメソッドを持つことができるようになりました。

interfaceにdefaultメソッドがあれば、interfaceを実装するクラスでオーバーライドする必要のないメソッドは書く必要がありません。
~~~ java
interface Formula {
    double calculate(int a);

    default double sqrt(int a) {
        return Math.sqrt(a);
    }
}
~~~

~~~ java
Formula formula = new Formula() {
    @Override
    public double calculate(int a) {
        return sqrt(a * 100);
    }
};

formula.calculate(100); // 100.0
formula.sqrt(16); // 4.0
~~~

~~~ java
Formula formula = a -> Math.sqrt(a*100);
~~~





