Android使用Gradle依赖配置compile、implementation与api的区别介绍



AndroidStudio升级到3.0之后，gradle版本也随之升级到了3.0.0版本。

当gradle插件升级到3.0.0及以上后，我们会发现在gradle中添加依赖的时候，会推荐你使用implementation或者api，而不再推荐你使用compile，今天就来简单介绍下这两者的使用与区别！



```kotlin
classpath 'com.android.tools.build:gradle:3.0.0'
```

在新建一个Android工程的时候，build.gradle中的依赖默认为implementation，而不是之前的compile。另外，gradle 3.0.0版本以上，还有依赖指令api。本文主要介绍下implementation和api的区别。

新建工程默认生成的app的build.gradle文件中的依赖：

```kotlin
dependencies {

 implementation fileTree(include: ['*.jar'], dir: 'libs')

 implementation 'com.android.support:appcompat-v7:26.1.0'

 implementation 'com.android.support.constraint:constraint-layout:1.0.2' 

 testImplementation 'junit:junit:4.12'

 androidTestImplementation 'com.android.support.test:runner:1.0.1'

 androidTestImplementation 'com.android.support.test.espresso:espresso-core:3.0.1'

}
```

api 指令

完全等同于compile指令，没区别，你将所有的compile改成api，完全没有错。

implementation指令

这个指令的特点就是，对于使用了该命令编译的依赖，对该项目有依赖的项目将无法访问到使用该命令编译的依赖中的任何程序，也就是将该依赖隐藏在内部，而不对外部公开。

简单的说，就是使用implementation指令的依赖不会传递。例如，有一个module为testLib，testLib依赖于Glide：


```kotlin
implementation 'com.github.bumptech.glide:glide:3.8.0'
```
这时候，在testsdk里边的java代码是可以访问Glide的。

另一个module为app，app依赖于testLib：

```kotlin
implementation project(':testLib')
```
这时候，因为testsdk使用的是implementation 指令来依赖Glide，所以app里边不能引用Glide。

但是，如果testLib使用的是api来引用Glide：


```kotlin
api 'com.github.bumptech.glide:glide:3.8.0'
```
则与gradle3.0.0之前的compile指令的效果完全一样，app的module也可以引用Glide，这就是api和implementation的区别。

建议

compile在3.x版本的gradle中已被废弃，将在2018年底，被google移除，所以不要使用compile了
依赖首先应该设置为implementation，如果没有错误，那就用implementation ，如果有错，那么使用api指令
