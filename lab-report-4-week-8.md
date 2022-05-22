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

![tester1](https://user-images.githubusercontent.com/90715607/169676047-adedeac1-33b0-46df-9a4b-eccde332abb2.PNG)

My implementation failed this test. Here is the failure from JUnit:

![fail1](https://user-images.githubusercontent.com/90715607/169676181-306cf701-5d6d-4c35-8250-46b0883f04b7.PNG)

My implementation could not be fixed with a single line change. We would have to create a new if/else statement that rejects the website addition if a ` appears before the []() pair, but not after it.

The implementation that I reviewed failed this test. Here is the failure from JUnit:

![reviewfail1](https://user-images.githubusercontent.com/90715607/169678890-84888895-72e0-40e0-a4de-e349689c6ff4.PNG)

Similarly to my implementation of MarkdownParse, we cannot fix this implementation's error with a single line change. We would have to use if/else statements to set up a condition that rejects the website if it contains a `` "pair" where one ` is inside the []() pair, and the other is outside the []() pair.

### Snippet 2

With the second snippet...

```
[a [nested link](a.com)](b.com)

[a nested parenthesized url](a.com(()))

[some escaped \[ brackets \]](example.com)

```

We would expect the following array to be returned: `["a.com", "a.com(())", "example.com"]`

The following tester can be used on this snippet.

![tester2](https://user-images.githubusercontent.com/90715607/169676052-4eaf8989-21ff-4cba-8091-33ae1025acee.PNG)

My implementation failed this test. Here is the failure from JUnit:

![fail2](https://user-images.githubusercontent.com/90715607/169676196-92147d49-9bad-43e9-aa50-8cbee3b11bc6.PNG)

My implementation could not be fixed with a single line change. We would have to create a new if/else statement that rejects the website addition if there isn't a unique pairing of ( for every ).

The implementation that I reviewed failed this test. Here is the failure from JUnit:

![reviewfail2](https://user-images.githubusercontent.com/90715607/169678902-485a893f-221d-4e1b-9c84-61fbb148d4b6.PNG)

Similarly to my implementation of MarkdownParse, we cannot fix this implementation's error with a single line change. We need to create an if/else statement that checks for each ( corresponding to a ), and rejecting the website if any of the parentheses are unpaired.

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

![tester3](https://user-images.githubusercontent.com/90715607/169676061-9ea3dedb-a4c3-408e-a7fa-83439a152983.PNG)

My implementation failed this test. Here is the failure from JUnit:

![fail3](https://user-images.githubusercontent.com/90715607/169676218-612a998e-bd46-433f-a849-46a7195ddec4.PNG)

My implementation could not be fixed with a single line change. I would have to make sure the brackets [] and parentheses () are both on the same line. I would also want to check that nested URLs aren't added to the array, since the last item in the array included a []() pair WITHIN an open parenthesis before it closed.

The implementation that I reviewed failed this test. Here is the failure from JUnit:

![reviewfail3](https://user-images.githubusercontent.com/90715607/169678908-90e917cf-2d07-473a-98b1-0305b2558dbc.PNG)

Similarly to my implementation of MarkdownParse, we cannot fix this implementation's error with a single line change. We would have to add an if/else statement checking that the brackets[] and parentheses () are on the same line, which would be too complicated to fix in one line.
