## LocalDateで日にちの比較

## 目的
`LocalDate`を使った日にちの比較で引っかかりそうな点を発見したのでみんなに知ってもらいたいです。

## TLDR
２つの`LocalDate`の日にちを比較するときは`ChronoUnit`と`Period`が役立ちます。`ChronoUnit`は日時の単位（年、月、日など）ごとに違いを計算するのに役立ちます。`Period`は年、月、日に割り当てたあとの日にちの単位の違いを計算するのに役立ちます。説明だけだと分かりづらいので下記の例を見てください。
```java
LocalDate startDate = LocalDate.of(2021, 1, 1);
LocalDate endDate = LocalDate.of(2022, 1, 1);
ChronoUnit.YEARS.between(startDate, endDate); // 1
ChronoUnit.MONTHS.between(startDate, endDate); // 12
ChronoUnit.DAYS.between(startDate, endDate); // 366

Period period = Period.between(startDate, endDate);
period.getYears(); // 1
period.getMonths(); // 0
period.getDays(); // 0
```

## LocalDateを使った日にちの比較で起こったバグ
２つの`LocalDate`の比較でバグが起きてました。月の計算を`Period`を使って下記のように計算していました。

```java
// Arguments
LocalDate startDate;
LocalDate endDate;

int months = Period.between(startDate, endDate).getMonths();
```

最初はこれでちゃんと計算されていましたが、一年経ってから動かなくなりました。

### バグの原因
月の計算に使っていた`Period`の`getMonths()`メソッドが、２つの日にちの月の違いを取得するものではありませんでした。実際は年、月、日に割り当てたあとの月の違いが計算されていました。
```java
LocalDate startDate = LocalDate.of(2021, 1, 1);
LocalDate endDate = LocalDate.of(2022, 3, 4);
Period period = Period.between(startDate, endDate);

period.getYears(); // 1
period.getMonths(); // 2
period.getDays(); // 3
```

### 解決方法
`Period`を使った正しい月の計算は下記でした。
```java
Period period = Period.between(startDate, endDate);
int months = period.getYears() * 12 + period.getMonths();
```

`ChronoUnit`っていうクラスを使えばもっとシンプルにできます。
```java
ChronoUnit.MONTHS.between(startDate, endDate);
```

## 結論
２つの`LocalDate`の計算をするときは`ChronoUnit`と`Period`の違いを理解して使い分けたほうがいいです。`ChronoUnit`は日時の単位（年、月、日など）ごとに違いを計算するのに使い、`Period`は年、月、日に割り当てたあとの日にちの単位の違いを計算するのに役立ちます。
```java
LocalDate startDate = LocalDate.of(2021, 1, 1);
LocalDate endDate = LocalDate.of(2022, 1, 1);
ChronoUnit.YEARS.between(startDate, endDate); // 1
ChronoUnit.MONTHS.between(startDate, endDate); // 12
ChronoUnit.DAYS.between(startDate, endDate); // 366

Period period = Period.between(startDate, endDate);
period.getYears(); // 1
period.getMonths(); // 0
period.getDays(); // 0
```