## Date comparison in Java using LocalDate

## The goal of this post
I am writing this post to clarify date comparisons in Java so that I don't have to look things up again.

## TLDR
Use `ChronoUnit` or `Period` for getting the number of units(year, month, day) between 2 dates.  Use `ChronoUnit` to get the total number of units, and use `Period` to get the units after allocating to year, month, and date. Not really sure if that's the proper explanation so please see the example below.  
E.g.
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

## The problem I had
I ran into a bug today! The bug was caused by a piece of code that was getting the number of months between dates.
```java
// Arguments
LocalDate startDate;
LocalDate endDate;

int months = Period.between(startDate, endDate).getMonths();
```

This seems to work if the difference between `startDate` and `endDate` is less than a year, but a wrong value is returned once it's more than a year.

## The solution I came up with
After looking at the value of `getMonths()` and `getDays()` it looks like the number of units after allocating the period to years, months, and days.
```java
LocalDate startDate = LocalDate.of(2021, 1, 1);
LocalDate endDate = LocalDate.of(2022, 3, 4);
Period period = Period.between(startDate, endDate);

period.getYears(); // 1
period.getMonths(); // 2
period.getDays(); // 3
```

So I was able to get the total amount of months by the following code.
```java
Period period = Period.between(startDate, endDate);
int months = period.getYears() * 12 + period.getMonths();
```

I also found another solution that was concise and more readable.
```java
ChronoUnit.MONTHS.between(startDate, endDate);
```

## Conclusion
From now on I'm going to use `ChronoUnit` or `Period` for getting the number of units(year, month, day) between 2 dates.  Use `ChronoUnit` to get the total number of units, and use `Period` to get the units after allocating to year, month, and date. Comparing the results of these methods makes it very clear to decide which one to use for your use case.
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

## Thanks!
Thank you for reading till the end!

I would be happy to see some feedback, so please let me know your thoughts!