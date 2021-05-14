#【Kotlin】抽象类 ( 声明 | 抽象类成员 | 抽象类继承 | 抽象方法覆盖 | 抽象方法实现 )


## I . 抽象类总结

抽象类总结 :

① 声明 : 抽象类中使用 abstract 声明 ;

② 成员 : 抽象类中既可以定义正常属性和方法 , 又可以定义抽象的属性和方法 ;

③ 继承 : 抽象类可以继承抽象类 , 抽象类也可以继承正常类 , 正常类可以继承抽象类 ;

④ 重写 : 抽象类中可以使用抽象方法重写正常方法 , 也可以进行正常的方法重写 ;

⑤ 特征 : 抽象方法只能定义在抽象类中 , 正常类中不能有抽象方法 ;



## II . 抽象类声明

1 . 抽象类简介 : 抽象类不能被实例化 , 在 class 关键字前使用 abstract 修饰 ;


① 抽象类默认 open 修饰 : 抽象类 , 默认使用 open 关键字修饰 , 可以直接继承 ;

② 抽象方法默认 open 修饰 : 抽象方法 , 默认使用 open 关键字修饰 , 可以直接 override 重写 ;

```kotlin
//使用 abstract 修饰抽象类 
abstract class Student {
}
```


## III . 抽象类中的 ( 正常 / 抽象 ) 的 ( 成员 / 方法 )

0 . 抽象类内成员总结 : 抽象类中可以定义正常的成员和方法 , 也可以定义抽象的成员和方法 ;


1 . 定义正常的属性和方法 : 抽象类中可以定义正常的 成员属性 和 成员方法 ;


① 正常成员属性 : 该成员属性可以是常量 , 也可以是变量 ;

② 正常成员方法 : 正常的方法 , 定义有方法体 ; 如果函数有方法体 , 不能声明为抽象方法 ;

```kotlin
abstract class Student {
    //抽象类中定义普通常量
    val name: String = "Tom"

    //抽象类中定义普通变量
    var age: Int = 18

    //抽象类中定义正常方法
    fun say(){
        println("姓名 : ${name} , 年龄 : ${age}")
    }
}
```

3 . 定义抽象的属性和方法 : 抽象类中可以定义抽象的 成员属性 和 成员方法 ;


① 抽象属性 : 被 abstract 修饰的 常量 var 或 变量 val 属性 , 没有初始化值 , 没有 getter 和 setter 方法 ;

```kotlin
abstract class Student {
    //抽象类中定义抽象常量 , 没有初始值 , 没有 get set 方法
    abstract val name: String

    //抽象类中定义抽象变量 , 没有初始值 , 没有 get set 方法
    abstract var age: Int
}
```

② 抽象方法 : 使用 abstract 修饰的方法 , 没有方法体 ; 如果函数有方法体 , 不能声明为抽象方法 ; 如果类中有抽象函数 , 该类必须声明成抽象类 ;

```kotlin
abstract class Student {
    //抽象类中定义抽象方法 , 没有方法体
    abstract fun say()
}
```


## IV . 抽象类继承

1 . 抽象类可以继承抽象类 :


```kotlin
abstract class Father{
}

//抽象类可以继承抽象类
abstract class Son : Father() {
}
```
2 . 抽象类可以继承正常类 : 该正常类必须使用 open 修饰 ;

```kotlin
open class Father{
}

//抽象类可以继承正常类 , 该正常类必须使用 open 修饰
abstract class Son : Father() {
}
```

## V . 抽象方法的覆盖

1 . 抽象方法覆盖 : 父类的正常的方法 , 可以在子类中使用抽象方法进行覆盖 ;


① 注意父类方法的 open 修饰符 : 抽象类中的正常方法 , 如果想要在子类中设置可以被重写 , 需要使用 open 修饰 ;

② 抽象函数与正常函数的继承 : <font color = "red">其抽象函数默认使用 open 修饰 , 可以直接重写 , 正常函数需要使用 open 修饰才能被 override 重写 ;</font>


2 . 将正常函数覆盖成抽象函数 : 将 Father 类的 open 改成 abstract 也是可以的 , 覆盖操作仍能成立 ;

```kotlin
//该类可以是正常类 , 也可以是抽象类
//  此处的示例是正常类 , 将 open 改成 abstract 也成立
open class Father{
    open fun action(){ println("Father")}
}

//抽象类可以继承正常类 , 该正常类必须使用 open 修饰
abstract class Son : Father() {
    override abstract fun action()
}
```
3 . 将正常函数覆盖成正常函数 : 正常函数都可以被覆盖成抽象函数 , 那么正常函数的正常覆盖 , 也可以进行 ;   
将 Father 类的 open 改成 abstract 也是可以的 , 覆盖操作仍能成立 ;

```kotlin
//该类可以是正常类 , 也可以是抽象类
//  此处的示例是正常类 , 将 open 改成 abstract 也成立
open class Father{
    open fun action(){ println("Father")}
}

//抽象类可以继承正常类 , 该正常类必须使用 open 修饰
abstract class Son : Father() {
    //也可以将其重写成正常函数
    override fun action(){ println("Father") }
}
```


## VI . 抽象方法的实现

抽象方法实现 :


① 正常类子类 : 正常的类继承抽象类必须实现 abstract 抽象方法 ;

```kotlin
abstract class Father{
    abstract fun action()
}

//正常类继承抽象类 , 必须实现抽象类中的抽象方法
class Son : Father() {
    override fun action() {
        println("正常类继承抽象类 , 必须实现抽象类中的抽象方法")
    }
}
```

② 抽象类子类 : 如果抽象类继承抽象类 , 可以不实现父累抽象方法 ;

```kotlin
abstract class Father{
    abstract fun action()
}

//抽象类继承抽象类 , 可以不实现抽象方法
abstract class Son : Father() {
}
```