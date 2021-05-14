2.2、Lambda语法
为了让大家彻底的弄明白Lambda语法，我这里用三种用法来讲解。并且举例为大家说明

语法如下：

```kotlin
    //1. 无参数的情况 ：
    val/var 变量名 = { 操作的代码 }

    //2. 有参数的情况
    val/var 变量名 : (参数的类型，参数类型，...) -> 返回值类型 = {参数1，参数2，... -> 操作参数的代码 }

    可等价于
    // 此种写法：即表达式的返回值类型会根据操作的代码自推导出来。
    val/var 变量名 = { 参数1 ： 类型，参数2 : 类型, ... -> 操作参数的代码 }

    3. lambda表达式作为函数中的参数的时候，这里举一个例子：
    fun test(a : Int, 参数名 : (参数1 ： 类型，参数2 : 类型, ... ) -> 表达式返回类型){
        ...
    }
```      

* 无参数的情况

```kotlin
    // 源代码
   fun test(){ println("无参数") }
  
    // lambda代码
    val test = { println("无参数") }

    // 调用
    test()  => 结果为：无参数
```
* 有参数的情况,这里举例一个两个参数的例子，目的只为大家演示

```kotlin
    // 源代码
    fun test(a : Int , b : Int) : Int{
        return a + b
    }

    // lambda
    val test : (Int , Int) -> Int = {a , b -> a + b}
    // 或者
    val test = {a : Int , b : Int -> a + b}
    
    // 调用
    test(3,5) => 结果为：8
```
* lambda表达式作为函数中的参数的时候

```kotlin
    // 源代码
    fun test(a : Int , b : Int) : Int{
        return a + b
    }

    fun sum(num1 : Int , num2 : Int) : Int{
        return num1 + num2
    }

    // 调用
    test(10,sum(3,5)) // 结果为：18

    // lambda
    fun test(a : Int , b : (num1 : Int , num2 : Int) -> Int) : Int{
        return a + b.invoke(3,5)
    }

    // 调用
    test(10,{ num1: Int, num2: Int ->  num1 + num2 })  // 结果为：18
```  
        
