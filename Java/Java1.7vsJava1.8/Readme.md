# Java 8 新特性


-------

## 目录
1. [Lambda表达式](#category1)
2. 方法引用
3. 默认方法
4. Stream API
5. Date Time API
6. Optional类
------

## <span id = "category1"> Labmbda表达式</span>
1. 什么是Lambda表达式
	* 允许把函数作为一个方法的参数的表达式（闭包）。
	* 简化Java 7的匿名内部类写法。
	* 给Java提供了函数式编程的特点。
2. 什么是匿名类
    *   定义类的同时再新建这个类的实例。
    *   匿名类由以下部分组成：new操作符，接口名称，参数列表，大括号{}。
    *   经典例子，new Runnable(){...}； new Comparator(){...}；
    *   访问权限：
        1. 外层Class里的字段。
        2. 不能访问外层方法中除final修饰的变量。
        3. 如果内部类的名称与外面能访问的名称相同，则会把名称覆盖掉。
    * 匿名类内部不可有的东西：
        1. 静态代码块；
        2. 定义接口；
        3. 定义构造函数；
3. 简写匿名内部类的依据
	* 能使用Lambda表达式的匿名内部类必须有相应的函数接口（FunctionalInterface)。
	* 如何实现一个可以使用Lambda的接口呢？编写一个只有一个抽象方法的接口即可。
4. 用Lambda表示式实现函数编程，编译后不会产生额外的类。
    ```java
	public class Lambda {
		static {
			System.setProperty("jdk.internal.lambda.dumpProxyClasses", ".");
		}
		public static void main(String[] args) {
			Consumer<String> c = new Consumer<String>(){
				@Override
				public void accept(String s) {
					System.out.println(s);
				}
				};
			c.accept("hello lambda");
		}
	}
	```
	上述代码编译后会产生两个class, (Lambda.class与Lambda$1.class).
	```java
	import java.util.function.Consumer;

	public class Lambda {
		public static void main(String[] args) {
			Consumer<String> c = s -> System.out.println(s);
			c.accept("hello lambda!");
		}
	}
	```
	使用Lambda表达式替换后，只会产生一个class.(Lambda.class)

5. 造成上面情况的原因：Invokedynamic指令
	* 什么是InvokedDynamic指令？Java7发布的一条新指令，通常指令（invokevirtual, invokespecial, invokestatic, invokeinterface），通常方法的符号引用在静态类型语言编译时就能产生，而这条指令给Java提供了在运行期进行类型检查的功能。

6. 
