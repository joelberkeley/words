# Languages

An exploration of languages of particular interest.

## Of fundamental interest

### [Idris](https://www.idris-lang.org/)

Idris is a purely functional language with dependent types and theorem proving. It shares these attributes with Agda, but is [designed for](http://docs.idris-lang.org/en/latest/faq/faq.html#what-are-the-differences-between-agda-and-idris) general purpose programming. It is inspired by Haskell, and uses much of the same syntax, but is written in C. As of 2021, Idris isn't ready for production deployment.

### [Rust](https://www.rust-lang.org/)

Rust gives the performance and memory profile of C, while guaranteeing memory and thread safety. It achieves this with an ownership memory model and its type system. It is often spoken of as having a steep learning curve, but I don't think this opinion is always justified. It simply enforces the rules you _should_ learn in languages like C, but often don't. Moreover, there are a number of ways of explicitly trading performance or safety for syntactic and conceptual simplicity.

Beyond the features of the language itself, Rust boasts an intuitive and reliable package manager, Cargo, as well as some of the [best learning resources](https://www.rust-lang.org/learn) around, such as [_the book_](https://doc.rust-lang.org/book/). I personally learnt Rust using a different book, [_Programming Rust_](http://shop.oreilly.com/product/0636920040385.do) by Blandy and Orendorff, which I consider the best programming book I've read.

### [Scala](https://www.scala-lang.org/)

Scala was the first language I explored in depth, following the excellent [_Programming in Scala_](https://www.artima.com/shop/programming_in_scala_4ed), as well as [_Functional Programming in Scala_](https://www.manning.com/books/functional-programming-in-scala) for the functional side. Scala is object-oriented with a very powerful type system, and supports both imperative and pure functional programming. It does this in an impressively coherent way (using [Amin et al.'s DOT calculus](https://infoscience.epfl.ch/record/215280), Scala 3's type system is [provably sound](https://dotty.epfl.ch/blog/2016/02/17/scaling-dot-soundness.html)). It encourages functional idioms, but allows imperative style to enable performant algorithms without sacrificing readability or comprehensibility. The ability to combine advanced FP and imperative constructs in a statically typed language makes Scala unique, though there are discussions in a number of other languages of achieving the same (e.g. in [Rust](https://github.com/rust-lang/rfcs/issues/324)).

A common feeling among developers I've spoken to is that Scala has too many features, too many ways of doing things, and that codebases can become a tangle of different styles and techniques. I wonder if the language may have been simpler, whilst retaining many of its advantages, if it wasn't object-oriented.

## Of circumstantial interest

### [Python](https://www.python.org/)

Python is the bread and butter of machine learning research, which is why I use it frequently. Python is great for prototyping and small projects: it's straightforward, flexible, and doesn't ask much of you, but when you need to build something that will make good use of hardware resources, or hold strong, unattended, under heavy usage, it's just not the right tool for the job.
