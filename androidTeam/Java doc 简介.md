# Java doc 简介


[Java doc 官方传送门](https://docs.oracle.com/javase/7/docs/technotes/tools/windows/javadoc.html)

| Java Tags	| JDK	| Overview Tags	| Package Tags	| Class Tags	| Field Tags | Method Tags 
| --- | :-: | :-: | :-: | :-: | :-: | :-: |
| [@author](https://docs.oracle.com/javase/7/docs/technotes/tools/windows/javadoc.html#author) | 1.0 |✓	|✓	|✓	|	||
| [{@code}](https://docs.oracle.com/javase/7/docs/technotes/tools/windows/javadoc.html#code) | 1.5 |	|	|	|	||
| [{@docRoot}](https://docs.oracle.com/javase/7/docs/technotes/tools/windows/javadoc.html#docRoot) | 1.3 |✓	|✓	|✓	|✓	|✓|
| [@deprecated](https://docs.oracle.com/javase/7/docs/technotes/tools/windows/javadoc.html#deprecated) | 1.0 |	|✓	|✓	|✓	||
| [@exception](https://docs.oracle.com/javase/7/docs/technotes/tools/windows/javadoc.html#exception) | 1.0 |	|	|	|✓	||
| [{@inheritDoc}](https://docs.oracle.com/javase/7/docs/technotes/tools/windows/javadoc.html#inheritDoc) | 1.4 |	|	|	|	|✓|
| [{@link}](https://docs.oracle.com/javase/7/docs/technotes/tools/windows/javadoc.html#link) | 1.2 |✓	|✓	|✓	|✓	|✓|
| [{@linkplain}](https://docs.oracle.com/javase/7/docs/technotes/tools/windows/javadoc.html#linkplain) | 1.4 |✓	|✓	|✓	|✓	|✓|
| [{@literal}](https://docs.oracle.com/javase/7/docs/technotes/tools/windows/javadoc.html#literal) | 1.5 |	|	|	|	||
| [@param](https://docs.oracle.com/javase/7/docs/technotes/tools/windows/javadoc.html#param) | 1.0 |	|	|	|✓	||
| [@return](https://docs.oracle.com/javase/7/docs/technotes/tools/windows/javadoc.html#return) | 1.0 |	|	|	|✓	||
| [@see](https://docs.oracle.com/javase/7/docs/technotes/tools/windows/javadoc.html#see) | 1.0 |✓	|✓	|✓	|✓	|✓|
| [@serial](https://docs.oracle.com/javase/7/docs/technotes/tools/windows/javadoc.html#serial) | 1.2 |	|✓	|✓	|✓	||
| [@serialData](https://docs.oracle.com/javase/7/docs/technotes/tools/windows/javadoc.html#serialData) | 1.2 |	|	|	|	|✓|
| [@serialField](https://docs.oracle.com/javase/7/docs/technotes/tools/windows/javadoc.html#serialField) | 1.2 |	|	|	|✓	||
| [@since](https://docs.oracle.com/javase/7/docs/technotes/tools/windows/javadoc.html#since) | 1.1 |✓	|✓	|✓	|✓	|✓|
| [@throws](https://docs.oracle.com/javase/7/docs/technotes/tools/windows/javadoc.html#throws) | 1.2 |	|	|	|	|✓|
| [{@value}](https://docs.oracle.com/javase/7/docs/technotes/tools/windows/javadoc.html#value) | 1.4 |	|	|	|✓	||
| [@version](https://docs.oracle.com/javase/7/docs/technotes/tools/windows/javadoc.html#version) | 1.0 |✓	|✓	|✓	|✓	|✓|

    
1. 类/接口注释
> 类或者接口的注释必须在所有import语句的后面，同时又要位于class定义的前面。 用来说明类的一些情况, 可以包涵 @version,@author参数, 但Javadoc缺省情况下不处理, 也就是说不在最后文档中出现的, 为了使用这些信息, 我们可以加入参数 -version和 -author来强制输出到最后的文档中.

2. 变量注释
> 变量注释写在变量前面，对变量用途的简单介绍

3. 方法注释
> 紧靠在每条方法的前面，一个对方法功能的描述，和方法参数、返回值的解释，也可以包括方法的作者、添加版本和日期等

====

 * @author 作者名
> 当使用author标记时，用指定的文本文字在生成的文档中添加“Author”（作者）项。文档注释可以包含多个@author标记。可以对每个@author指定一个或者多个名字。当然你同样可以使用多个作者标记，但是它们必须放在一块。

* @version 版本
> 这个标记建议一个“版本”条目，后面的文字可以是当前版本的任意描述。一般用于类。

* @since 版本/日期/...
> 该标记可以生成一个注释表明这个特性（类、接口、属性或者方法等）是在软件的哪个版本之后开始提供的。

* @deprecated 类、属性、方法名等
> 指出一些旧功能已由改进过的新功能取代。该标记的作用是建议用户不必再使用一种特定的功能，因为未来改版时可能摒弃这一功能。若将一个方法标记为@deprecated，则使用该方法时会收到编译器的警告。这个标记可以增加一条注释，后面得句子还可以解释为什么不鼓励使用它。有时候，我们也推荐另外一种解决办法，例如：
<pre>@deprecated Use  newApi使用{@link}标记给一个推荐的链接。</pre>
        
* @see 链接 label
> 这个标记在“See also”（参见）小节增加一个超链接。这里的链接可以是下面几项内容：
    <pre>· package.class#member label 添加一个指向成员的锚链接，空格前面是超链接的目标，后面是显示的文字。注意分隔类和它的成员的是#而不是点号，你可以省略包名或者连类名也一块省略，缺省指当前的包和类，这样使注释更加简洁，但是#号不能省略。label是可以省略的。</pre>
    
* \{@link 链接 label\}和\{@linkplain 链接 label\}
> 其实准确的说，link的用法和see的用法是一样，see是把链接单列在参见项里，而link是在当前的注释中的任意位置直接嵌入一段带超级链接的文字。如果label是纯为使用linkplain
> 
    ```
    /**
     * 计算两个参数的和
     *
     * @param a 参数1
     * @param b 参数2
     * @return 两个参数的和
     * @throws ArithmeticException look {@link Math#addExact(int, int)}
     * @see Math#addExact(int, int)
     * @since 1.1
     */
    public static int addExact(int a, int b) {
        return Math.addExact(a, b);
    }
    ```

* {@value} 
> 用于生成被标记的常量字段的值
>
    ```
    /**
     * for test 值为 {@value}
     */
    private static final int TEST = 1;
   ```
   ```
    /**
     * test @value
     * @return 值为 {@value #TEST}
     */
    public int getTestValue() {
        return TEST;
    }
    ```
 
* {@literal}和{@code}
> 忽略包裹的html标记
> 
    ```
    /**
     * test {@literal <a>html标签</a>}
     * 这里的a标签是不会被识别为h5标记
     */
    public void testLiteral() {
        System.out.println("test {@literal}");
    }
    ```

====
##### 方法独有的tag

* @param 方法变量描述
> 当前方法需要的所有参数，都需要用这个标记进行解释，并且这些标记都应该放在一起。具体的描述（说明）可同时跨越多行，并且可以使用html标记。

* @return 方法的返回值
> 这个标记为当前方法增加一个返回值（“Returns”）小节。同样具体描述支持html并可跨多行。

* @throws @exception 方法抛出的异常
> 这个标记为当前方法在“Throws”小节添加一个条目，并会自动创建一个超级链接。具体的描述可以跨越多行，同样可以包括html标记。一个方法的所有throws都必须放在一起。@throw(1.0)和@exception(1.2)只是添加的版本不一样

* {@inheritDoc} 继承父类doc

====
###### 其他Other
* java doc 支持 
    * 纯文本
    * 邮箱链接
    <pre>
        \<a href="test@mail.com"\>e-mail\</a>
        @author \<a href="you email">you name\</a> 

    </pre>
    
    * HTTP链接
    <pre>
        \<a href="http://www.che300.com"> link\</a> 
        @author \<a href="you blog">you name\</a>
    </pre>
* \<pre>code\</pre> 保留样式
> 例如：
> 示例代码，需要使用\<pre>formated code\</pre>包裹

* \<p>、\<br> 换行 \<p>会在换行时插入间隔


=====
author：胡晟昊
date：2018.3.16




