# Summary

#### [Introduction](README.md)
### [写在前面](xie_zai_qian_mian.md)
### [关于本书](guan_yu_ben_shu.md)
### [这本书适合你吗？](zhe_ben_shu_shi_he_ni_ma_ff1f.md)
### [关于作者](guan_yu_zuo_zhe.md)
### [介绍](jie_shao.md)

   * [什么是Kotlin？](shi_yao_shi_kotlin.md)
   * [我们通过Kotlin得到什么（数据类、扩展函数、？空安全）](wo_men_tong_guo_kotlin_de_dao_shi_yao.md)
   
   
### [准备工作](zhun_bei_gong_zuo.md)


   * [Android Studio](android_studio.md)
   * [安装Kotlin插件（Kotlin Android Extensions）](an_zhuang_kotlin_cha_jian.md)

   
### [创建一个新的项目](chuang_jian_yi_ge_xin_de_xiang_mu.md)

   * [在Android Studio中创建一个项目](zai_android_studio_zhong_chuang_jian_yi_ge_xiang_mu.md)
   * [配置Gradle（Anko库配置）](pei_zhi_gradle.md)
   * [把MainActivity转换成Kotlin代码](ba_mainactivity_zhuan_huan_cheng_kotlin_dai_ma.md)
   * [测试是否一切就绪（测试非findviewbyid方法）](ce_shi_shi_fou_yi_qie_jiu_xu.md)

   
### [类和函数](lei_he_han_shu.md)


   * [怎么定义一个类](zen_yao_ding_yi_yi_ge_lei.md)
   * [<font color = "blue">抽象类</font>](chou_xiang_lei.md)
   * [类继承(kotlin中的super()写法)](lei_ji_cheng.md)
   * [函数](han_shu.md)
   * [构造方法和函数参数（指定形参默认值、$）](gou_zao_fang_fa_he_han_shu_can_shu.md)
   * [<font color = "blue">构造函数详解</font>](gou_zao_detail.md)

   
### [编写你的第一个类](bian_xie_ni_de_di_yi_ge_lei.md)


   * [创建一个layout(as)](chuang_jian_yi_ge_layout.md)
   * [The Recycler Adapter（list）](the_recycler_adapter.md)

   
### [变量和属性（概念：一切皆对象）](bian_liang_he_shu_xing.md)


   * [基本类型（基本类型的转换: toInt、or、and、一个String可以像数组那样访问，并且被迭代）](ji_ben_lei_xing.md)
   * [变量(const)](bian_liang.md)
   * [属性（属性的get()和set()）](shu_xing.md)

   
### Anko和扩展的函数
   * [Anko是什么？](ankoshi_shi_yao_ff1f.md)
   * [开始使用Anko](kai_shi_shi_yong_anko.md)
   * [扩展函数](kuo_zhan_han_shu.md)

   
### 从API中获取数据
   * [执行一个请求（OpenWeatherMap API、readText()）](zhi_xing_yi_ge_qing_qiu.md)
   * [在主线程以外执行请求（async()）](zai_zhu_xian_cheng_yi_wai_zhi_xing_qing_qiu.md)

   
### [数据类](shu_ju_lei.md)


   * [额外的函数](e_wai_de_han_shu.md)
   * [复制一个数据类（使用copy()修改val()对象属性值）](fu_zhi_yi_ge_shu_ju_lei.md)
   * [映射对象到变量中（映射、in）](ying_she_dui_xiang_dao_bian_liang_zhong.md)

   
### 解析数据


   * [转换json到数据类（companion object {...}）](zhuan_huan_json_dao_shu_ju_lei.md)
   * [构建domain层（.map()、.format()、as别名）](gou_jiandomain_ceng.md)
   * [在UI中绘制数据（.with()）](zaiui_zhong_hui_zhi_shu_ju.md)

   
### [操作符重载](cao_zuo_fu_zhong_zai.md)


   * [--  !!  操作符表   !!  ---（操作符对应的方法，===、!==、.invoke()）](cao_zuo_fu_biao.md)
   * [<font color = "blue">双冒号的使用(::、invoke定义)</font>](shuang_mao_hao.md)
   * [例子（java与kotlin的list的区别以及kotlin的list常用操作）](li_zi.md)
   * [扩展函数中的操作符（github案例代码实现）](kuo_zhan_han_shu_zhong_de_cao_zuo_fu.md)

   
#### [使Forecast list可点击（init{}、invoke、.with()）](shi_forecast_list_ke_dian_ji.md)
### [Lambdas](lambdas.md)

   * [<font color = "blue">lambda用法详解</font>](lambda用法详解.md) 
   * [<font color = "red">简化setOnClickListener() （object对象表达式，创建一个匿名内部类、监听的lambda简化）</font>](jian_hua_setonclicklistener.md)
   * [<font color = "blue">object关键字详解</font>](object关键字详解.md)
   * [ForecastListAdapter的click listener（it）](forecastlistadapterde_click_listener.md)
   * [扩展语言（inline、泛型）](kuo_zhan_yu_yan.md)

   
### [可见性修饰符](ke_jian_xing_xiu_shi_fu.md)


   * [修饰符（internal）](xiu_shi_fu.md)
   * [构造器  （constructor）](gou_zao_qi.md)
   * [润色我们的代码](run_se_wo_men_de_dai_ma.md)

   
### [Kotlin Android Extensions](kotlin_android_extensions.md)


   * [怎么去使用Kotlin Android Extensions](zen_yaoqu_shi_yong_kotlinandroid_extensions.md)
   * [重构我们的代码（使用Kotlin Android Extensions demo）](zhong_gou_wo_men_de_dai_ma.md)

   
### [Application单例化和属性的Delegated](applicationdan_li_hua_he_shu_xing_de_delegated.md)


   * [Applicaton单例化（!!、饿汗式单例）](applicatondan_li_hua.md)
   * [委托属性](wei_tuo_shu_xing.md)
   * [<font color = "blue">by实现委托详解（by）</font>](委托_by关键字.md)
   * [标准委托（by lazy、Observable、.notNull()）](biao_zhun_wei_tuo.md)
   * [怎么去创建一个自定义的委托（?:）](zen_yao_qu_chuang_jian_yi_ge_zi_ding_yi_de_wei_tuo.md)
   * [<font color = "blue">复合符号图解（?. &emsp;&emsp; ?: &emsp;&emsp; as? &emsp;&emsp; !! &emsp;&emsp; ? &emsp;&emsp; ）</font>](复合符号.md)
   * [重新实现Application单例化（自定义委托demo）](zhong_xin_shixian_application_dan_li_hua.md)

   
### [创建一个SQLiteOpenHelper](chuang_jian_yi_ge_sqliteopenhelper.md)


   * [ManagedSqliteOpenHelper（.use{}）](managedsqliteopenhelper.md)
   * [定义表（object对象声明，单例）](ding_yi_biao.md)
   * [实现SqliteOpenHelper（to）](shi_xian_sqliteopenhelper.md)
   * [依赖注入](yi_lai_zhu_ru.md)

   
### [集合和函数操作符](ji_he_he_han_shu_cao_zuo_fu.md)


   * [总数操作符](zong_shu_cao_zuo_fu.md)
   * [过滤操作符](guo_lv_cao_zuo_fu.md)
   * [映射操作符](ying_she_cao_zuo_fu.md)
   * [元素操作符](yuan_su_cao_zuo_fu.md)
   * [生产操作符](sheng_chan_cao_zuo_fu.md)
   * [顺序操作符](shun_xu_cao_zuo_fu.md)

   
### [从数据库中保存或查询数据](cong_shu_ju_ku_zhong_bao_cun_huo_cha_xun_shu_ju.md)


   * [创建数据库model类](chuang_jian_shu_ju_ku_model_lei.md)
   * [写入和查询数据库](xie_ru_he_cha_xun_shu_ju_ku.md)

   
### [Kotlin中的null安全](kotlinzhong_de_null_an_quan.md)


   * [可null类型怎么工作](ke_null_lei_xing_zen_yao_gong_zuo.md)
   * [可null性和Java库](ke_null_xing_he_java_ku.md)

   
### [创建业务逻辑来访问数据](chuang_jian_ye_wu_luo_ji_lai_fang_wen_shu_ju.md)
### [Flow control和ranges](flow_controlhe_ranges.md)


   * [If表达式](ifbiao_da_shi.md)
   * [When表达式](whenbiao_da_shi.md)
   * [For循环](forxun_huan.md)
   * [While和do/while循环](whilehe_do__while_xun_huan.md)
   * [Ranges](ranges.md)

   
### [创建一个详情界面](chuang_jian_yi_ge_xiang_qing_jie_mian.md)


   * [准备请求](zhun_bei_qing_qiu.md)
   * [提供一个新的activity](ti_gong_yige_xin_de_activity.md)
   * [启动一个activity：reified函数](qi_dong_yige_activity__reified_han_shu.md)

   
### 接口和委托


   * [接口](jie_kou.md)
   * [委托](wei_tuo.md)
   * [在我们的App中实现一个例子](zai_wo_men_de_app_zhong_shi_xian_yi_ge_li_zi.md)

   
### [泛型](fan_xing.md)


   * [基础(fun < T>)](ji_chu.md)
   * [变体(< out T>、 < in T>)](bian_ti.md)
   * [泛型例子](fan_xing_li_zi.md)

   
### [设置界面](she_zhi_jie_mian.md)


   * [创建一个设置activity](chuang_jian_yi_ge_she_zhi_activity.md)
   * [访问Shared Preferences](fang_wen_shared_preferences.md)
   * [泛型preference委托](fan_xing_preference_wei_tuo.md)

   
### [测试你的App](ce_shi_ni_de_app.md)


   * [Unit testing](unit_testing.md)
   * [Instrumentation tests](instrumentation_tests.md)

   
### [其它的概念](qi_ta_de_gai_nian.md)


   * [内部类](nei_bu_lei.md)
   * [枚举](mei_ju.md)
   * [密封（Sealed）类](mi_feng_lei.md)
   * [异常（Exceptions）](yi_chang_ff08_exceptions.md)

   
### [<font color = "blue">kotlin高阶函数常用</font>](kotlin高阶函数的使用.md)
####### [结尾](jie_wei.md)

