## Text selection between symbols in vim

I love vim, and I always use either vim in a terminal or a vim emulator in my IDE. One of the commands I use most frequently is the text selection between symbols.

## Using `vib` to select text inside between parenthesis
You can type `vib` inside a pair of parenthesis to select text in visual mode inside the parenthesis. For example, let's say your cursor is inside the parenthesis in the text of the first bullet and you typed `vib`. The text will be highlighted like the second bullet
- void aMethod(String arg);
- void aMethod(`String arg`);

This is very useful when programming, since many of the programming languages use parenthesis. Especially lisp since the language is basically made up of parenthesis. I usually use this to change the parameters and arguments in Java. 

## Using `vab` to select text around a pair of parenthesis
`vab` is very similar to `vib` but you select the parenthesis itself as well. For example, let's say your cursor is inside the parenthesis in the text of the first bullet and you typed `vab`. The text will be highlighted like the second bullet
- void aMethod(String arg);
- void aMethod`(String arg)`;

You can see that the parenthesis is also highlighted. This is useful when you want to get rid of the whole thing including the parenthesis.

## Selecting text inside a pair of other symbols
`vi_` and `va_` are not only for parenthesis but you can also use them to highlight inside other symbols too. The ones I frequently use are:
- `vi"`: highlight inside double quotes
- `vi'`: highlight inside single quotes
- `vit`: highlight inside tags (tags as in HTML tags XML tags)
- `vi{`: highlight inside curly braces
- `vi[`: highlight inside brackets

## Using other commands on selected text
`vi_` doesn't have to start with a `v`. If you start with a `d`, for example, you can delete the selected text instead of highlighting it by typing `di_`. You can also you `c` to delete and then go into insert mode, and also `y` to yank the text.

## Thanks!
Thanks for reading till the end! I hope you find this helpful!
