## Week 10 Lab Report

In this lab report, we will compare the expected output of two tests in our test-files/ folder with the results obtained from my group's MarkdownParser and the provided MarkdownParser implementation.

* [Group MarkdownParser](https://github.com/cbaeucsd/markdown-parser)
* [Provided MarkdownParser](https://github.com/nidhidhamnani/markdown-parser)

To find the tests with different results, I first moved my MarkdownParse.java file to the parent directory in ieng6.
`cp -R MarkdownParse.java $(pwd)/../`
Then, I renamed the file so I wouldn't confuse it with the other MarkdownParse.java.
`mv MarkdownParse.java MyMarkdownParse.java`
After that, I moved my MarkdownParse implementation into the repository that contains the provided MarkdownParse.
`mv MyMarkdownParse.java cse15lsp22-markdown-parser`

### Test

