## Week 8 Lab Report

In this lab report, we will compare the expected output of a working MarkdownParser with the results obtained from my MarkdownParser and a MarkdownParser implementation that I reviewed.

* [My MarkdownParser](https://github.com/theseb72/markdown-parser)
* [Reviwed MarkdownParser](https://github.com/cbaeucsd/markdown-parser/blob/main/MarkdownParse.java)

### Snippet 1

With the first snippet...

```
`[a link`](url.com)

[another link](`google.com)`

[`cod[e`](google.com)

[`code]`](ucsd.edu)
```

We would expect the following array to be returned: ```["`google.com", "google.com", "ucsd.edu"]```

The following tester can be used on this snippet.

![image](https://user-images.githubusercontent.com/90715607/169675448-e6addd1c-e4a6-4ed9-a0c7-265f51f2051e.png)

### Snippet 2

With the second snippet...

```
[a [nested link](a.com)](b.com)

[a nested parenthesized url](a.com(()))

[some escaped \[ brackets \]](example.com)

```

We would expect the following array to be returned: `["a.com", "a.com(())", "example.com"]`

The following tester can be used on this snippet.

![tester2](https://user-images.githubusercontent.com/90715607/169675458-ccfaccd1-3c1c-4957-858f-71a7c8fe0b14.PNG)


### Snippet 3

With the third snippet...

```
[this title text is really long and takes up more than 
one line

and has some line breaks](
    https://www.twitter.com
)

[this title text is really long and takes up more than 
one line](
https://sites.google.com/eng.ucsd.edu/cse-15l-spring-2022/schedule
)


[this link doesn't have a closing parenthesis](github.com

And there's still some more text after that.

[this link doesn't have a closing parenthesis for a while](https://cse.ucsd.edu/



)

And then there's more text

```

We would expect the following array to be returned: `["https://sites.google.com/eng.ucsd.edu/cse-15l-spring-2022/schedule"]`

The following tester can be used on this snippet.

![tester3](https://user-images.githubusercontent.com/90715607/169675636-97771ae4-3391-4dc7-ac0a-e23cea907e5a.PNG)
