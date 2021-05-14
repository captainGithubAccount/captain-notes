# koin
> https://insert-koin.io/docs/quickstart/kotlin
>> [点击跳转koin官网](https://insert-koin.io/docs/quickstart/kotlin)

依赖注入框架(原理): 为了解决类与类之间的依赖问题,通过依赖反转来达到解耦的目的(实现原理A类里面加载C类，C类里面某个方法可以生成B类，这样A就不需要通过构造方法或者set方法传入B类，所以不用依赖B类，可以通过C类拿到B类，从而使用B类的方法,达到A类与B类的解耦)
## 一、koin的环境配置


```kotlin
//project -> build.gradle
// Add Maven Central to your repositories if needed
repositories {
    mavenCentral()    
}

//common module -> build.gradle
dependencies {
    // Koin for Android
    compile "org.koin:koin-android:$koin_version"
}
```

## 二、koin的简单使用步骤
### 1、业务class的创建

### 2、定义koin的容器模块module，声明内部类的创建(单例，工厂等)


### 3、在Application调用startKoin内部初始化modules

## 三、使用koin框架注入单例
> https://insert-koin.io/docs/quickstart/android
>> [点击跳转koin官网](https://insert-koin.io/docs/quickstart/android)

### 1、module的创建
kt文件的顶层声明即可,不需要放到类里面声明

```kotlin
val appModule = module {

    // 方式一:single instance of HelloRepository
    single<HelloRepository> { HelloRepositoryImpl() }

	//方式二:通过参数决定是否懒加载
	single(createdAtStart = false){ HelloRepositoryImpl() }
	//@param createdAtStart false：为懒加载 true: 非懒加载的直接创建
	
	
    // Simple Presenter Factory
    factory { MySimplePresenter(get()) }
}
```
### 2、Application中配置module
BaseApplication中声明

```kotlin
class MyApplication : Application(){
    override fun onCreate() {
        super.onCreate()
        // Start Koin
        startKoin{
            androidLogger()
            androidContext(this@MyApplication)
            modules(appModule)
        }
    }
}
```
### 3、类里面注入加载对象
需要用到ViewModel对象的类里面声明  

<font color = "blue">INFO</font>  

* The by viewModel() function allows us to retrieve a ViewModel instance from Koin, linked to the Android ViewModelFactory.

* The getViewModel() function is here to retrieve directly an instance (non lazy)

#### 方式一: 通过by viewModel()懒加载方式拿到对象

```kotlin
class MyViewModelActivity : AppCompatActivity() {
    //module方式一的获取单例写法
    // Lazy Inject ViewModel,懒加载注入ViewModel实例,告别传统的获取ViewModel实例的方式
    val myViewModel: MyViewModel by viewModel()

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_simple)

        //...
    }
}
```
#### 方式二:通过getViewModel()非懒加载方式拿到对象

```kotlin
class MyViewModelActivity : AppCompatActivity() {
    //module方式一的获取单例写法二
    // non Lazy Inject ViewModel,非懒加载注入框架ViewModel的实例,告别传统的获取ViewModel实例的方式
    val myViewModel: MyViewModel = getViewModel<MyViewModel>()

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_simple)

        //...
    }
}
```
## 四、Koin结合ViewModel注入ViewModel实例
> https://insert-koin.io/docs/quickstart/android-viewmodel
>> [点击跳转koin官网](https://insert-koin.io/docs/quickstart/android-viewmodel) 

> https://insert-koin.io/docs/reference/koin-android/viewmodel
>> [点击跳转koin官网](https://insert-koin.io/docs/reference/koin-android/viewmodel)

### 1、module的创建
kt文件的顶层声明即可,不需要放到类里面声明

```kotlin
val appModule = module {

    // single instance of HelloRepository
    single<HelloRepository> { HelloRepositoryImpl() }

    // MyViewModel ViewModel
    viewModel { MyViewModel(get()) }
}
```
### 2、Application中配置module
BaseApplication中声明

```kotlin
class MyApplication : Application(){
    override fun onCreate() {
        super.onCreate()
        // Start Koin
        startKoin{
            androidLogger()
            androidContext(this@MyApplication)
            modules(appModule)
           	//配置module
        }
    }
}
```
### 3、类里面注入加载对象
需要用到ViewModel对象的类里面声明  

<font color = "blue">INFO</font>  

* The by viewModel() function allows us to retrieve a ViewModel instance from Koin, linked to the Android ViewModelFactory.

* The getViewModel() function is here to retrieve directly an instance (non lazy)

#### 方式一: 通过by viewModel()懒加载方式拿到对象

```kotlin
class MyViewModelActivity : AppCompatActivity() {
    
    // Lazy Inject ViewModel,懒加载注入ViewModel实例,告别传统的获取ViewModel实例的方式
    val myViewModel: MyViewModel by viewModel()

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_simple)

        //...
    }
}
```
#### 方式二:通过getViewModel()非懒加载方式拿到对象

```kotlin
class MyViewModelActivity : AppCompatActivity() {
    
    // non Lazy Inject ViewModel,非懒加载注入框架ViewModel的实例,告别传统的获取ViewModel实例的方式
    val myViewModel: MyViewModel = getViewModel<MyViewModel>()

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_simple)

        //...
    }
}
```
## 五、Koin结合Factory(工厂类设计模式)注入对象

> https://insert-koin.io/docs/reference/koin-android/get-instances
>> [点击跳转kotlin官网](https://insert-koin.io/docs/reference/koin-android/get-instances)

### 1、module的创建
kt文件的顶层声明即可,不需要放到类里面声明

```kotlin
val appModule = module {
	single{ Presenter()}
	
    // 方式一
    factory { Presenter() }
    
    //方式一，特定条件下的写法
    factory(override = true) { Presenter() }
    //override = true是当module了里面已经存在了创建Presenter实例如上面的single{ Presenter()}，若不标识(即override = true)则编译报错

    // MyViewModel ViewModel
    viewModel { MyViewModel(get()) }
}
```
### 2、Application中配置module
BaseApplication中声明

```kotlin
class MyApplication : Application(){
    override fun onCreate() {
        super.onCreate()
        // Start Koin
        startKoin{
            androidLogger()
            androidContext(this@MyApplication)
            modules(appModule)
           	//配置module
        }
    }
}
```
### 3、类里面注入加载对象
需要用到ViewModel对象的类里面声明  

<font color = "blue">INFO</font>  

* The by viewModel() function allows us to retrieve a ViewModel instance from Koin, linked to the Android ViewModelFactory.

* The getViewModel() function is here to retrieve directly an instance (non lazy)

#### 方式一: 通过by viewModel()懒加载方式拿到对象

```kotlin
class MyViewModelActivity : AppCompatActivity() {
    //module方式一的获取单例写法
    // Lazy Inject ViewModel,懒加载注入ViewModel实例,告别传统的获取ViewModel实例的方式
    val myViewModel: MyViewModel by viewModel()

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_simple)

        //...
    }
}
```
#### 方式二:通过getViewModel()非懒加载方式拿到对象

```kotlin
class MyViewModelActivity : AppCompatActivity() {
    //module方式一的获取单例写法二
    // non Lazy Inject ViewModel,非懒加载注入框架ViewModel的实例,告别传统的获取ViewModel实例的方式
    val myViewModel: MyViewModel = getViewModel<MyViewModel>()

    override fun onCreate(savedInstanceState: Bundle?) {
        super.onCreate(savedInstanceState)
        setContentView(R.layout.activity_simple)

        //...
    }
}
```
