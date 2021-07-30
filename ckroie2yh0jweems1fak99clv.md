## Inserting characters to a String in Java

# Inserting characters to a String in Java

## The goal of this post
I am writing this post to clarify the solution to a particular problem I had, so that next time I run into the same problem I already have a solution. 

## The problem I had
I wanted to format a phone number string.  
E.g. `"11122223333"` to `"111-2222-3333"`

I was aiming for a readable code and was not really concerned with performance so I will not mention those stuff here.

## TLDR
Use `StringBuilder`'s `insert` method!
```java
int firstHyphenIndex = "xxx".length();
int secondHyphenIndex = "xxx-xxxx".length();

String result = new StringBuilder("11122223333")
        .insert(firstHyphenIndex, "-")
        .insert(secondHyphenIndex, "-")
        .toString();
// 111-2222-3333
```

## The solution I came up with
I worked through the problem in the following order:
1. How do you insert a character at an index of a string?
2. How do you insert characters at multiple indexes of a string?

### How do you insert a character at an index of a string?
How do you convert the string `"1112222"` to `"111-2222"`?

The first solution I came up with was using substrings.
```java
String s = "1112222";
String firstPart = s.substring(0, "111".length());
String secondPart = s.substring("111".length());

String result = firstPart + "-" + secondPart;
// 111-2222
```

Then I found out that `StringBuilder` has a useful method `insert` for this operation. 
```java
String result = new StringBuilder("1112222")
        .insert("111".length(), "-")
        .toString();
// 111-2222
```

These two codes don't differ that much. So I don't really have a preference at this point. 

### How do you insert characters at multiple indexes of a string?
How do you convert the string `"11122223333"` to `"111-2222-3333"`?

Substring solution:
```java
String s = "11122223333";
int indexOfSecondPart = "111".length();
int indexOfThirdPart = "1112222".length();
String firstPart = s.substring(0, indexOfSecondPart);
String secondPart = s.substring(indexOfSecondPart, indexOfThirdPart);
String thirdPart = s.substring(indexOfThirdPart);

String result = firstPart + "-" + secondPart + "-" + thirdPart;
// 111-2222-3333
```

StringBuilder solution:
```java
String result = new StringBuilder("11122223333")
        .insert("111".length(), "-")
        .insert("111-2222".length(), "-")
        .toString();
// 111-2222-3333
```

Now the StringBuilder solution looks a lot better to me. The substring solution's result is easier to understand, but I could see myself making a mistake while writing this code. The StringBuilder solution is simpler and less error-prone in my opinion, so I'm going to use StringBuilder.

## Thanks!
Thank you for reading till the end!

I would be happy to see some feedback, so please let me know your thoughts!