Bash 脚本：学习使用正则表达式（基础）
======
正则表达式（简写为 regex 或者 regexp）基本上是定义一种搜索模式的字符串，可以被用来执行“搜索”或者“搜索并替换”操作，也可以被用来验证像密码策略等条件。

正则表达式是一个我们可利用的非常强大的工具，并且使用正则表达式最好的事情是它能在几乎所有计算机语言中被使用。所以如果你使用 Bash 脚本或者创建一个 python 程序时，我们可以使用正则表达式或者也可以写一个单行搜索查询。

在这篇教程中，我们将会学习一些正则表达式的基本概念，并且学习如何在 Bash 中使用‘grep’时使用它们，但是如果你希望在其他语言如 python 或者 C 中使用它们，你只能使用正则表达式部分。那么让我们通过正则表达式的一个例子开始吧，

 **Ex-** 一个正则表达式看起来像

 **/t[aeiou]l/**

但这是什么意思呢？它意味着所提到的正则表达式将寻找一个词，它以‘t’开始，在中间包含字母‘a e i o u’中任意一个，并且字母‘l’最为最后一个字符。它可以是‘tel’，‘tal’或者‘til’，匹配可以是一个单独的词或者其它单词像‘tilt’，‘brutal’或者‘telephone’的一部分。

 **grep 使用正则表达式的语法是**

 **$ grep "regex_search_term" file_location**

如果头脑中没有想法，不要担心，这只是一个例子，来展示可以利用正则表达式获取什么，并且相信我这是最简单的例子。我们可以从正则表达式中获取更多。现在我们将从正则表达式基础的开始。

 **（推荐阅读: [你应该知道的有用的 linux 命令][1]）**

## **基础的正则表示式**

现在我们开始学习一些被称为元字符（MetaCharacters）的特殊字符。他们帮助我们创建更复杂的正则表达式搜索项。下面提到的是基本元字符的列表，

 **. or Dot** 将匹配任意字符

 **[ ]** 将匹配范围内字符

 **[^ ]** 将匹配除了括号中提到的那个之外的所有字符

 ***** 将匹配零个或多个前面的项

 **+** 将匹配一个或多个前面的项

 **? ** 将匹配零个或一个前面的项

 **{n}** 将匹配‘n’次前面的项

 **{n,}** 将匹配‘n’次或更多前面的项

 **{n m} ** 将匹配在‘n’和‘m’次之间的项

 **{ ,m}** 将匹配少于或等于‘m’次的项

 **\ ** 是一个转义字符，当我们需要在我们的搜索中包含一个元字符时使用

现在我们将用例子讨论所有这些元字符。

### **. or Dot**

它用于匹配出现在我们搜索项中的任意字符。举个例子，我们可以使用点如

 **$ grep "d.g" file1**

这个正则表达式意味着我们在‘file_name’文件中正查找的词以‘d’开始，以‘g’结尾，中间可以有任意字符。同样，我们可以使用任意数量的点作为我们的搜索模式，如

 **T ……h**

这个查询项将查找一个词，以‘T’开始，以‘h’结尾，并且中间可以有任意 6 个字符。

###  **[ ]**

方括号用于定义字符的范围。 例如，我们需要搜索一些特别的单词而不是匹配任何字符，

 **$ grep "N[oen]n" file2**

这里，我们正寻找一个单词，以‘N’开头，以‘n’结尾，并且中间只能有‘o’，‘e’或者‘n’中的一个。 在方括号中我们可以提到单个到任意数量的字符。

我们在方括号中也可以定义像‘a-e’或者‘1-18’作为匹配字符的列表。

###  **[^ ]**

这就像正则表达式的 not 操作。当使用 [^ ] 时，它意味着我们的搜索将包括除了方括号内提到的所有字符。例如，

 **$ grep "St[^1-9]d" file3**

这意味着我们可以拥有所有这样的单词，它们以‘St’开始，以字母‘d’结尾，并且不得包含从1到9的任何数字。

到现在为止，我们只使用了仅需要在中间查找单个字符的正则表达式的例子，但是如果我们需要看的更多该怎么办呢。假设我们需要找到以一个字符开头和结尾的所有单词，并且在中间可以有任意数量的字符。这就是我们使用乘数（multiplier）元字符如 + * & ? 的地方。

{n}，{n. m}，{n , } 或者 { ,m} 也是可以在我们的正则表达式项中使用的其他乘数元字符。

### * (星号)

以下示例匹配字母k的任意出现次数，包括一次没有：

 **$ grep "lak*" file4**

它意味着我们可以匹配到‘lake’，‘la’或者‘lakkkk’

### +

以下模式要求字符串中的字母k至少被匹配到一次：

 **$ grep "lak+" file5**

这里k 在我们的搜索中至少需要发生一次，所以我们的结果可以为‘lake’或者‘lakkkk’，但不能是‘la’。

###  **?**

在以下模式匹配中

 **$ grep "ba?b" file6**

字符串 bb 或 bab，使用‘？’乘数，我们可以有一个或零个字符的出现。

###  **非常重要的提示：**

当使用乘数时这是非常重要的，假设我们有一个正则表达式

 **$ grep "S.*l" file7**

我们得到的结果是‘small’，‘silly’，并且我们也得到了‘Shane is a little to play ball’。但是为什么我们得到了‘Shane is a little to play ball’，我们只是在搜索中寻找单词，为什么我们得到了整个句子作为我们的输出。

这是因为它满足我们的搜索标准，它以字母‘s’开头，中间有任意数量的字符并以字母‘l’结尾。那么，我们可以做些什么来纠正我们的正则表达式来只是得到单词而不是整个句子作为我们的输出。

我们在正则表达式中需要增加 ? 元字符，

 **$ grep "S.*?l" file7**

这将会纠正我们正则表达式的行为。

###  **\ or Escape characters**

\ 是当我们需要包含一个元字符或者对正则表达式有特殊含义的字符的时候来使用。例如，我们需要找到所有以点结尾的单词，所以我们可以使用

 **$ grep "S.*\\." file8**

这将会查找和匹配所有以一个点字符结尾的词。

通过这篇基本正则表达式教程，我们现在有一些关于正则表达式如何工作的基本概念。在我们的下一篇教程中，我们将学习一些高级的正则表达式的概念。同时尽可能多地练习，创建正则表达式并试着尽可能多地在你的工作中加入它们。如果有任何疑问或问题，您可以在下面的评论区留言。

--------------------------------------------------------------------------------

via: http://linuxtechlab.com/bash-scripting-learn-use-regex-basics/

作者：[SHUSAIN][a]
译者：[kimii](https://github.com/kimii)
校对：[校对者ID](https://github.com/校对者ID)

本文由 [LCTT](https://github.com/LCTT/TranslateProject) 原创编译，[Linux中国](https://linux.cn/) 荣誉推出

[a]:http://linuxtechlab.com/author/shsuain/
[1]:http://linuxtechlab.com/useful-linux-commands-you-should-know/




