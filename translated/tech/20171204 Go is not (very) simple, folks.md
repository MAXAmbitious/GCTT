> 原文链接：[https://medium.com/@bob.clark_34506/go-is-not-very-simple-folks-3e84220e73c7](https://medium.com/@bob.clark_34506/go-is-not-very-simple-folks-3e84220e73c7)

出于好奇，我最近开始接触一些 `Go` 的代码。我之前对他有一些了解，但是从来没有尝试去写（没有需求）。
但是现在 `Go` 被我们团队作为一个选择来开发一些项目，所以我感觉能够获得一些经验是很好的。

到目前为止，对于这门语言我已经学习了很长时间。在这个博客的末尾，我会写更多关于 `Go` 的干货。

社区实际上并不那么令人愉快，特别是那些因为它的简单性而主张使用 `Go` 的人。似乎简单已经成为Go 社区中的一个流行语，许多人反复重复它，却没有给出太多实际的想法。

这对我来说似乎很不幸，因为在我看来，`Go` 是一个“极其简单的语言”：

1. 不应该考虑使用 `Go` 的主要原因
2. 从他们应得的注意力中推出其他有利的理由
3. 甚至不是真的

在这篇文章中，我想围绕 `Go` 来分析一些简单需求。

*在深入之前，我想强调一件事情*：这篇文章并不是对`Go` 的批评，而是 `Go` 的宣传和倡导的方式。有时候，我可能会批评这个语言的某个方面，但这不是我们关注的重点，我只会试图用一种偶然的，事实的，每种语言都提到这些方式。

## 我来自哪里

我使用多种编程语言专业和作为一种爱好。我不赞成有“最喜欢的语言”的概念。过去我曾经有过一些最喜欢的语言，但是认识到情绪通常更好，这始终只是一个时间问题。

现在作为我工作的一部分，我在大型服务的后端使用 `C++` 和 `Python` 进行编码。过去我曾经在一个你可能知道的操作系统上工作，而且我也做了嵌入式工作。作为爱好项目的一部分，我做了其他各种事情。

我并不是说所有这些夸耀或什么（我都不是特别的），我只是想表明我对编程的许多领域至少有一些赞赏，而我正在努力保持开放的态度。
所以，不要着急，让我们开始讨论业务，看看几个主张。

### 1.“与主流语言相比，`Go` 的关键字非常少”

我从最明显的例子开始，而这个绝对是我的宠儿，当谈到围绕倡导。

首先，即使它是真实的，我不知道为什么关键字计数是一个语言的学习曲线或复杂性的任何重要。当然，如果有成千上万的关键字，这可能是一个问题。但是大多数语言最多只有几十个关键字，而在这个尺度上，这个关键字的数量是相当可观的。

我还没有听到有人因为一些关键词而抱怨某种语言。

其次，`Go` 的“低”关键字数量实际上只不过是一个聪明的律师的伎俩（也许我甚至会去“虚假广告”）。 [Go specification](https://golang.org/ref/spec#Keywords)列出了25个关键字，这个关键字比大多数其他语言要低一些，但是在我看来，`Go` 并没有使用其他语言中关键字表示的较少数量的概念，`Go` 并没有这些概念的关键字，但实际上仍将其作为语言的一部分（即实际的复杂性保持不变）。

为了说明我的意思，请考虑一个`while` 循环。 `Go` 没有这个关键字，这是真的，但它仍然有一个while循环，[文档](https://tour.golang.org/flowcontrol/3)甚至是这样说的，它的目的只是重用其他关键字。

另一个这样的例子是 `private` 和 `public`。 `Go` 没有这些关键字，但它仍然有 `private` 和 `public`，它只是使用字母大小写而不是关键字。

用来刮掉关键字的另一个技巧叫 [`Predeclared identifiers`](https://golang.org/ref/spec#Predeclared_identifiers)，在技术上它不是关键字，但是在实践中仍然需要它们，但是创建一个名称相同的变量仍然不是一个好主意，因此，在一天结束时...他们基本上是关键字。此外，其中一些预先标识的标识符是其他语言的关键字，因此仅将它们与 `Go` 的关键字列表进行比较是非常不公平的。就像苹果和桔子。

### 2. 接收者参数

[接受者参数](https://tour.golang.org/methods/1)对我来说有些古怪。看起来`GO` 似乎并不建议使用`that` 和 `self`，但是仍然需要函数方法，所以就存在‘接收者参数’，除了方法签名看上去很奇怪之外，它们基本上是一样的。


对于接收者参数我有一个问题，当访问一个方法时，我需要知道接收方参数（这是任意的）的名称，以明确这个方法的作用。语法高亮受到缺少关键字的阻碍。 （看吧？这是减少关键字实际上是如何使事情变得更加复杂）这有点像`C++` 中的隐式`this`。

这里有一个新人容易混淆的[例子](https://stackoverflow.com/questions/17932722/go-difference-between-parameter-and-receiver)。


恕我直言，最简单，最直接的方式来表达一个接收器是`UFCS`，而不是`C ++` 或`Go` 做什么。但就像我说的，我不是在抱怨`Go`，我真的不介意接受者参数的观点（如果我忍受不了`C ++` 的怪异，我可以忍受`Go` 的）。

### 3. 函数返回值

如果接收参数不够，方法签名能够得到更多的巴洛克式的各种返回值声明。一个典型的语言将允许你通过`return` 语句返回函数中的一个值。而在`Go` 语言中，你可以额外的返回多个值（我认为可以用更优雅的方式通过元组来解决，但是就这样吧）除此之外，还有[命名返回值](https://tour.golang.org/basics/7)。`IMO` 并不是一个好主意，因为他允许我们在那些很难找到返回值的地方写入混淆代码。结合接收方参数，您可以创建这样的函数签名：

```
func (f Foobar) Something(a int, b int, c int) (foo int, bar int) {
    // ...
}
```

这是有效的`GO` 代码。如您所见，有三个参数列表。我真的不希望任何人试图选择这个“简单”，因为这个语法只不过是很简单的。

### 4. 不继承

`Go`（或许只是一个社区组织）似乎很反对“传统的OOP”（不管那是什么意思，可能是`java` 或者`C++`），我记得有人说`Go` 如此却是一件好事。

除了它，`Go` 有一个功能叫做[嵌入式](https://golang.org/doc/effective_go.html#embedding)，这个文档以及一些博客文章声称`Go` 不继承。我试着用各种方式而且我真的不能摆脱这样的印象，它只是继承。上面链接的文档说：

> There’s an important way in which embedding differs from subclassing. When we embed a type, the methods of that type become methods of the outer type, but when they are invoked the receiver of the method is the inner type, not the outer one.

有差别吗？继承通常以相同的方式工作，继承的方法也对内部类型起作用。

`IMO` 真的唯一不同的是，比如，在`Go` 中，多态可以从结构体中解耦。你需要使用接口将多态性带到项目中。但一旦你做了，你可以做的事情，传统的OOP非常相似，包括重写方法 - [这里是演示](https://play.golang.org/p/DRozP3HCAk)。

关于`Go` 有件事令我很惊讶-一种简单的语言-就是你甚至可以做多重继承。**确实很糟糕。**`golang-nut` 的邮件列表中，有一个人发现，`Go` 并不能很好的处理继承的歧义。我已经调整了其中提及的代码，以便它也展示了著名的“可怕的钻石问题”：

```
package main
import "fmt"
type T1 struct {
  T2
  T3
}
type T2 struct {
  T4
  foo int
}
type T3 struct {
  T4
}
type T4 struct {
  foo int
}
func main() {
  t2 := T2{ T4{ 9000 }, 2 }
  t3 := T3{ T4{ 3 } }
  fmt.Printf("foo=%d\n", t2.foo)
  fmt.Printf("foo=%d\n", t3.foo)
  t1 := T1{
    t2,
    t3,
  }
  fmt.Printf("foo=%d\n", t1.foo)
}
```

[这是在Go 中实现的代码](https://play.golang.org/p/cSCLyGHssR)

我认为上面编译的代码没有任何警告或者错误。[这是C++中的一个类似的代码](https://ideone.com/gfKYqR)，你可以看到，它没有编译那些存在歧义的地方。

结果会如何？首先，我认为多继承的特性几乎排除了在编程语言描述中任何地方使用“简单”这个词的用法。**在我看到上面的代码后，没有人能说服我，`Go` 是最简单的语言之一，甚至可能是一种简单的语言。**它甚至没有功能的一些你可以用嵌入其他的事情，如嵌入的指针或嵌入接口指针。（我甚至不确定这些特征的含义到底是什么。）

其次，我想做一个简短的例外，就是Go语言本身。不处理这样的歧义似乎是一个设计或者实现错误。即使是`C++` 足够疯狂的编译代码没有怨言，这应该告诉你一些事情。

### 5. 错误处理

各种错误处理通常会导致一个巨大的口水战。我不想谈那件事。我曾经在不同的语言中使用过所有常见的错误处理风格（我认为），我也不喜欢所有这些语言。我认为，错误处理无论什么一直是一个`PITA`。把一种风格换成另一种风格，你只需把一套问题换成另一套。没有好的方法。

回到简单的话题：`Go` 让我选择不使用异常，这使事情更简单了。多个返回值的特征不能使事情变得简单，这意味着不能返回一个错误或成功的结果，你可以返回所有值或者都不返回（`CS` 术语你可以说这个问题是一个产品类型而不是总和式的用法）。事实上，我看过的许多对于新人的代码审查。

如果`Go` 不允许多个返回值，而有一些合适的和或者喜欢的类型，这会使事情变得更像`IMO`。出于同样的原因，忽略`GO` 或者未能向调用者或其他适当目的地报告错误是相当容易的。

另一件事，让事情不简单的恐慌。不要误解我的意思，我理解`Go` 存在的原因以及它是如何有用的，事实上，其他语言也有类似的安排。我只是提出来作为反对简单一点说一新加入者是`IMHO`我可能搞不清楚这两个设施之间的区别是什么，哪一个是适当的时候。

### 6. 泛型

这个主题和错误处理比起来，可能是一个更大的蠕虫。

和错误一样，我只想考虑一下这里的复杂性或者简单性。在`Go` 社区的许多人似乎认为，泛型的本质上是复杂的（=坏，嗯嗯嗯咳），有一个巨大的开销的一种或另一种。这在某种程度上是真实的，但我不认为它有点像有些人喜欢描绘的那样糟糕。似乎那些人已经经历了`C++` 模板的痛苦，从那以后，无论何时提及泛型，都会遭受`PTSD` 的攻击。

看到这里的人，**泛型不是一个怪物**。他们当然不需要他们在`C++` 复杂（或者其他一些奇怪的语言）。我的意思是，即使前端的人用泛型工作这些天（TypeScript, Flow, …），如果他们不害怕泛型，其他程序员应该是没有理由的：）（对不起，前端开发者，只是开个玩笑。）

人们还没有意识到，如果明智地使用泛型，泛型可以使许多类型和功能的用户更加简单。例如，考虑`Go` 的[堆中接口](https://golang.org/pkg/container/heap/)。这就是从一个堆中声明这个接口的方式：

```
popped := heap.Pop(&someheap)
myfoo := popped.(*Foo)       // ZOMG what just happened here?
```

图片解释这一个网络新手，包括恐慌的风险。也可能考虑如果他们不能真正得到整个`interface{}` 正确的话会发生什么。相比之下：

```
myfoo := heap.Pop(&someheap) // myfoo has the correct type
```

这是更容易阅读，更容易解释（你解释它就像你将解释`map `类型已经存在于`Go`！）而且在编写代码时也更难弄乱。

缺乏泛型是造成额外复杂性的原因，它在`Go` 的其他部分也会造成相当多的复杂性，主要是需要存在各种“神奇”的函数/类型。`map`，`slice` 和`channel` 类型的魔法，以及伴随的`make()` 功能，这是他们三个构造函数。`slice` 类型既可以作为数组的引用，也可以作为动态数组。（不管发生什么事，“做一件事，做好它”？）

（只是为了提醒大家，我并不介意这些，只是为了不简单的争论而提及它。）

### 7. 其他

我想我已经把主要的简单违反者排除在外了。我的单子上只剩下几个简单的：

1. `<-` 和 `->` 操作符。这些可能只是`channel` 类型的方法。
2. `iota` - 基本一样，但奇怪的枚举。
3. 固有的复杂算法
4. [如果使用一个简短的语句](https://tour.golang.org/flowcontrol/6)（有时可能有用，但`if` 语法比其他语言中使用的更复杂的话）

我想就是这样。可能忘记了什么，但我想已经足够了。

所以，我想如果`Go`不简单的话，怎么实际带来上面的话这些呢？

## 任务 - “goroutines”

这可能看起来有点显而易见，因为`goroutines` 是一个经常被提及的特性，就像“简单”一样，所以我觉得需要一个区别：我认为这不是通常意义上的并发性，它构成了Go的强度。不要误解我的意思，Go的并发性是可以的。这在任何方面都不是特别的。你有渠道，这肯定是好的，但基本上，他们只是像我在别处习惯的并发队列。然后你有通常的调用像互斥体，读写锁，条件变量等并发基元。你可以同步你的东西，你可以得到像许多其他语言一样的竞争条件和死锁。

我喜欢`goroutines`（除了明显的事实，他们是轻量级的用户空间线程）是他们可以使用I/O的方式 - 调度连接到主机操作系统的低级I/O `API` 的方式（`epoll`， `kqueue`，`IOCP`，...）。这对于程序员来说通常很难做出令人愉快和有用的东西，特别是在编译本地语言的时候。我仍然在这里了解细节，但在我看来，这是一个很好的做法，也是为什么我认为`Go` 是未来计划的一个亮点。

正如已经暗示的，我也喜欢`Go` 编译为本地代码的事实。很高兴看到新的语言使用垃圾收集（或其他形式的自动内存管理 - `Swift` 中有提及）来保留这种欺骗性。

## 结论

所以，读者们，为什么所有这些都离开了你呢？是`GO` 复杂还是其他什么原因？


当然不是，绝对不像`C ++` 或`Haskell` 那样复杂。相比之下，`Go` 的确很简单。另一方面，比较`Go` 和其他常见语言（如`Java` ，`JavaScript` ，`Python` 等）的复杂性时，情况就不太清楚了，正如我希望的那样。 （此外，这是一个很难，没有明确的任务。）

我可以提供相似的例子。在某些方面，`Go` 可能比这些语言更简单，有些则不是那么多...大致上我会说它和其他常用语言的平均差不多。我也不认为简单，无论是感觉上还是实际使用中，在一天结束时真的是非常重要的。我不这么认为。

最后，这篇文章从哪里来，作者吗？我不肯定。我还不知道`Go` 是否会在我的日常工作中被选为一个（子）项目，或者我是否可能将它用于兴趣爱好项目。我想避免推动本文提到的那种教条的社区的一部分。有没有意识面向`Go` 的地方呢？大家可以随意就此提出建议。

我和`Rust` 社区有同样的问题，请不要介意，我也知道离开那些更狂热的支持者会更好。 （Q：“你能否在`Rust` 重写你的项目？”A：“迷失了”）也许这就是这些新语言的性质，以及他们为激励人们如此激励阳光的争斗。

----------------

via: https://ewanvalentine.io/microservices-in-golang-part-3/

作者：[Ewan Valentine](http://ewanvalentine.io/author/ewan)
译者：[deadvia](https://github.com/deadvia)
校对：[校对者ID](https://github.com/校对者ID)

本文由 [GCTT](https://github.com/studygolang/GCTT) 原创编译，[Go 中文网](https://studygolang.com/) 荣誉推出