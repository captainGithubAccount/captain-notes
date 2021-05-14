# Kotlin学习系列——双冒号 :: 使用
> 通俗来讲就是引用一个方法

Kotlin 中 双冒号操作符 表示把一个方法当做一个参数，传递到另一个方法中进行使用，通俗的来讲就是引用一个方法。先来看一下例子：

```kotlin
fun main(args: Array<String>) {
    println(lock("param1", "param2", ::getResult))
}

/**
 * @param str1 参数1
 * @param str2 参数2
 */
fun getResult(str1: String, str2: String): String = "result is {$str1 , $str2}"

/**
 * @param p1 参数1
 * @param p2 参数2
 * @param method 方法名称
 */
fun lock(p1: String, p2: String, method: (str1: String, str2: String) -> String): String {
    return method(p1, p2)
}
```
这里需要注意的是，lock 函数 的第三个参数传入 method 时，要确定参数个数、类型、返回值都和其形参一致。

输出结果:

```kotlin
result is {param1 , param2}
```
如果我们需要调用其他 Class 中的某一个方法是：
写法为：

```kotlin
fun main(args: Array<String>) {
    var d = Test()
    println(lock("param1", "param2", d::getResult))
}
``` 

我们在 Class 中的某个方法中使用双冒号调用当前 Class 的内部方法时调动方式为：

```kotlin
class Test1 {
    fun isOdd(x: Int) = x % 2 != 0

    fun test() {
        var list = listOf(1, 2, 3, 4, 5)
        println(list.filter(this::isOdd))
    }
}
``` 

一般情况，我们调用当前类的方法 this 都是可省略的，这里之所以不可省略的原因是

```kotlin
为了防止作用域混淆 ， :: 调用的函数如果是类的成员函数或者是扩展函数，必须使用限定符,比如this
```

如果把 isOdd 写到 class 外部 (全局) 这里也是可以省略限定符。



<h3><font color = "red">函数式编程的高级进阶</font></h3>

<font color = "blue">定义</font>：一个用函数作为参数或者返回值的函数  
<font color = "blue">如何定义</font>：()->Unit 括号里面代表函数的参数，箭头后面代表函数的返回值。  
传递一个函数，或要将这个函数赋值给一个变量的时候，需要在函数前面加双冒号。  
这个双冒号的写法，叫`函数引用`Function Reference  
<font color = "blue">加了两个冒号，这个函数才变成了一个对象。</font>  
在kotlin里 [ 函数可以作为参数 ] 这件事的本质是函数可以作为对象存在。  
因为<font color = "blue">只有是对象才可以被作为参数传递。</font>  
<font color = "blue">kotlin中函数就是函数，不是对象。</font>  
kotlin选择创建一个和函数具有相同功能的对象（用双冒号）。  
一个指向对象的引用。  
<font color = "blue">这个对象不是函数本身，而是一个和这个函数具有相同功能的对象。</font>  
怎么相同？你可以怎么用这个函数，就可以怎么用它（加了双冒号的对  象）。  
<font color = "red">只有函数类型的对象，才能调用invoke</font>（在函数对象后面直接加括号是kotlin的语法糖）。  
函数就是函数，它和对象是两个维度的东西。  
<font color = "blue">双冒号表达的是它是一个指向对象的引用，而不是指向函数本身。</font>  
而是指向一个我们在代码中看不见的对象。  
这个对象复制了原函数的功能。  

```kotlin
fun a(params: (Int) -> String) {
    println("aaa")
}

fun b(int: Int): String {
    return "acb"
}

fun main() {
    a(::b)
    val c = ::b
    c.invoke(1)
    c(2)
}
```
除了用双冒号引用，还可以直接把函数挪过来写  
这种写法叫匿名函数  
注：d不是函数的名字，而是变量的名字，指向这个匿名函数类型的对象。  

```kotlin
val d = fun(param: Int): String {
    return param.toString()
}

val z : (Int)->String = {
     it.toString()
}

val y: () -> Unit = {
    println("hahaha")
}

val w = {
    println("???")
}
```
如果Lambda是函数的最后一个参数，可以把lambda写在括号外面，  
而如果lambda是函数唯一的参数，可以把参数省略，用it指代这个参数  
lambda的返回值不是用return，而是取最后一行代码的值  

<font color = "red">kotlin的匿名函数其实不是函数，而是个对象，它和（::+函数名）是一个东西。  
同理Lambda也是一个函数类型的对象。</font>  

