# Kotlin by 关键字详解

委托模式已已经证明是实现继承的一个很好的替代方式

Kotlin 中 by 就是用于实现委托的。

```kotlin
fun main(args: Array<String>) {
    val b =BaseImpl("base")
    Derived(b).print()
 
}
interface  Base{
    fun print()
}
class BaseImpl(val x :String):Base{
    override fun print()  = print(x)
 
}
class  Derived(b: Base) :Base by b
```
Derived 的父类列表中的by子句 会将b 存储Derived内部，并且编译器会生成所有b类型的方法

## 覆盖由委托实现的接口成员

```kotlin
fun main(args: Array<String>) {
    val b =BaseImpl("base")
    val derived = Derived(b)
    derived.printLine()//base----base
    derived.printMessage()//Derived
    println(derived.message)//Derived----
 
}
interface  Base{
    val message :String
    fun printMessage()
    fun printLine()
}
class BaseImpl(val x :String):Base{
    override val message: String="base----$x"
 
    override fun printMessage() = print(x)
 
    override fun printLine() = println(message)
 
}
class  Derived(b: Base) :Base by b{
    override val message: String="Derived----"
    override fun printMessage() = print("Derived")
}
```
Derived 可以重写方法，但是重写的成员不会在委托对象的成员中调用

## 属性委托  
属性委托的语法： val/var <属性名>: <类型> by <表达式>

属性委托不需要实现任何接口但是要重写setValue 和 getValue 方法

```kotlin 
class Delegate{
    operator fun getValue(thisRef: Any?, property: KProperty<*>): String {
        return "${thisRef?.javaClass}, thank you for delegating '${property.name}' to me!"
    }
 
    operator fun setValue(thisRef: Any?, property: KProperty<*>, value: String) {
        println("$value has been assigned to '${property.name}' in ${thisRef?.javaClass}.")
    }
}
 
 
fun main(args: Array<String>) {
    val example=Example()
    print(example.str)//class sample.xietaichen.koinsample.Example, thank you for delegating 'str' to me!
example.str="aaa"//aaa has been assigned to 'str' in sample.xietaichen.koinsample.Example@19469ea2.
}
class  Example{
    var str :String by Delegate()
}
```
当我们从委托到一个 Delegate实例的 str读取时，将调用Delegate中的 getValue() 函数， 所以它第一个参数是读出str的对象、第二个参数保存了对str自身的描述 （例如你可以取它的名字)。

<font size = 3 color = "blue">setValue 同理</font>

对于一个只读属性（即 val 声明的），委托必须提供一个名为 getValue 的函数，该函数接受以下参数：

* thisRef —— 必须与 属性所有者 类型（对于扩展属性——指被扩展的类型）相同或者是它的超类型；
* property —— 必须是类型 KProperty<*> 或其超类型。
这个函数必须返回与属性相同的类型（或其子类型）

对于一个可变属性（即 var 声明的），委托必须额外提供一个名为 setValue 的函数，该函数接受以下参数：

* thisRef —— 同 getValue()；
* property —— 同 getValue()；
* new value —— 必须与属性同类型或者是它的超类型。  

getValue() 或/与 setValue() 函数可以通过委托类的成员函数提供或者由扩展函数提供。 当你需要委托属性到原本未提供的这些函数的对象时后者会更便利。 两函数都需要用 operator 关键字来进行标记。

委托类可以实现包含所需 operator 方法的 ReadOnlyProperty 或 ReadWriteProperty 接口之一

```kotlin
interface ReadOnlyProperty<in R, out T> {
    operator fun getValue(thisRef: R, property: KProperty<*>): T
}
 
interface ReadWriteProperty<in R, T> {
    operator fun getValue(thisRef: R, property: KProperty<*>): T
    operator fun setValue(thisRef: R, property: KProperty<*>, value: T)
}
```

