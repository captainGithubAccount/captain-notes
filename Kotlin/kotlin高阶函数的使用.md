## kotlin高阶函数的使用. 


### 1、foreach函数

```kotlin
fun main(args: Array<String>) {
    var list = listOf(1, 2, 3, 4, 5, 6)
    list.forEach(::println)

    val newList = arrayListOf<String>() --->1,2,3,4,5,6

    list.forEach {
        newList.add((it * 2).toString()) --->2,4,6,8,10,12
    }
    
    newList.forEach(::println)
}

```
		
### 2、map函数 &emsp; &emsp; &emsp; flatMap函数flatMap是一种支持二维集合映射的高阶函数

map:

```kotlin
fun main(args: Array<String>) {
    val list = listOf(1, 2, 3, 4, 5, 6)

    val newList = list.map {
        //对集合中的数据进行操作，然后赋值给新的集合
        (it * 2).toString()
    }.forEach(::println) //2 4 6 8 10 12

    val doubleList = list.map {
        it.toDouble()
    }.forEach(::print) //1.0 2.0 3.0 4.0 5.0 6.0
    //函数作为参数的第二种方式调用 类名::方法名
    val doubleList2 = list.map(Int::toDouble).forEach(::print) 1.0 2.0 3.0 4.0 5.0 6.0

}

```

flatMap:

```kotlin
val arr = intArrayOf(1, 2, 4, 6)
val arr2 = intArrayOf(10, 39, 39, 18, 88)
var arr3 = intArrayOf(100, 200, 383, 198)

val newArr = arrayListOf(arr, arr2, arr3)
val flatArr = newArr.flatMap {
    iterator -> iterator.map {
        it.toString()
    }
}

// 输出结果
// [1, 2, 4, 6, 10, 39, 39, 18, 88, 100, 200, 383, 198]

```
### 3、reduce ，fold，foldRight (倒序), joinToString 

```kotlin
fun main(args: Array<String>) {
    val list = arrayOf(
        1..5,
        2..3
    )

    val newList = list.flatMap {
        it
    }
    //1 , 2 , 3 , 4 , 5 , 50 , 51 , 52 , 53 , 54 , 55 ,
    newList.forEach { print("$it , ") }

    //求和 reduce 返回值必须是 acc类型
    println(newList.reduce { acc, i -> acc + i }) //20

    //带基数求和
    println(newList.fold(10) { acc, i -> acc + i }) //30


    //fold 返回值类型是 "基数" 对应的类型,比如 StringBuilder hello--1--2--3--4--5--2--3--
    println(newList.fold(StringBuilder("hello--")) { acc, i -> acc.append(i).append("--") }) //30

    //拼接字符串 1---, 2---, 3---, 4---, 5---, 2---, 3---
    println(newList.joinToString { "$it---" })
    
}

```

### 4、filter函数(筛选)&emsp; &emsp; &emsp; &emsp; filterIndexed函数(下标筛选)

```kotlin
fun main(args: Array<String>) {
    val list = arrayOf(
        1..5,
        2..3
    )
    val newList = list.flatMap {
        it
    }
    //筛选 集合中数据 > 2的item
    val filterList = newList.filter { it > 2 }
    filterList.forEach(::print) //3453
    //筛选 集合中下标是奇数item
    val filterIndexList = newList.filterIndexed { index, i -> index % 2 == 0; }
    filterIndexList.forEach { print(it) } //1 3 5 3
}

```

### 5、 takeWhile函数(截至条件)

```koltin
fun main(args: Array<String>) {
    val list = arrayOf(
        1..5,
        2..3
    )
    val newList = list.flatMap {
        it
    }
    //截取符合条件的前面的所以的item 1234523，< 3 ，12
   // newList.takeWhile { it < 3 }.forEach { print(it) } // 1 2

    //返回包含 最后[n]元素 的列表。，包含最后2个元素
    newList.takeLast(2).forEach(::print) // 23
}

```
### 6、?. 判空执行，let 类作为参数，apply 类扩展

```kotlin
fun main(args: Array<String>) {
    val person = getPerson()
    println(person?.name) //判空处理，如果不为空 执行后面的方法

    person?.let { //类作为参数(即对这个类对象进行操作) it
        println(it.name)
        println(it.age)
        it.work()
    }

    person?.apply { //类扩展 可以直接调用
        println(name)
        println(age)
        work()
    }
}

fun getPerson(): Person? {
    return Person("shadow", 18)
}

class Person(val name: String, val age: Int) {
    fun work() {
        println("hello shadow")
    }
}

```
### 7、with
####定义：fun <T, R> with(receiver: T, block: T.() -> R): R功能：将对象作为函数的参数，在函数内可以通过 this指代该对象。返回值为函数的最后一行或return表达式。(注意与apply很像，但是apply是用来调用的，with是用来传的)

```kotlin
fun main(args: Array<String>) {
    val br = BufferedReader(FileReader("shadow.txt"))
    br.readLine()
    br.read()
    //使用给定的[receiver]调用指定的函数[block]并返回其结果。
   /* with(br) {
        var readLine: String?
        while (true) {
            readLine = readLine() ?: break //如果不为空 就执行前面的表达式 否则执行后面的表达式
            println(readLine)
        }
        close()
    }*/
}

```

### 10、 use函数
#### use函数会自动关闭调用者（无论中间是否出现异常&emsp;Kotlin的File对象和IO流操作变得行云流水&emsp;，use函数内部实现也是通过try-catch-finally块捕捉的方式，所以不用担心会有异常抛出导致程序退出 close操作在finally里面执行，所以无论是正常结束还是出现异常，都能正确关闭调用者


```kotlin
  BufferedReader(FileReader("build.gradle")).use {
        var readLine: String?
        while (true) {
            readLine = readLine() ?: break //如果不为空 就执行前面的表达式 否则执行后面的表达式
            println(readLine)
        }
    }

```
### 11、图解

| 函数名 | 定义inline的结构	| 函数体内使用的对象 |	返回值 | 是否是扩展函数 | 适用的场景 |
| :---: | :---: | :---: | :---: | :---: |:---: |
|let	|fun <T, R> T.let(block: (T) -> R): R = block(this)|	it指代当前对象|	闭包形式返回|	是	|适用于处理不为null的操作场景|
|with|	fun <T, R> with(receiver: T, block: T.() -> R): R = receiver.block()|	this指代当前对象或者省略	|闭包形式返回	|否	|适用于调用同一个类的多个方法时，可以省去类名重复，直接调用类的方法即可，经常用于Android中RecyclerView中onBinderViewHolder中，数据model的属性映射到UI上|
run	|fun<T, R> T.run(block: T.() -> R): R = block()	|this指代当前对象或者省略|	闭包形式返回|	是	|适用于let,with函数任何场景。|
apply|	fun T.apply(block: T.() -> Unit): T { block(); return this }|	this指代当前对象或者省略|	返回this	|是|	1、适用于run函数的任何场景，一般用于初始化一个对象实例的时候，操作对象属性，并最终返回这个对象.2、动态inflate出一个XML的View的时候需要给View绑定数据也会用到.3、一般可用于多个扩展函数链式调用4、数据model多层级包裹判空处理的问题|
also	|fun T.also(block: (T) -> Unit): T { block(this); return this }|	it指代当前对象|	返回this	|是|	适用于let函数的任何场景，一般可用于多个扩展函数链式调用|
### 12、区别

> 在Kotlin中有几个十分相似的标准库函数，他们之间也有一些差异，如果使用不当可能回得到与预期相反的效果，所以我们来简短的区分一下let、also、run、with、apply 这5个标准库函数的区别。 Kotlin提供了这几种标准域函数主要是为了简化一些操作，让代码看起来更加的简洁，可读性更好。

在最开始我们先创建一个简单的Book类，作为例子我们来看看每种函数的不同

```kotlin
data class Book(var name: String, var author: String, var price: String){
  fun adjust( value: Int){
    price = price.plus(value)
  }
}
fun main(){
}
```

上述是一个非常简单的Book类，包括三个属性：书名、作者、价格。然后有一个调整价格的方法。


* <font color = "blue" size = 4>let</font>

```kotlin
Book("《海边的卡夫卡》", "村上春树", 59).let {
    println(it)
    it.adjust(-5)  //let的参数为it，也就是自身
    println(it)
  }
```
复制代码
在Book类的main函数中添加上述代码，并且运行，结果如下:

```
Book(name=《海边的卡夫卡》, author=村上春树, price=59) Book(name=《海边的卡夫卡》, author=村上春树, price=54)
```

在上述代码中，我们可以看到<strong>let的参数为自身，即：block: .(T)，将自身作为参数传递。</strong>

* <font color = "blue" size = 4>run</font>
如果我们要用run函数实现与let一样的功能，应该是这样的：

```kotlin
Book("《海边的卡夫卡》", "村上春树", 59).run {
    println(this)
    this.adjust(-5)
    println(this)
  }
```

<strong>可以看出来，run更像是Book对象的扩展函数，即：block: T.()。他是将this作为参数传递，在大多数情况下this可以被省略，因此我们可以更加关注内部实现。</strong>

* <font color = "blue" size = 4>with</font>
同样的，如果要实现上述目的，我们使用with应该是这样的：

```kotlin
with(Book("《海边的卡夫卡》", "村上春树", 59)){
    println(this)
    this.adjust(-5)
    println(this)
  }
```

这里要说明的一点是，<strong>with与其余4个库函数最大的不同就在于with不是一个扩展函数。with是一个普通函数</strong>，那么如果我们在with中传递了一个可为空的参数时，with函数将会变成：

```kotlin
val book: Book? = Book("《海边的卡夫卡》", "村上春树", 59) 
  with(book){
    println(this)
    this!!.adjust(-5)    //将空判断放在了with方法内部
    println(this)
  }
``` 
 

可以看到我们是将空判断放在了with内部，显然这样不是一个非常好的实现，如果我们使用run，就可以很方便的解决这个问题：

```kotlin
val book: Book? = Book("《海边的卡夫卡》", "村上春树", 59)
book?.run{
    println(this)
    this.adjust(-5)
    println(this)
  }
```

* <font color = "blue" size = 4>also</font>
上面我们说到了，<strong>let与run的区别就在于传递的参数不同，那么let与also的区别就在于返回值的不同，他们的参数都是it，但是let返回的是lamda表达式的结果。而also返回的是上下文，即：this。</strong> 我们看一下下面的代码。

```kotlin
Book("《海边的卡夫卡》", "村上春树", 59)
  .let {
    println(it)
    it.adjust(-5)   
    it  			//因为adjust()方法没有返回值，我们需要将调整价格后的Book对象作为lamda表达式的返回值返回
  }
  .let {
    print(it)
  }
 
Book("《海边的卡夫卡》", "村上春树", 59)
  .also {
    println(it)
    it.adjust(-5)			// 由于also直接返回当前对象，所以我们不用再提供返回值
  }
  .let {
    print(it)
  }
```

上述两段代码都输出：

```
Book(name=《海边的卡夫卡》, author=村上春树, price=59) Book(name=《海边的卡夫卡》, author=村上春树, price=54)
```

如果我们将第一段代码中的第一个let{}中最后一个it返回值去掉，则会输出：

```
Book(name=《海边的卡夫卡》, author=村上春树, price=59)
Kotlin Unit
```

可以看到，<strong>let输出的是lamda表达式的值，而also的返回值是this. </strong>通过also与let的配合，我们可以写出一些可读性更强的链式调用的语句。

* <font color = "blue" size = 4>apply</font>

<strong>对于apply函数来说，传递的参数是this， 返回值也是this。当然apply还有另一个作用，就是可以轻松的实现Builder模式</strong>(这里我们使用另一个对象Persion)：

```kotlin
Persion().apply{
    name = "小明"
    age = "13"
    brithday = "2000-01-01"
}
```


