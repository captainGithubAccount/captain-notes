# 变量

<font color = "blue">val a--> final a</font>  
<font color = "blue">var a--> 非final</font>  
<font color = "blue">const val a-->static final a</font>

```
没加const的时候，采用getter获取属性，对于顶级属性和object里定义的属性调用方法还略有不同:

top-lelve属性没加const时，直接是在编译后的java类名下调用getter。
而object和company object里面的属性没加const时，要通过实例去调用getter。
```

变量可以很简单地定义成可变(`var`)和不可变（`val`）的变量。这个与Java中使用的`final`很相似。但是__不可变__在Kotlin（和其它很多现代语言）中是一个很重要的概念。

一个不可变对象意味着它在实例化之后就不能再去改变它的状态了。如果你需要一个这个对象修改之后的版本，那就会再创建一个新的对象。这个让编程更加具有健壮性和预估性。在Java中，大部分的对象是可变的，那就意味着任何可以访问它这个对象的代码都可以去修改它，从而影响整个程序的其它地方。

不可变对象也可以说是线程安全的，因为它们无法去改变，也不需要去定义访问控制，因为所有线程访问到的对象都是同一个。

所以在Kotlin中，如果我们想使用不可变性，我们编码时思考的方式需要有一些改变。__一个重要的概念是：尽可能地使用`val`__。除了个别情况（特别是在Android中，有很多类我们是不会去直接调用构造函数的），大多数时候是可以的。

之前提到的另一件事是我们通常不需要去指明类的类型，它会自动从后面分配的语句中推断出来，这样可以让代码更加清晰和快速修改。我们在前面已经有了一些例子：

```kotlin
val s = "Example" // A String
val i = 23 // An Int
val actionBar = supportActionBar // An ActionBar in an Activity context
```

如果我们需要使用更多的范型类型，则需要指定：

```kotlin
val a: Any = 23
val c: Context = activity
```
