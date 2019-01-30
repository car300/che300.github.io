#android开发规范
##命名
###文件名
### 包名全部小写，连续的单词使用下划线连接起来，。
包结构

* model-model功能-项目功能-模块-功能  适合大型项目。model层次分明，模块独立、高内聚，模块间低耦合，易于移植，方便独立开发测试，易于集成

类文件 

* 模块-功能-组件 大驼峰 例：EnquireDetailAcitivty，EnquiryListActivity，CarDetailBaseFragment

* 接口文件 用途-模块-功能-组件 大驼峰 例：JSDialogInterface

* 资源文件 资源使用属性-模块-功能-属性  全部小写，下划线连接单词 例：activity_authentication_rejected.xml

  item_authentication_rejected_list.xml

  layout_authentication_rejected.xml

  img_assess_report_share.jpg

  round_ff6600_stoke_f4e9e1_back_radius_2dp.xml（drawable）
  ic_arrow2bottom_yellow.png
  umeng_socialize_slide_in_from_bottom.xml（anim）

变量

* 基类变量 m+大驼峰 例：mContext，mContentParams
* 类自成员变量 小驼峰  例：minRegYear，tvVinNum（控件变量：控件名首字母小写的缩写-模块—功能 kotlin  tv_vin_num）
* 常量 全部大写，单词间用下划线_连接
* 局部变量 小驼峰

变量声明

* 每次只声明一个变量不要使用组合声明，比如int a, b;。
* 需要时才声明，并尽快进行初始化，不要在一个代码块的开头把局部变量一次性都声明了(这是c语言的做法)，而是在第一次需要使用它时才声明。 局部变量在声明时最好就进行初始化，或者声明后尽快进行初始化。

方法 小驼峰 

* 静态公共类方法 动词-模块名-功能名
* 内部方法 动词-名词 参数判空注解、类型注解，返回值使用提示注解（如果需要）

Javadoc

* 至少在每个public类及它的每个public和protected成员处使用Javadoc，以下是一些例外：
* 1 例外：不言自明的方法，对于简单明显的方法如getFoo，Javadoc是可选的(即，是可以不写的)。这种情况下除了写“Returns the foo”，确实也没有什么值得写了
* 2 例外：重写
  如果一个方法重写了超类中的方法，那么Javadoc必需的。
  其他
* 少用全局变量作为非业务内聚方法间传参
* 抽取通用公共方法，抽取与具体业务需求无关方法
* 抽取相同作用类型代码为方法。如界面赋值、变量赋值。
* 一个方法代码如无必要，逻辑代码尽量不要超过十行。
* 网络请求成功的回调里 逻辑代码不要超过10行。if-else 嵌套不超过两层
* 少用并行判断。多用线性判断（易于理解和维护）
* 多用封装的工具类
* 尽量链式调用代码（易于理解。思路少分支）
* 注意判空处理，异常捕获与处理。兼容异常情况，异常分布捕获。尽量限制异常捕获范围到具体可能发生的异常。


