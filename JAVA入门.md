[TOC]

[TOC]

#                                               JAVA入门



## Homework1

### JDK JRE JVM关系

1. **JDK = JRE + java开发工具**
2. **JRE = JVM + 核心类库**

### 环境变量path配置及其作用

1.环境变量的作用是为了在dos的任意目录，可以用java和javac命令

2.先配置JAVA_HOME=指向jdk安装的主目录

3.编辑path环境变量，增加%JAVA_HOME%\bin(%表示引用)(等价于d:\JDK\bin)

## API

### API概念

是JAVA提供的基本编程接口 中文在线文档：https://www.matools.com

## 变量



### 变量原理

变量是程序组成的基本单位 三要素（类型 名称 值）



### 变量概念

变量相当于内存中一个数据存储空间表示，可以将变量看做是一个房间的门牌号，通过门牌号我们可以找到房间，而通过变量名可以访问到变量值

### 变量细节

1.变量表示内存的一个存储区域（不同的变量 类型不同 占用的空间大小不同）

2.该区域有自己的名称【变量名】和类型【数据类型】

3.变量必须先声明 再使用

4.该区域的数据/值可以在同一类型范围内不断变化

5.变量在同一个作用域内不能重名

6.变量=变量名+值+数据类型

**同一个变量名不能存在于同一个作用域（即类） 在不同作用域可以存在**





## 数据类型



### 基本数据类型



#### 数值型



##### 整数型

一字节中可以放8个二进制编码(bit) 第一位表示正负数0表示正数 1表示负数

###### byte[1]

范围：-128~127（-2<sup>7</sup>  ~2<sup>7</sup> -1）

###### short[2]

范围：-2<sup>15</sup> ~2<sup>15</sup> -1

###### int[4]

范围：-2<sup>31</sup> ~2<sup>31</sup> -1

###### long[8]

范围：-2<sup>63</sup> ~2<sup>63</sup> -1



##### 整数型细节

1.JAVA默认为int型 声明long型常量需要加上"l"或者"L"

2.java程序中变量常声明为int型，除非不足表示大数，才用long

int n1=1;

int n2=1L(**`错`**) 无法将8字节塞入4字节中

解决办法：long n3=1L;



##### 小数型

浮点数存放形式：

**浮点数=符号位+指数位+尾数位**

**尾数部分可能丢失，造成精度损失（小数都是近似值）**

单精度float[4]

双精度double[8]

注意：

1.JAVA的浮点型常量默认为double型，声明float型常量，需后加**’f'或‘F'**

2.浮点型常量有**两种表示形式**

十进制形式：如 5.12 512.0f   .512(等价于0.512)（必须有小数点）

科学计数法形式：5.12e2[]  5.12E-2[]

3.通常使用double类型 它比float更精确

4.浮点数使用陷阱

```java
    double num8=2.7;//2.7

	double num9=8.1/3;//2.6999999999999997
//false
	/*if（num8=num9）
{
    System.out.println("相等")；
}*/

//ture
if（Math.abs(num8-num9)<0.00000001)//use API
{
    System.out.println("equal to");
}

```

**电脑认为8.1后还有很多位000000（如8.10000001），以精度形式返回值**

**因此判断相等时不能直接使用=**

**而是使用两个值的差值在一定的范围内**



#### 字符型

基本介绍：字符类型可以表示单个字符 字符类型是char char是两个字节（可以存放汉字）

多个字符我们可以用字符串String

char 本质是一个**整数** 在默认输出时 **是unicode码对应的字符** 并且可以进行运算（输出的也是一个整数）

进行类型转换加上（int）

#### +号的使用

1.当左右两边都是数值型时，则作加法运算

2.当左右两边有字符型时，做拼接运算

**例如：**System.out.println(100+98);输出的值为198

​		  System.out.println(100+98);输出的值为10098

  		System.out.println(“hello“+98);输出的值为hello98





#### 布尔型(boolean)

boolean[1],存放true false

适用于逻辑运算 一般用于程序流程控制

**不可以以0或者非0的整数代替false和true 与C语言不同**

不参与自动转换

不能强转 例如不能将Int型转换为boolean型

if 

while

do-while

for



### 基本数据类型转换

当JAVA程序在进行赋值或者运算时 精度小的类型**自动转换**为精度大的数据类型，这个就是就是自动类型转换



**char-**>int->long->float->double

**byte->short-**>int->long->float->double





#### 自动类型转换使用和细节

1.有多种类型的数据混合计算时 系统首先自动将所有数据转换成容量最大的那种数据类型(向下兼容) 然后再进行计算**（float类型加f/F）**

byte b1=10;//**对**  判断范围

int n2=1;

byte b2=n2;//**错误** 换成变量时 判断类型 塞不进去

**byte转成short而不是char**



2.当我们的精度（容量）大的数据类型赋值给精度（容量）小的数据类型时 就会报错 反之就会进行自动类型转换

3.（byte,short）和char之间不会相互自动转换

4.byte short char 三者可以进行运算在计算时（**包括相同类型计算 如byte+byte**）首先转换为int类型

如：byte b2=1; short s1=1; short s2=bs+s1;(**错**)

5.boolean不参与转换

6.自动提升原则：结果为操作数最大的类型



#### 强制类型转换



将精度高的转换成精度小的

**1.造成精度损失 int a=（int)1.9; 结果为1**

**2.造成溢出**  装不下 后面的数造成溢出

**3.优先级大于加减乘除 转换最近的数**

如：int x=(int)10 * 3.5+6 * 1.5;错 将10转换成int型再计算 右边仍是double类型

int x=(int)（10 * 3.5+6 * 1.5）;对 利用小括号提升优先级

4.char类型可以保存int的常量值 不能保存int的变量值 需要强制转换   

如： int m=100; char c2=m;(错) char c3=(char)m;(对)

5.byte short char 三者可以进行运算在计算时（**包括相同类型计算 如byte+byte** **与常数计算 如byte+1**）首先转换为int类型





### 基本数据类型和String类型的转换



#### 基本类型转String类型

 **语法：将基本数据类型的值+" "即可**



#### String类型转基本数据类型

**语法：**通过基本类型的包装类调用parseXX方法即可



#### 注意事项

1.在将String类型转成基本数据类型时 要确保String类型能够转成有效的数据 

例如我们可以将123转成一个整数 而不能将“hello”转换成一个整数

2.如果格式不正确，就会抛出异常 程序就会终止 这个问题在异常处理章节中会处理

![image-20220801165558484](C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220801165558484.png)



### 引用数据类型

#### 类（class)

#### 接口(interface)

#### 数组([])



## 运算符



### 算数运算符

算术运算符是对数值类型的变量进行运算的



<img src="C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220801172856224.png" alt="image-20220801172856224"  />



**当%运算a为负数时 公式为a-(int)a/b*b**

**有小数运算得到的是近似值**



#### ++运算符

**前++：++i先自增后赋值**

**后++：++i先赋值后自增**



### 关系运算符

介绍：

1.结果都是boolean型  姚明是true要么是false

2.关系运算符常用于if结构的条件中或循环结构条件中



### 逻辑运算符



1.短路与&& 短路或||  取反！

2.逻辑与& 逻辑或|  ^逻辑异或（当a b不同时 结果为true 否则为false）



**注意：短路与有假即为假 短路或有真则为真 不判断第二个 除此情况与逻辑与或相同 因此短路与短路或效率较高**



<img src="C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220812154518364.png" alt="image-20220812154518364" style="zoom: 50%;" />



### 赋值运算符



赋值运算符就是将某个运算后的值，赋给指定的变量



赋值运算符的特点

1.复合赋值运算符等价于下面的效果

比如：a+=3 等价于a=a+3 **前面的值加上后面的值**

2.复合赋值运算符会进行类型转换

byte b=2; b+=3；**（底层等价于（byte）b+=3;若为b=b+3;即会报错）** b++;**（底层等价于（byte） b++;））**

3.运算顺序从右向左

4.左边只能是变量 右边可以是变量 表达式 常量值  



### 三元运算符



语法

条件表达式？表达式1：表达式2；

1.如果为真 执行表达式1 反之执行表达式2

2.表达式1和表达式2要为可以赋给接收变量的类型（或可以自动转换）

3.三元运算符可以转成if-else语句



### 运算符的优先级

<img src="C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220812163047909.png" alt="image-20220812163047909" style="zoom:50%;" />





## 标识符



### 标识符的命名规则与规范

1.Java对各种变量 方法和类命名时使用的字符序列都称作标识符

2.凡是自己可以起名字的地方都叫标识符 int num1=1;



### 标识符的命名规则（必须遵守）

1.由26个英文字母大小写，0-9，—或&组成

2.不可以数字开头

3.不可以使用关键字和保留字，但能包含关键字和保留字

4.Java中严格区分大小写 长度无限制

5.标识符不能包含空格



### 标识符的命名规范（更加专业）



1.包名：多单词组成时所有字母都小写;aaa.bbb.ccc

2.类名 接口名：多单词组成时 所有单词的首字母大写：XxxYyyZzz

3.变量名 方法名：多单词组成时，第一个单词字母小写 第二个单词开始每个字母大写：xxxYyyZzz

4.常量名：所有字母都大写 单词间用—连接





## 键盘输入语句



### 介绍



在编程中 需要接收用户输入的数据 就可以使用键盘输入语句来获取

**input.java**  需要一个扫描器 就是Scanner（在util这个包）

<img src="C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220813092230405.png" alt="image-20220813092230405" style="zoom: 44%;" />



### 步骤

1.导入该类所在包 java.util.*

2.创建该类对象（声明变量）

3.调用里面的功能

**注意：**输入时第一个用.next（）；代表从这开始查找

后面的用各个类型对应的类 nextInt（） nextDouble（）



## 进制



**N进制**：到N进1（如8进制中的8为10）



### N进制转十进制

**规则：**从最低位开始 将每个位上的数提取出来 乘以N的（位数-1）次方然后求和



### 十进制转为N进制



**规则：**将该数不断除以N直到商为0为止 然后将每步得到的余数**倒过来** 就是对应N进制



### 二进制转为八进制



**规则：**从最低位开始 将二进制数每三位一组，转成对应八进制即可



### 八进制转为二进制

**规则：**将八进制每一位转换为对应的一个三位数的二进制数即可



### 二进制转为十六进制



**规则：**从最低位开始 将二进制数每四位一组，转成对应十六进制即可



### 十六进制转为二进制

**规则：**将十六进制每一位转换为对应的一个四位数的二进制数即可



### 二进制在运算中的说明

现代计算机技术全部采用的是二进制 易用电子方式实现 计算机内部处理的信息 都是采用二进制数来表示的



### 原码反码补码

 



**要求背出来**

1.二进制的最高位是符号位：**0表示正数 1表示负数（1倒下去就是-）**

2.正数的原码  反码 补码都一样**(三码合一)**

3.负数的反码=它的原码**符号位不变** 其他**位取反**（0-1 1-0）

4.**负数的补码=它的反码+1 负数的反码=负数的补码-1  **（原码=>反码=>补码）

5.**0的反码补码都是0**

6.Java中的数都是**有符号**的

7.计算机在运行的时候都是以**补码**的方式来运行的（补码统一了正数负数）

8.当我们看结果的时候 要看他的**原码（重点）**

<img src="C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220814203303561.png" alt="image-20220814203303561" style="zoom:44%;" />



### 位运算符



按位与&      ：两位**全为1**才为1否则为0

按位或|       ：**有1**则为1 无一为0

按位异或^   ：两个一个为0一个为1则为1 否则为0

按位取反~   ：0->1 1->0

算数右移>>  :低位溢出 符号位不变 并用符号位补溢出的高位（1>>2本质就是1 / 2 / 2）

算数左移<<  :符号位不变 低位补0                                             (1<<2本质就是1 * 2 * 2)

逻辑右移>>> :低位溢出 高位补0   （没有<<<符号）





## 控制结构





### 顺序控制



程序从上到下逐行进行 中间没有任何判断和跳转





### 分支控制



#### 单分支



if（条件表达式）

{执行代码块；（可以有多条语句）}

else

{执行代码块；（可以有多条语句）}



#### 多分支



##### if else

if（条件表达式1）

{执行代码块1；}

else if(条件表达式2)

{执行代码块2；}

......

else

{执行代码块n；}

从上往下判断 **只**运行一个执行路口 如果全部都不成立 默认执行else后的语句

**多分支可以没有else** 如果所有的条件表达式都不成立 则一个执行路口都没有



##### **switch分支**

switch（表达式）

{case 常量1：//当

语句块1；

break；//结束switch

case 常量n：//当

语句块n；

break；

...

default:

default语句块；//前面都没匹配成功

break；

}

<img src="C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220815171754967.png" alt="image-20220815171754967" style="zoom:50%;" />



**也可以还几个case输出一个语句**

case1：

case2：

case3：
语句块

break；



**switch注意事项**

1.表达式的类型 应该和case后的常量类型一致 或者是可以自动转成可以相互比较的类型 比如输入的是字符 而常量是int

2.switch表达式中表达式的返回值必须是：**（byte short int char enum String)**

3.case子句中的值必须是常量 而不能是变量

4.default子句是可选的 当没有匹配的case时 执行default 若没有default 语句 则没有输出

5.break语句用来执行完一个case分支后使程序跳出switch语句块 如果没有写break 程序会顺序执行到switch结尾





### 循环控制



#### for循环控制

**语法：**

for(循环变量初始化；循环条件；循环变量迭代)

{

循环语句；

}



##### for循环控制流程分析



**循环条件判断=>循环操作=>循环变量迭代=>循环条件判断**

<img src="C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220816101211998.png" alt="image-20220816101211998" style="zoom: 80%;" />







##### for循环注意事项

1.循环条件的返回一个布尔值的表达式

2.for(;循环判断条件；)中的初始化和变量迭代可以写道其他地方，但是两边的分号不能省略//**循环之后还想使用i 值是退出循环返回的值**

3.循环初始值可以有多条初始化语句 但是要求类型一样 并且中间用逗号隔开 循环变量迭代也可以用多条语句 用逗号隔开



#### while循环

先判断再执行

语法：

while（循环条件）

{

循环语句；

循环变量迭代；

}



<img src="C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220816110503140.png" alt="image-20220816110503140" style="zoom:150%;" />





#### do while循环

先执行后判断 也就是**最少会执行一次**

语法：
do{

循环语句；

循环变量迭代；

}

while（循环条件）；

![image-20220816111820276](C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220816111820276.png)







### 跳转控制语句



#### break语句

![image-20220818094400195](C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220818094400195.png)





##### break细节

1.语句中存在多层嵌套的语句块中 可以通过标签指明要终止的是哪一层语句块

![image-20220818095056255](C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220818095056255.png)



（1）lable是名称 可以改

（2）label语句可以指定退出哪层

（3）在实际开发中 尽量不要使用标签

（4)如果没有标签 默认推出最近的循环体



##### break练习



<img src="C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220819195237321.png" alt="image-20220819195237321" style="zoom:80%;" />

import java.util.Scanner;
public class BreakExercise
{

```java
public static void main(String[]args)
{

	Scanner myScanner=new Scanner(System.in);

	String name="";//初始化
	String passwd="";//初始化
	int chance=3;
	for(int i=1;i<=3;i++)
	{
		System.out.println("please input your name");
		name=myScanner.next();
		System.out.println("please input your passwd");
		passwd=myScanner.next();
		if("DJ".equals(name)&&"666".equals(passwd))//用equals方法判断是否相等
		{
			System.out.println("Congratulations on your login");
			break;//终止for循环
		}
		
		else
		{
			chance--;
			System.out.println("You have "+chance+" chances to log in");

		}
	}
}
```

}







#### continue语句



**基本介绍**

**1.continue语句用于结束本次循环** **继续执行下一次循环**

2.continue也可使用标签指明跳过哪一层循环 和break规则一样



**基本语法**

{

......

continue;

......

}





<img src="C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220819200039503.png" alt="image-20220819200039503" style="zoom:67%;" />



**代码**

public class continue01
{

```java
public static void main(String[]args)
{
	int i=1;
	while(i<=4)
	{
		i++;
		if(i==2)
		{
			continue;
		}
		System.out.println("i=" + i);
		
	}
}
```

}

**结果**

![image-20220821152508233](C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220821152508233.png)





#### return语句



**介绍**

return使用在方法 表示跳出所在的方法 在讲解方法的时候 会详细的介绍 

注意：如果return写在main方法 退出程序





```java
public static void main(String[]args)
{
	for(int i=1;i<=5;i++)
	{

		if(i==3)
		{
			System.out.println("hsp"+i);
			return;
		}
		System.out.println("Hello World!");
	}
	System.out.println("go on...");//有return不执行（退出程序） 而break执行（退出循环）
}
```



运行结果：

<img src="C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220821154800771.png" alt="image-20220821154800771"  />



#### 本章练习



<img src="C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220821155455229.png" alt="image-20220821155455229" style="zoom: 80%;" />





```java
public static void main(String[]args)
{
	int a=100000;
	int sum=0;
	while(a>50000)
	{

		a=(int)(0.95*a);
		sum++;
		if(a<50000)
		{
			break;
		}

	}

	sum=sum+(int)(a/1000);
```


		System.out.println("sum=" +sum);


```java
}
```



<img src="C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220821161259027.png" alt="image-20220821161259027" style="zoom:80%;" />



import java.util.Scanner;
public class Exercise02
{

```java
public static void main(String[]args)
{

	System.out.println("please input number!");
	Scanner myScanner=new Scanner(System.in);

	int a=myScanner.nextInt();

	int b=a/100;

	int c=a%100/10;

	int d=a%10;
	int E=b*b*b+c*c*c+d*d*d;
	if(a==E)
	{
		System.out.println("Yes!");
	}
	else
	{
	System.out.println("No!");
	}
}
```

}







<img src="C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220821164634201.png" alt="image-20220821164634201" style="zoom:80%;" />



```java
public static void main(String[]args)
{
	int count=0;
	for(int i=1;i<=100;i++)
	{
			if(i%5!=0)
			{
				conut++;//用count计算输出个数
				System.out.print(+i);
			}
			
			if(count%5==0)//当统计个数为5时进行换行
			{
				System.out.println();
			}
	}
}
```






![image-20220821165242964](C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220821165242964.png)

**法一：**

```java
public static void main(String[]args)
{	
    for(char c1='a';c1<='z';c1++)//字符本质就是编码
	{
	System.out.print(c1+" ");
	}
	for(char c2='Z';c2>='A';c2--)
	{
	
	System.out.print(c2+" ");
	}
}
```


**法二：**


```java
public static void main(String[]args)
{	
    for(int i=97;i<=122;i++)
	{
		
		System.out.println((char)(+i));//强制类型转换
	}
	for(int j=90;j>=65;j--)
	{
		
		System.out.println((char)(+j));//强制类型转换
	}
}
```







![image-20220821171913771](C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220821171913771.png)

```java
public static void main(String[]args)
{

	double sum=0;
	
	for(int i=1;i<=100;i++)
	{
		
		if(i%2==0)
		{
			sum=sum-(1.0/i);//是1.0不是1 否则得不到精确值
		}

		else
		{
			sum=sum+(1.0/i);//是1.0不是1 否则得不到精确值
		}
	}
	System.out.println(sum+" ");
}
```

​	

**注意：是1.0不是1 否则得不到精确值**

分子为1时sum=1 为1.0时sum=0.688

![image-20220821172147372](C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220821172147372.png)







<img src="C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220821172725425.png" alt="image-20220821172725425" style="zoom:80%;" />





```java
public static void main(String[]args)
{
	int total=0;
	int sum=0;
	for(int i=1;i<=100;i++)
	{
		sum=sum+i;
		total=total+sum;
	}
	System.out.println(total+" ");
}
```







## 数组



### 数组介绍



数组可以存放同一个类型的数据。数组也是一种数据类型 是引用类型

即：**数（数组）组（一组）就是一组数据**



double[]：**double型的数组**  [0]:下标从零开始编号

hens：**数组名**

{3,5,1,3.5,2,50}：**数组元素**

可以根据数组名.length得到数组的大小/长度  如：hens.length

数组创建后 没有赋值有默认值

int byte short long=0;  float double=0.0; boolean false; String null;




```java

	public static void main(String[]args)
	{
	double[]hens={3,5,1,3.5,2,50};
	double totalWeight=0;
	for(int i=0;i<6;i++)//0-5
	{
		totalWeight+=hens[i];
	}
	System.out.println(totalWeight);
}
```







### 数组的使用



#### 方式**int a[ ]=new int[5];**

数据类型 数组名[ ]=new 数据类型[ 大小]

**int a[ ]=new int[5];**



#### 方式 int a[ ]a=new int[10];

先声明数组

语法：数据类型 数组名[ ];也可以 数据类型[ ] 数组名；

**int a[ ]; 或者 int [ ]a;**

创建数组

语法：数组名=new 数据类型[大小]；

**a=new int[10];**



#### 方式-静态初始化



静态初始化

语法：数据类型 数组名[ ]={元素值 ，元素值.....}

int a[ ]={2,3,4,5,6,7,8};





###  数组应用案例





<img src="C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220822094828348.png" alt="image-20220822094828348" style="zoom:80%;" />



```java
	public static void main(String[]args)
	{
	char[]arr=new char[26];
	for(int i=0;i<arr.length;i++)
	{

		arr[i]=(char)(i+65);//等同于 arr[i]=(char)('A'+i); 'A'+i是int类型需要强转
	}
	for(int i=0;i<arr.length;i++)
	{

		System.out.print(arr[i]+" ");
	}
}
```







<img src="C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220822095130347.png" alt="image-20220822095130347" style="zoom:67%;" />



```java
	int arr[]={4,-1,9,10,23};
	int max=arr[0];
	int maxIndex=0;//利用maxIndex储存下标
		for(int i=1;i<arr.length;i++)
		{
		if(arr[i]>max)
		{
			max=arr[i];
			maxIndex=i;
		}
	}
	System.out.println(max+" ");
	System.out.println(maxIndex+" ");

```





### 数组赋值机制



1.基本数据类型赋值 这个值就是**具体的数据** 而且相互**不影响**  //**值传递**

int n1=2; int n2=n1;

2.数组在默认情况下是引用传递 **赋的是地址** **能够影响**  //**引用传递** **地址拷贝**





```java
	public static void main(String[]args)
	{
		int n1=10;
		int n2=n1;
		n2=80;
		System.out.println(n1+ " ");//10
		System.out.println(n2+ " ");//80 不影响n1

		int[]arr1={1,2,3};
		int[]arr2=arr1;
		arr2[0]=10;//影响arr1
		System.out.println(arr1[0]+" ");
	}
```



<img src="C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220822101905772.png" alt="image-20220822101905772" style="zoom: 57%;" />





### 数组拷贝





```java
public static void main(String[]args)
	{
		int arr1[]={1,2,3};
	int arr2[]=new int[arr1.length];
	for(int i=0;i<arr1.length;i++)
	{

		arr2[i]=arr1[1];
	}
	arr2[0]=100;

	System.out.println(arr1[0]+" ");//不影响arr1
	System.out.println(arr2[0]+" ");
}
```





### 数组反转





```java
	public static void main(String[]args)
	{
	int arr1[]={1,2,3,4,5};
	int temp;
	for(int i=0;i<arr1.length/2;i++)//注意交换次数为arr1.length/2
	{
		temp=arr1[i];
		arr1[i]=arr1[arr1.length-1-i];
		arr1[arr1.length-1-i]=temp;
	}

	for(int i=0;i<arr1.length;i++)
	{
		System.out.println(arr1[i]+" ");
	}
}
```





### 数组扩容



```java
import java.util.Scanner;
public class ArrayAdd
{
	public static void main(String[]args)
	{
		int arr[]={1,2,3};
		Scanner myScanner=new Scanner(System.in);
		do
		{
			int arrnew[]=new int[arr.length+1];
			for(int i=0;i<arr.length;i++)
			{
				arrnew[i]=arr[i];
			}
			System.out.print(" please input");
			arrnew[arrnew.length-1]=myScanner.nextInt();
			arr=arrnew;
			for(int i=0;i<arr.length;i++)
			{
				System.out.print(arr[i]+" ");
			}
			System.out.print(" please input y/n");
			char key=myScanner.next().charAt(0);
			if(key=='n')
             {
				break;
			}
		}
		while(true);
		System.out.print(" go on...");
	}
}
```







### 数组缩减



```java
import java.util.Scanner;
public class ArrayAdd02
{
	public static void main(String[]args)
	{
		int arr[]={1,2,3};
		do
		{
			int arrnew[]=new int [arr.length-1];
			for(int i=0;i<arr.length-1;i++)
			{
				arrnew[i]=arr[i];
			}
			arr=arrnew;
			for(int i=0;i<arrnew.length;i++)
			{
				System.out.println(arrnew[i]+" ");
			}
				System.out.println("please input y/n");
				Scanner myScanner = new Scanner(System.in);
				char key=myScanner.next().charAt(0);
				if(key=='n'||arrnew.length==1)
				{
					break;
				}
		}while(true);
		System.out.println("go on...");
    }
}
```




### 冒泡排序法



依次比较相邻元素的值 若发现逆序则交换 使值较大的元素逐渐像后移 



**化繁为简 先内层再外层**

```java
public class BubbleSort
{
	public static void main(String[]args)
	{
		int arr[]={3,1,4,5,2};
		int temp;
		for(int i=0;i<arr.length-1;i++)
		{
			for(int j=0;j<arr.length-1-i;j++)
			{
				if(arr[j]>arr[j+1])
				{
					temp=arr[j];
					arr[j]=arr[j+1];
					arr[j+1]=temp;
				}
			}
		}
			for(int j=0;j<arr.length;j++)
			{
				System.out.print(arr[j]+" ");
			}
	}
}
```





### 二维数组



**二维数组的每一个元素都是一维数组**

应用场景

开发一个五子棋游戏 棋盘需要二维数组来表示



```java
public class TwoDimensionalArray
{
	public static void main(String[]args)
	{
		int [][] arr={{0,0,0},{0,1,0},{0,0,0}};

		 for(int i=0;i<arr.length;i++)
		 {
			for(int j=0;j<arr[i].length;j++)//访问二维数组中第i+1个数组
			{

				System.out.print(arr[i][j]+" ");
			}
			System.out.println();
	 	}
	}
}
```





#### 二维数组的使用



int a[][]=new int [2] [3];

表示二维数组中有2个一维数组 一维数组中有3个元素

<img src="C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220822155700417.png" alt="image-20220822155700417" style="zoom:80%;" />



```java

	public class TwoDimensionalArray02
{
	public static void main(String[]args)
	{
		int arr[][]=new int[3][];//只确定一维数组的个数 一维数组还没有开辟空间
		for(int i=0;i<arr.length;i++)//arr.length是二维数组中一维数组的个数
		{
			arr[i]=new int[i+1];//给一维数组开辟空间
		}
		for(int j=0;j<arr[i].length;j++)//arr[i].length是二维数组中第i个一维数组中元素的个数
		{
			arr[i][j]=i+1;
		}
	}	
}
```


**二维数组的存在形式**



arr[2] [3]的存在形式



<img src="C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220822154839753.png" alt="image-20220822154839753" style="zoom:80%;" />





#### 应用案例-杨辉三角



规律

1.第一行有1个元素 第n行有n个元素

2.每一行的首尾都是1

3.从第三行开始 arr[i] [j]=arr[ i-i] [j]+arr[ i-1] [j-1];



```java

public class YangHui
{
	public static void main(String[]args)
	{

		int arr[][]=new int[10][];

		for(int i=0;i<arr.length;i++)
		{
			arr[i]=new int[i+1];

			for(int j=0;j<arr[i].length;j++)
			{
				if(j==0||j==arr[i].length-1)
				{
					arr[i][j]=1;
				}
				else
				{
					arr[i][j]=arr[i-1][j]+arr[i-1][j-1];
				}
			}

		}
		for(int i=0;i<arr.length;i++)
		{
			for(int j=0;j<arr[i].length;j++)
			{
				System.out.print(arr[i][j]+" ");
			}
			System.out.println();
		}
	}

}
	
```



![image-20220822202528518](C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220822202528518.png)



#### 二维数组注意事项



二维数组实际上是由多个一维数组组成的 各个一维数组长度可以不一样 但必须是一维数组





#### 二维数组练习题





<img src="C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220822210212755.png" alt="image-20220822210212755" style="zoom:80%;" />





### 本章练习



<img src="C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220823091007425.png" alt="image-20220823091007425" style="zoom: 67%;" />









## 面向对象初级



### 类与对象

<img src="C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220823112617571.png" alt="image-20220823112617571" style="zoom: 67%;" />





<img src="C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220823112714093.png" alt="image-20220823112714093" style="zoom:67%;" />





```java

public class Object01
{
	public static void main(String[]args)
	{
        
        Cat cat1=new Cat();//创建一只猫 将其赋值给cat1
        cat1.name="a";
        cat1.age=3;
        cat1.color="white";
        
         Cat cat2=new Cat();
        cat2.name="b";
        cat2.age=4;
        cat2.color="blue";
        
        System.out.println("cat1:"+cat1.name+" "+cat1.age+" "+cat1.color);
         System.out.println("cat2:"+cat2.name+" "+cat2.age+" "+cat2.color);
    }
    
}

class Cat
{
    String name;
    int age;
    String color;
    
}
```



通过上面案例可以看出

1.类是抽象的 概念的 代表一类事物 比如人类 猫类

2.对象是具体的 实际的 代表一个具体事物

3.类是对象的模板 对象是类的一个个体 对应一个实例



#### 对象在内存中的存在形式



![image-20220823114347840](C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220823114347840.png)





#### 属性/成员变量



1.从概念上看：成员变量=属性=field（字段）(成员变量是用来表示属性的)

2.属性是类的一个组成部分 一般是基本数据类型 也可以是引用类型（对象 数组） 比如int age就是属性



**Person p1=new Person();**

**p1是对象名（对象引用）**

**new Person创建的对象空间 才是真正的对象**

<img src="C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220823151638270.png" alt="image-20220823151638270" style="zoom: 67%;" />



#### 如何创建对象



**先声明再创建**

Cat cat;//声明对象cat 栈和堆中为空 创建了才有

cat=new Cat();//创建



**直接创建**

Cat cat=new Cat();





#### 如何访问属性



对象名.属性名;

cat.name;



#### 类与对象的内存分布机制（重要）

<img src="C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220823152557368.png" alt="image-20220823152557368" style="zoom: 67%;" />





![image-20220824100243866](C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220824100243866.png)

![image-20220824100209981](C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220824100209981.png





**Java创建对象的流程简单分析**

1.先加载Penson类信息（属性和方法信息，只会加载一次）

2.在堆中分配空间 进行默认初始化（看规则）

3.把地址赋给p1,p1就指向对象

4.进行指定初始化 比如p1.name="小明"；

Person p2=p1;相当于一个人有两个名字（取小名 鲁迅和周树人）



#### 堆 栈 方法区

栈：一般存放基本数据类型（局部变量）

堆：存放对象（Cat cat,数组等）

方法区：常量池（常量，比如字符串），类加载信息





### 成员方法



基本介绍

在某些情况下 我们需要成员方法 比如人类 除了有一些属性外（年龄 姓名）我们人类还有一些行为比如：

可以说话 跑步  通过学习 还可以做算术题  这时就需要成员方法才能完成





```java
public class Method01
{
	public static void main(String[]args)
	{
	    //方法使用
        //1.方法写好后 如果不去调用 不会输出
        //2.先创建对象 然后调用方法即可
        Person p1=new Person;
        p1.speak();
        p1.cal01();
        p1.cal02(5);
        p1.getsum(1,1);
        int returnres=p1.getsum(1,1);
        System.out.println(returnres+" ");
	}
}


class Person
{
	String name;
	int age;
	//1.public表示方法是公开
	//2.void表示方法没有返回值
    //3.speak() speak是方法名 ()是形参列表
    //4.{}方法体 可以写我们执行的代码
	public void speak()
	{
		System.out.println("I am a good boy！");
	}

    public void cal01()
	{

		int res=0;
		for(int i=0;i<=1000;i++)
		{
			res+=i;
		}
		System.out.println(res+" ");
	}
    //(int n)形参列表 表示当前有一个形参n 可以接收用户输入
	public void cal02(int n)
	{
		System.out.println("please input n ");
		int res=0;
		for(int i=0;i<=n;i++)
		{
			res+=i;
		}
		System.out.println(res+" ");
	}
    
    //添加getsum方法 计算两个数之和
    //int 返回一个int值(res)
    //(int num1,int num2)可以接收两个数
    
    public int getsum(int num1,int num2)
	{
		int res=num1+num2;
		return res;   
    }
}
```





#### 方法调用机制（重要）



![image-20220824105425543](C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220824105425543.png)





#### 成员方法的定义



public 返回数据类型 方法名(**形参列表...**)

{方法体语句；

return 返回值；}

1.形参列表：表示成员方法输入cal(int n),getsum(int num1,int num2)

2.返回数据类型：表示成员方法输出 void表示没有返回值

3.方法主体：表示为了实现某一功能代码块

4.return 语句不是必须的



#### 注意事项和细节



##### **返回类型**

1.一个方法最多只有一个返回值【思考 如何返回多个结果 **返回数组**】

2.返回类型可以是任意类型 包含基本类型或引用类型(数组 对象)

3.如果方法要求有返回数据类型 则方法体中最后执行的语句必须为return值 而且要求返回值类型必须和return的值类型一致或兼容

4.如果方法是void 则方法中可以没有return



##### **形参列表**



1.一个方法可以有0个参数 也可以有多个参数 中间用逗号隔开 比如getsum

2.参数类型可以为任意类型 包含基本类型和引用类型 比如(printArr(int[ ] [ ]map))

3.调用带参数的方法时 一定要对应着参数列表传入相同类型或兼容类型的参数

4.方法**定义时的参数**称为形式参数 简称**形参** 方法**调用传入的参数**称为实际参数 简称**实参** 

实参和形参的类型要一致或兼容  个数 顺序必须一致



##### **方法体**

方法体里面不能嵌套定义方法！(即方法不能嵌套定义)



##### 方法调用

1.同一个类中的方法调用 直接调用即可 比如print(参数)；

2.跨类中的方法A类调用B类方法 需要通过对象名调用 比如 对象名.方法名(参数)；



```java
public class Method03
{
	public static void main(String[]args)
	{
		A a=new A();
		a.m1();//注意代码执行顺序
	}
}
class A
{
	public void m1()//通过A类中m1方法调用B类
	{
		System.out.println("m1() go...");
		B b=new B();
		b.hi();
		System.out.println("m1() on...");
	}
}
class B
{
	public void hi()
	{
		System.out.println("hi!");
	}
}

```



![image-20220824155419920](C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220824155419920.png)





#### 成员方法传参机制



##### 基本数据类型的传参机制



```java
public class Method04
{
	public static void main(String[]args)
	{	
		int a=10;
		int b=20;
		A a1 = new A();
		a1.swap(a,b);
		System.out.println(" a="+a+"b="+b);//回到主方法后仍然时10 和 20
	}

}

class A
{

	public void swap(int a,int b)
	{
		System.out.println("1 a="+a+"b="+b);
		int temp=a;
		a=b;
		b=temp;
		System.out.println("2 a="+a+"b="+b);
	}
}
```



![image-20220824165126374](C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220824165126374.png)





**a1.swap(a,b);传入的a和b赋值给swap栈中的a和b 交换也是交换swap栈中的a和b而不是main方法中的a和b**

**在方法中调用其他方法开辟新的栈 这两个栈是独立的空间**

**结论：基本数据类型 传的是值(值拷贝) 形参的任何改变不影响实参**



##### 引用类型的传参机制

```java
public class Method05
{
	public static void main(String[]args)
	{	
		B b=new B();
		int[] arr={1,2,3};
		b.test100(arr);
		System.out.println("main--------");
		for(int i=0;i<arr.length;i++)
		{
			System.out.print(arr[i]+" ");

		}
		System.out.println();
	}
}

class B
{
	public void test100(int[] arr)
	{
		arr[0]=200;
		System.out.println("test100--------");
		for(int i=0;i<arr.length;i++)
		{
			System.out.print(arr[i]+" ");

		}
		System.out.println();
	}

}
```



![image-20220824171206127](C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220824171206127.png)





**引用类型拷贝的是地址  数组arr/对象Person 在栈中存放的是地址 指向堆中的数据空间**

**因此在方法中调用其他方法 处理的是同一批数据**





#### 递归



##### 递归执行机制



![image-20220825105652404](C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220825105652404.png)





**为什么最上面的栈会逐级返回？**

**顶级栈在哪里调用返回到哪里**

**此时没有调用方法开辟新的空间** **在执行完这个空间代码后便会返回上一个栈**

若上一个栈有未执行的代码块 **则执行未执行的代码块**





![image-20220825151414445](C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220825151414445.png)



**if else是一个整体执行了if就不再执行else 因此这个代码块已经运行过 返回时不在运行**



![image-20220825162133312](C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220825162133312.png)



##### 递归重要规则



1.执行一个方法时 就创建一个新的受保护的独立空间（栈空间）

2.方法的局部变量是独立的 不会相互影响 比如n变量

3.如果方法中使用的引用类型变量（比如数组 对象）就会共享该引用类型的数据

4.递归必须向退出递归的条件逼近 否则就是无限递归 出现StackOverflowError

5.当一个方法执行完毕 或者遇到了return 就会返回 遵守谁调用 就将结果返回给谁

同时当方法执行完毕或者返回时 该方法也就执行完毕



##### 递归练习

###### 斐波那契数



![image-20220825163612159](C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220825163612159.png)

```java
public class Recursion
{
	public static void main(String[]args)
	{	

		T t1=new T();
		System.out.println("n=7 fibonaci number="+t1.fibonaci(7));
	}
}
class T
{
	public int fibonaci(int n)
	{
		if(n>=1)
		{
			if(n==1||n==2)
			{
				return 1;
			}
			else 
			{
				return fibonaci(n-2)+fibonaci(n-1);
			}
		}
		else
		{
			System.out.println("Wrong!");
			return -1;//要有返回值 不然报错
		}
	}
}
```



###### 猴子吃桃

![image-20220825163637615](C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220825163637615.png)



**思路分析**

1.day=10 有一个桃子

2.day=9 有（day10+1)*2=4

3.day=8 有（day9+1)*2=10

4.规律：前一天=（ 后一天+1 ）* 2

```java
import java.util.Scanner;
public class RecursionExercise
{
	public static void main(String[]args)
	{	
		System.out.println("please input day");
		Scanner myScanner=new Scanner(System.in);
		int day=myScanner.nextInt();
		Monkey m1=new Monkey();
		System.out.println("The day "+day+" number is "+m1.Peach(day));
	}
}

class Monkey

	public int Peach(int day)
	{
		if(day>=0&&day<=10)
		{	
			if(day==10)
			{
				return 1;
			}
			else
			{
				return (Peach(day+1)+1)*2;
			}
		}
		else
		{
			System.out.println("Wrong!");
			return -1;
		}
	}
}
```



###### 迷宫问题

![image-20220825165608366](C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220825165608366.png)





**思路**

1.先创建迷宫 用二维数组表示 int[ ] [ ]map=new int [8] [7] ;

2.规定map数组的元素值 ：0可以走 1表示障碍物

3.将最上面和下面的一行设置为1 最左边最右边为1



```java
public class MiGong
{
	public static void main(String[]args)
	{

		int[][]map=new int [8][7];
		for(int i=0;i<7;i++)
		{
			map[0][i]=1;
			map[7][i]=1;
		}

		for(int i=0;i<8;i++)
		{
			map[i][0]=1;
			map[i][6]=1;
		}
		map[3][1]=1;
		map[3][2]=1;
		for(int i=0;i<map.length;i++)
		{
			for(int j=0;j<map[i].length;j++)
			{
				System.out.print(map[i][j]+" ");
			}
			System.out.println();
		}
	}

		T t1=new T();
		t1.findway(map,1,1);
		System.out.print(" =========== ");
		for(int i=0;i<map.length;i++)
		{
			for(int j=0;j<map[i].length;j++)
			{
				System.out.print(map[i][j]+" ");
			}
			System.out.println();
		}
}	

class T
{
	//使用递归回溯的思想来解决老鼠出迷宫
	//1.findway方法就是专门来找出迷宫的路径
	//2.如果找到 就返回true 否则返回false
	//3.map就是二维数组 即表示迷宫
	//4.i j就是老鼠的位置 初始化的位置为（1，1）
	//5.因为是递归找路 先规定 map数组各个值的含义
	//   0表示可以走 1表示障碍物 2表示可以走 3表示走过但是是死路
	//6.当map[6][5]=2就表示找到通路 就可以结束 否则继续找
	//7.先确定老鼠找路的策略 下->右->上->左
    //8.策略不同的路线也不同
	public boolean findway(int [][]map,int i,int j)
	{

		if(map[6][5]==2)//说明已经找到
		{
			return true;
		}
		else
		{
			if(map[i][j]==0)//当前位置0 表示可以走
			{
				//假定能走通
				map[i][j]=2;
				//使用策略 来确定该位置是否真的能走通 下->右->上->左
				if(findway(map,i+1,j))//再次调用findway此时i变成i+1
				{
					return true;//退出
				}
				else if(findway(map,i,j+1))
				{
					return true;
				}
				else if(findway(map,i-1,j))
				{
					return true;
				}
				else if(findway(map,i,j-1))
				{
					return true;
				}
				else
				{
                      map[i][j]=3;
					return false;
				}

			}
            else
			{
				return false;
			}
		}
	}
}
```





![image-20220825174034102](C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220825174034102.png)





###### 汉诺塔





```java
public class HanoiTower
{
	public static void main(String[]args)
	{
		T t1=new T();
		t1.move(3,'A','B','C');
	}
}

class T
{

	public void move(int num,char a,char b,char c)
	{

		if(num==1)
		{
			System.out.println(a+"->"+c);
		}
		else
		{
			move(num-1,a,c,b);
			System.out.println(a+"->"+c);
			move(num-1,b,a,c);		
		}
	}
}
```



**不断进行判断 直到num=1再逐级返回 move(move(move...))结构**

**中间a b c不断变化** **可以看作是不断移塔**



![image-20220826164419536](C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220826164419536.png)



###### 八皇后









### 方法重载



**基本介绍**

java中允许同一个类中 多个同名方法的存在 但要求形参列表不一致！



**重载的好处**

1.减轻了起名的麻烦

2.减少了记名的麻烦



```java
public class MyCalculator
{
	public static void main(String[]args)
	{
		MyCalculator01 m1=new MyCalculator01();
		System.out.println(m1.calculator(1,2,3));


	}
}
class MyCalculator01
{

	public int calculator(int n1,int n2)
	{
		return n1+n2;
	}

	public double calculator(int n1,double n2)
	{
		return n1+n2;
	}

	public double calculator(double n1,int n2)
	{
		return n1+n2;
	}

	public int calculator(int n1,int n2,int n3)
	{
		return n1+n2+n3;
	}
}
```



#### 注意事项和使用细节



1.方法名必须相同

2.形参列表一定要不同（形参类型或个数或顺序，至少有一样不同 参数名无要求）

3.返回类型无要求



### 可变参数



**基本介绍**



java允许将同一个类中多个同名同功能但参数个数不同的1方法 封装成一个方法 就可以通过可变参数实现



**基本语法**

访问修饰符 返回类型 方法名（数据类型...形参名）{  }





```java

public class VarParameter01
{
	public static void main(String[]args)
	{
		ZzxMethod z1=new ZzxMethod();
		System.out.println(z1.sum(1,2,3));
	}

}

class ZzxMethod
{
	public int sum(int...nums)//nums相当于一个数组
	{
		int res=0;
		for(int i=0;i<nums.length;i++)
		{
			res+=nums[i];
		}
		return res;
	}
}


```



**注意事项**



1.可变参数的实参可以是0个或者任意多个

2.可变参数的实参可以是数组

3.可变参数的本质就是数组

4.可变参数和普通类型的参数一起放在形参列表 但必须保证可变参数在最后

5.一个形参列表只能出现一个可变参数



```java

public class VarParameter01
{
	public static void main(String[]args)
	{
		ZzxMethod z1=new ZzxMethod();
		System.out.println(z1.show("zzx",1,2,3));//方法调用返回到这
	}

}

class ZzxMethod
{
	public String show(String name,double...nums)
	{
		double total=0;
		for(int i=0;i<nums.length;i++)
		{
			total+=nums[i];
		}
		
		return name+" Totalscore= " +total;//将姓名和成绩拼接 返回一个字符串并没有输出
	}
}


```





### 作用域



1.在java中 主要的变量就是属性（成员变量）和局部变量

2.我们说的局部变量一般是指在成员方法中定义的变量【举例Cat类：cry】

3.java中作用域的分类

全局变量：也就是属性 作用域为整个类体Cat类：cry eat等方法使用属性

局部变量：除了属性以外的变量 作用域在他的代码块中

4.全局变量可以不赋值 直接使用 因为有默认值 **局部变量必须赋值后才能使用** 因为没有默认值



**注意事项和细节使用**



1.属性和局部变量可以重名 访问时遵循**就近原则**

2.在同一个作用域中 比如在同一个成员方法中 两个局部变量 **不能重名**

3.属性生命周期较长 伴随着对象的创建而创建 伴随着对象的销毁而销毁 

局部变量 生命周期较短 伴随着他的代码块的执行而创建 伴随着代码块的结束而死亡 即在一次方法调用过程中

4.作用域范围不同

全局变量/属性：可以被本类使用 或其他类使用

局部变量：只能在本类中对应的方法中使用

5.修饰符的不同

全局变量/属性可以加修饰符

**局部变量不可以加修饰符**



### 构造器



需求：前面我们在创建人类对象时 是先把一个对象创建好后 再给它的年龄和姓名属性赋值 如果我现在要求 

在创建人类对象时 就直接指定这个对象的年龄和姓名 这时候就可以使用构造器



**基本语法**



[修饰符]方法名(形参列表)

{  方法体；   }



1.构造器的修饰符可以默认 也可以是public protected private

2.构造器**没有返回值**

3.方法名 和类名字必须一样

4.参数列表和成员方法一样的规则

5.构造器的调用由系统完成



**基本介绍**



构造方法又叫构造器 是类的一种特殊的方法 他的主要作用是完成对**新对象的初始化** 它有几个特点

1.方法名和类名相同

2.没有返回值

3.在创建对象时 系统会自动的调用该类的构造器**完成对对象的初始化**



**注意事项和使用细节**



1.一个类可以有定义多个不同的构造器 即**构造器重载**

2.构造器名和类名要相同

3.**构造器没有返回值**

4.构造器是**完成对象的初始化** **不是创建对象**  **new Person是创建对象并赋默认值 （）里的才是调用构造器进行初始化**

5.在创建对象时 **系统会调用**该类的构造方法

6.**如果程序员没有定义构造器 系统会自动给类生成一个默认的无参构造器（也叫默认构造器）比如Person(){}使用javap指令 反编译看看**

7.**一旦定义了自己的构造器 默认的构造器就覆盖了** **就不能再使用默认的无参构造器 除非显式的定义一下 即:Person(){}**





**练习**





<img src="C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220829143549472.png" alt="image-20220829143549472" style="zoom: 80%;" />

```java
public class ConstructorExercise01
{
	public static void main(String[]args)
	{

		Person p1=new Person();
		System.out.println("name: "+p1.name+" age: "+p1.age);
		Person p2=new Person("wjh",19);
		System.out.println("name: "+p2.name+" age: "+p2.age);
	}
}

class Person
{
	String name;
	int age;
	public Person()
	{
		age=18;

	}

	public Person(String pName,int pAge)
	{
		name=pName;
		age=pAge;
	}
}
```





![image-20220829143631283](C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220829143631283.png)





### 对象创造的流程分析



<img src="C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220829160557291.png" alt="image-20220829160557291" style="zoom: 50%;" />

流程分析（面试题）

1.加载Person类信息（Person.class ），只会加载一次

2.在堆中分配空间（地址）

3.完成对象初始化【3.1 默认初始化 age=0;name=null; 3.2显式初始化 age=90,name=null;

3.3构造器的初始化 age=20,name=小倩;





### this关键字



```java
public class this01
{
	public static void main(String[]args)
	{
		Dog d1=new Dog("wjh",18);
		d1.info();
	}
}
class Dog
{
	String name;
	int age;
	public Dog(String dName,int dAge)
	{
		name=dName;
		age=dAge;
	}
	public void info()
	{
		System.out.println(name+"\t"+age+"\t");
	}
}
```

想要将构造器中的形参写成属性名 但是出现了一个问题 根据变量的作用域原则

构造器的name和age是局部变量而不是属性





**this本质**



Java虚拟机会给每个对象分配this 代表当前对象

**哪个对象调用 this就代表哪个对象**

<img src="C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220829162837834.png" alt="image-20220829162837834" style="zoom: 66%;" />

```java
public class this01
{
	public static void main(String[]args)
	{
		Dog d1=new Dog("wjh",18);
		d1.info();

	}
}

class Dog
{
	String name;
	int age;

	public Dog(String name,int age)
	{
        //this.name就是当前对象属性name
        //当前对象就是谁在调用构造器 this就指向哪个对象(d1)
		this.name=name;
		this.age=age;
	}


	public void info()
	{
		System.out.println(name+"\t"+age+"\t");
	}
}
```





**this的注意事项和细节**



1.this关键字可以用于访问本类的属性 方法 构造器

2.this用于区分当前类的属性和局部变量

3.访问成员方法的语法：this.方法名(参数列表)

4.访问构造器语法：**this(参数列表)**  **注意只能在构造器中使用 **  **即只能在构造器中访问另一个构造器**

**访问构造器语法**：this(参数列表)；**必须放置第一条语句**

5.**this不能在类定义的外部使用 只能在类定义的方法中使用**





定义 Person 类，里面有 name、age 属性，并提供 compareTo 比较方法，用于判断是否和另一个人相等，提供测试类 TestPerson 用于测试, 名字和年龄完全一样，就返回 true, 否则返回 false 

代码

```java
 public class TestPerson
 { //编写一个 main 方法 
 	public static void main(String[] args) 
 	{ 
        Person p1 = new Person("mary", 20);
	    Person p2 = new Person("mary", 20); 
		 System.out.println("p1 和 p2 比较的结果=" + p1.compareTo(p2)); 
    } 
 } 
 /* 定义 Person 类，里面有 name、age 属性，并提供 compareTo 比较方法， 用于判断是否和另一个人相等，提供测试类 TestPerson 用于测试, 名字和年龄完全一样，就返回 true, 否则返回 false */

 class Person { String name; int age; //构造器 
 	public Person(String name, int age)
 	{
        this.name = name; this.age = age;
        
    } //compareTo 比较方法
               
 public boolean compareTo(Person p) 
 { //名字和年龄完全一样 // 
	 if(this.name.equals(p.name) && this.age == p.age)//this这里指p1
	 {
         // return true; // } else { // return false; // }
         
         return this.name.equals(p.name) && this.age == p.age; 
     } 
 }


```





### 本章练习



![image-20220831090110003](C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220831090110003.png)













![image-20220831090319735](C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220831090319735.png)



```java
public class Homework01
{
	public static void main(String[]args)
	{
		A01 a=new A01();
		double[]arr={};
		Double res=a.max(arr);
		if(res!=null)//判断数组长度是否正常
		{
			System.out.println("MAX= "+a.max(arr));
		}
		else
		{
			System.out.println("Wrong!!!");
		}
	}
}

class A01
{

	public Double max(double[]arr)//Double为一个包装类 null可以返回给Double类
	{

		if(arr.length>0)
		{
			double max=arr[0];
			for(int i=1;i<arr.length;i++)
			{
				if(arr[i]>max)
				{
					max=arr[i];
				}

			}
			return max;
		}
		else
		{
			return null;
		}
	}
}
```





![image-20220831092510140](C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220831092510140.png)



```java
public class Homework02
{
	public static void main(String[]args)
	{
		String []arr={"zzx","wjh","wly","xmj"};
		A02 a=new A02();
		int index=a.find("wjh",arr);
		if(index==-1)
		{
			System.out.println("NULL");
		}
		else
		{
			System.out.println("Index= "+index);
		}
	}
}

class A02
{

	public int find(String findstr,String[]arr)
	{
		for(int i=0;i<arr.length;i++)
		{
			if(findstr.equals(arr[i]))
			{
				return i;
			}
		}
				return -1;	
	}
}

```





![image-20220831093713277](C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220831093713277.png)



```java
public class Homework03
{
	public static void main(String[]args)
	{
		Book b=new Book("wjh",300);
		b.info();
		b.updatePrice();
		b.info();
	}
}

class Book
{
	String name;
	double price;
	public Book(String name,double price)
	{
		this.name=name;
		this.price=price;
	}
	public void updatePrice()
	{
		if(this.price>150)
		{
			this.price=150;
		}

		else if(this.price>150)
		{
			this.price=100;
		}
	}
	public void info()
	{
		System.out.println("name= "+this.name+"  price= "+this.price);
    }
}
```







## 面向对象中级



### IDEA使用





<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220902160424438.png" alt="image-20220902160424438" style="zoom:67%;" />

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220902160758957.png" alt="image-20220902160758957" style="zoom:70%;" />

<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220902161459670.png" alt="image-20220902161459670" style="zoom:67%;" />





模板：
Setting-Editor-LiveTemplates





### 包





**引出**

两个程序员共同开发一个项目 两个人定义了同一个类名 怎么办



**包的三大作用**

1.区分很多相同名字的类

2.当类很多时 可以很好的管理类（看Java API文档）

3.控制访问范围



**包基本语法**



**package com.hspedu**

说明：package是关键字 表示打包

hspedu表示包名



**包的本质分析**



**包的本质就是创建不同文件夹来保存类文件 画出示意图**



![image-20220902233101523](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220902233101523.png)



**注意事项**



![image-20220902233121162](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220902233121162.png)





![image-20220902233138305](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220902233138305.png)



1.package的作用是声明当前类所在包 需要放在类的最上面 一个类最多只有一句package

2.import指令位置放在package的下面 在类定义前面 可以有多句且**没有顺序要求**



### 访问修饰符



**基本介绍**

java提供四种访问控制修饰符号 用于控制方法和属性（成员变量）的访问权限（范围）

1.**公开级别**：用public修饰 对外公开

2.**受保护级别**：用protected修饰 对子类和同一个包中的类公开

3.**默认级别**：没有修饰符号 向同一个包的类公开

4.**私有级别**：用private修饰 只有类本身可以访问 不对外开放



#### 四种访问修饰符的访问范围（重要）



<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220903084259655.png" alt="image-20220903084259655" style="zoom:150%;" />



**注意这里的子类时不同包的子类**



**使用的注意事项**

1.修饰符可以用来修饰类中的**属性** **成员方法**以及**类**

2.只有默认的和public才能修饰类

3.成员方法的访问规则和属性完全一样







### 封装



封装就是把抽象出来的数据（属性）和对数据的操作（方法）封装在一起 数据被保护在内部

程序的其他部分只有通过被授权的操作（方法） 才能对数据进行操作



#### **封装的理解和好处**

1.隐藏实现细节：方法（连接数据库）<--调用（传入参数）

2.可以对数据进行验证 保证安全合理



#### 封装的具体步骤



1.将属性私有化private(不能直接修改属性)

2.提供一个公共的（public）set方法 用于对属性进行判断并赋值

public void setxxx(类型 参数名){//xxx表示某个属性

//加入数据的验证的业务逻辑

属性=参数名；

}

3.

提供一个公共的（public）get方法 用于获取属性的值public数据类型getxxx()

{

//权限判断 xxx是某个属性

return  xx;

}



#### 练习



**<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220903180330886.png" alt="image-20220903180330886" style="zoom:80%;" />**



```java
package com.zzx.encap;

public class AccountTest {
    public static void main(String[] args) {
        Account a1=new Account();
        a1.setName("万佳惠");
        a1.setBalance(66666);
        a1.setKey("666666");
        a1.info();
    }
}
package com.zzx.encap;

public class Account {
    private String name;
    private int balance;
    private String key;

    public Account() {
    }

    public Account(String name, int balance, String key) {
        this.setName(name);
        this.setBalance(balance);
        this.setKey(key);
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        if (name.length() >= 2 && name.length() <= 4) {
            this.name = name;
        } else {
            System.out.println("请输入长度2-4的姓名");
            this.name="无名";
        }
    }

    public int getBalance() {
        return balance;
    }

    public void setBalance(int balance) {
        if (balance >= 20) {
            this.balance = balance;
        } else {
            System.out.println("请输入大于18的年龄");
            this.balance = 0;
        }
    }


    public String getKey() {
        return key;
    }

    public void setKey(String key) {
        if (key.length() == 6) {
            this.key = key;
        } else {
            System.out.println("请输入六位数的密码");
            this.key = "000000";
        }
    }
    public void info()
    {
        System.out.println("信息为： name="+name+"  balance="+balance+"  key="+key);
    }
}

```





### 继承



我们编写了两个类 一个是pupil类（小学生） 一个是graduate（研究生）

问题：两个类的属性和方法很多事相同的 怎么办

解决方案：继承=>解决代码复用问题



**继承基本介绍**

继承可以解决代码复用 当多个类存在相同的属性和方法时 可以从这些方法中抽象出父类 在父类中定义这些相同的属性和方法

所有的子类不需要重新定义这些属性和方法 只需要通过 extend来声明继承父类即可



**继承的基本语法**

class 子类 extends父类

{}

1.子类就会自动拥有父类定义的属性和方法

2.父类又叫超类 基类

3.子类又叫派生类



#### 继承原理图



<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220904104519757.png" alt="image-20220904104519757" style="zoom:90%;" />





#### 继承细节



1.子类继承了所有属性和方法 **非私有的属性和方法可以在子类直接访问**

 但是私有属性和方法不能在子类直接访问 要**通过父类提供的公共方法**访问

2.**子类必须调用父类的构造器 完成对父类的初始化**

3.当创建子类对象时 **不管使用子类的哪个构造器 默认情况总会调用父类的无参构造器**

如果父类没有提供无参构造器 则必须在子类的构造器中用super**[super("zzx",18)]**去指定使用

父类的哪个构造器**完成对父类的初始化工作** 否则编译不会通过

4.如果希望指定去调用父类某个构造器 则**显式**的调用一下

5.super在使用时 需要放在构造器**第一行**（super只能在构造器中使用）

6.**super( )和this( )都只能放在构造器第一行 因此这两个方法不能共存在一个构造器**//注意this后的括号

7.Java所有的类都是object类的子类

8.父类构造器的调用不限于直接父类！将一直往上追溯到object类（顶级父类）

9.子类最多只能继承一个父类（指直接继承）即java中是单继承机制

如何让A类继承B类和C类？【A继承B B继承C】

10.不能滥用继承 子类和父类必须满足is-a的逻辑关系



#### 继承的本质分析（重要）



**继承的本质就是建立查找关系**

![image-20220904163552603](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220904163552603.png)







```java
System.out.println(son.name);
```

要按照查找关系来返回信息

（1）首先看子类是否有该属性

（2）如果子类有该属性 并且可以访问 则返回信息

（3）如果子类没有这个属性  就看父类有没有这个属性（如果有 并且可以访问 则返回 若无则重复（3）步骤



#### 继承练习



![image-20220904170424075](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220904170424075.png)





![image-20220904170456353](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220904170456353.png)





```java
package com.zzx.extend;

public class ExtendExercise03 {
    public static void main(String[] args) {
        PC p1=new PC("AMD",16,500,"ASUS");
        p1.printinfo();

        Notepad n1=new Notepad("inter",8,1000,"Lenvo");
        n1.printInfo();

    }
}

package com.zzx.extend;

public class PC extends Computer{
    private String brand;

    public PC(String cpu, int memory, int disk, String brand) {
        super(cpu, memory, disk);
        this.brand = brand;
    }

    public String getBrand() {
        return brand;
    }

    public void setBrand(String brand) {
        this.brand = brand;
    }

    public void printinfo()
    {
        System.out.println("PC信息：");
        System.out.println(getDetail()+" brand "+brand);//利用父类的getDetail方法得到相关属性信息
    }

}

package com.zzx.extend;

public class Notepad extends Computer{
    private String color;

    public Notepad(String cpu, int memory, int disk, String color) {
        super(cpu, memory, disk);
        this.color = color;
    }

    public String getColor() {
        return color;
    }

    public void printInfo()
    {
        System.out.println("Notepad信息：");
        System.out.println(getDetail()+" color: "+color);
    }


    public void setColor(String color) {
        this.color = color;
    }
}

```



### super关键字



基本介绍：super代表父类的引用 用于访问父类的属性，方法，构造器



**基本语法**：



1.访问父类的属性 但不能访问父类private的属性和方法 super.属性名； super.方法名（参数列表）；

2.访问父类的构造器 super（参数列表）；**只能在构造器中使用 只能放在构造器的第一句** 只能出现一句



**super给编程带来的好处**



1.调用父类的构造器的好处（分工明确，父类属性由父类初始化，子类的属性由子类初始化）

2.当子类中有和父类中的成员（属性和方法）重名时，为了访问父类的成员 必须通过super

如果没有重名 使用super  this  直接访问时一样的效果

3.super的访问不限于父类 如果爷爷类和本类中有同名的成员 也可以使用super去访问爷爷类的成员

如果多个基类（上级类）中都有同名的成员 使用super访问遵循就近原则 



**查找顺序**

this./直接访问：(1)先找本类 如果有 则调用 (2)如果没有 则找父类 (3)如果父类没有 则继续找父类

如果查找过程中 找到了但是不能访问 则报错   没有找到  提示该方法不存在



super. ：直接查找父类 其他规则一样



![image-20220905091128577](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220905091128577.png)





### 方法重写



**基本介绍**

方法覆盖（重写）就是子类有一个方法 和父类的某个方法的名称 返回类型 参数一样 那么我们就说子类的这个方法覆盖了父类的方法



**重写的作用**

重写是为了增强类的重用性和复用性，扩展性；

重写是对类中方法的扩充，因为继承用的是父类的东西，重写则不仅得到父类的东西，同时也加入了自己的东西，两全其美。



**注意事项及使用细节**



1.子类的方法的参数 方法名称 要和父类的参数 方法名称完全一样

2.子类方法的返回类型和父类的返回类型一样 或者父类返回类型的子类

比如 父类 返回类型是Object 子类的方法返回类型是String  //String的返回类型是Object的子类

3.子类方法不能缩小父类方法的访问权限   public>protected>默认>private



#### 方法重载与方法重写





![image-20220905094940905](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220905094940905.png)





**重载因为在本类所以对修饰符无要求**



**重写练习**



![image-20220905101328501](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220905101328501.png)







```java
package com.override;

public class overrideExercise {
    public static void main(String[] args) {
        Person p1=new Person("wjh",19);
        System.out.println(p1.say());
        Student s1=new Student("zzx",18,2021214965,100);
        System.out.println(s1.say());


    }
}

package com.override;

public class Person {

    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public String say()
    {
        return "name: "+name+" age: "+age;
    }
}

package com.override;

public class Student extends Person{
    private int id;
    private int score;

    public Student(String name, int age, int id, int score) {
        super(name, age);
        this.id = id;
        this.score = score;
    }

    public String say()
    {
        return super.say()+" id: "+id+" score: "+score;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public int getScore() {
        return score;
    }

    public void setScore(int score) {
        this.score = score;
    }


}

```





### 多态



**多态基本介绍**

方法或对象具有多种形态 是面向对象的第三大特征 多态是建立在封装和继承基础之上的





#### 1.方法的多态

重写和重载体现多态

例如：

这里传入不同的参数 就会调用不同的sum方法 就体现多态

System.out.print(a.sum(10,20));

System.out.print(a.sum(10,20,30));



#### 2.对象的多态  （重点）



**重要的几句话**

**（1)一个对象的编译类型（javac)和运行类型(java)可以不一致**

**Animal animal = new Dog();【animal的编译类型是Animal 运行类型Dog】**

**animal = new Cat();【animal的运行类型变成了Cat 编译类型仍然是Animal】**

**（2）编译类型在定义对象时 就确定了 不能改变**

**（3）运行类型时可以变化的**

**（4）编译类型看定义时 = 号的左边 运行类型看=号的右边**



**多态的好处**

通过父类对象能够只指向（接收）子类对象 减少很多子类代码复用

需要使用时 只需要用父类接收即可 



#### 多态注意事项和细节



多态的前提是 ：两个对象（类）存在继承关系



**多态的向上转型**

（1）本质：父类的引用指向了子类的对象

（2）语法：父类类型  引用名 = new 子类类型( );  Animal animal = new Cat();

（3）特点： 可以调用父类中的所有成员（需遵循访问权限）不能调用子类中特有成员；

​					最终效果看子类的具体实现！即调用方法时 从子类（运行类型）开始查找

​					方法调用规则和前面一致（一直找父类 直到找到为止）



**多态的向下转型**



（1）语法：子类类型  引用名 = （子类类型） 父类引用；Cat cat=(Cat) animal;

​		将animal强转为Cat **相当于再创建了个对象指向Cat**

（2）**只能强转父类的引用 不能强制父类的对象**

（3）要求父类的引用必须指向的是当前目标类型的对象

（4）当向下转型后 可以调用子类类型中所有的成员



属性没有重写之说 **属性的值看编译类型**

**编译看左 运行看右**

**属性看编译 方法看运行**（实际指向哪个空间）

instanceof比较操作符 用于判断**对象的运行类型**是否为**XX类型**或XX类型的**子类型**【举例说明】



```java
package com.Poly;

public class PolyDetail {
    public static void main(String[] args) {
        B b = new B();
        System.out.println(b instanceof B);//true
        System.out.println(b instanceof A);//true

        //a编译类型A 运行类型B
        A a=new B();
        System.out.println(a instanceof A);//true
        System.out.println(a instanceof B);//true


    }

}

class A{}

class B extends  A{}

```







#### 练习



![image-20220905172249725](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220905172249725.png)





#### java的动态绑定机制（非常非常重要）





![image-20220906102805266](C:\Users\QQ星⭐\AppData\Roaming\Typora\typora-user-images\image-20220906102805266.png)



方法看运行  运行类型为B( ); 因此结果分别为40 30



**java的动态绑定机制**



**1.当调用对象方法时 该方法会和该对象的内存地址/运行类型绑定**

**2.当调用对象属性时 没有动态绑定机制 哪里声明哪里使用**



```java


public class DynamicBinding {
    public static void main(String[] args) {
        //a 的编译类型 A, 运行类型 B
        A a = new B();//向上转型
        System.out.println(a.sum());//?40 -> 30
        System.out.println(a.sum1());//?30-> 20
    }
}

class A {//父类
    public int i = 10;
    //动态绑定机制:

    public int sum() {//父类sum()
        return getI() + 10;}//20 + 10  getI()调用的是子类getI()
    //调用方法时 和该对象的地址/运行类型即B类进行绑定

    public int sum1() {//父类sum1()
        return i + 10;//10 + 10
        //属性没有动态绑定机制 哪里声明用哪里的 执行当前类的属性 即i为本类的i
    }

    public int getI() {//父类getI
        return i;
    }
}

class B extends A {//子类
    public int i = 20;

//    public int sum() {
//        return i + 20;
//    }

    public int getI() {//子类getI()
        return i;
    }

//    public int sum1() {
//        return i + 10;
//    }
}

```





#### 多态的应用



##### 多态数组



![image-20220906105424847](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220906105424847.png)



```java
package com.Poly.polyarr;

public class PolyArray {
    public static void main(String[] args) {
        //父类的引用可以指向子类的对象
        Person[] persons = new Person[5];
        persons[0] = new Person("wjh",19);
        persons[1] = new Student("zzx",18,100);
        persons[2] = new Student("wly",19,99);
        persons[3] = new Tencher("hsp",35,20000);
        persons[4] = new Tencher("xmj",50,25000);

        //遍历数组
        for (int i = 0;  i< persons.length ; i++) {
            System.out.println(persons[i].say());
            // persons[i]编译类型时Person 运行类型根据实际情况由JVM调用

            //类型判断加向下转型
            if(persons[i] instanceof Student){//判断persons[i]是不是Student
                Student student=(Student)persons[i];
                student.study();
                //简化为：((Student)persons[i]).study();
            }
            else if(persons[i]instanceof Tencher){
                Tencher tencher=(Tencher) persons[i];
                tencher.teach();
            }
            else if(persons[i] instanceof Person){
                
            }
            else{
                System.out.println("类型有误！");
            }
        }

    }
}

```



```java
package com.Poly.polyarr;

public class Person {
    private String name;
    private int age;

    public Person(String name, int age) {
        this.name = name;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public String say(){
        return name+age;
    }
}

```



```java
package com.Poly.polyarr;

public class Student extends Person {

    private double score;

    public Student(String name, int age, double score) {
        super(name, age);
        this.score = score;
    }

    public double getScore() {
        return score;
    }

    public void setScore(double score) {
        this.score = score;
    }

    @Override
    public String say() {
        return super.say() + " socre: " + score;
    }

    public void study() {
        System.out.println("学生" + getName() + " 正在学java...");
    }
}

```



```java
package com.Poly.polyarr;

public class Tencher extends Person{
    private  double salary;

    public Tencher(String name, int age, double salary) {
        super(name, age);
        this.salary = salary;
    }

    public double getSalary() {
        return salary;
    }

    public void setSalary(double salary) {
        this.salary = salary;
    }

    @Override
    public String say() {
        return super.say()+" salary: "+salary;
    }

    public void teach(){
        System.out.println("老师 "+getName()+ "正在上课");
    }
}

```



##### 多态参数



方法定义的形参类型为父类类型 实参类型允许为子类类型



![image-20220906121637247](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220906121637247.png)





```java
package com.Poly.polyparameter;

public class Test {
    public static void main(String[] args) {
        Worker wjh = new Worker("wjh", 2500);
        manager zzx = new manager("zzx", 5000, 200000);
        Test t=new Test();//创建类对象调用show()函数
        t.show(wjh);
        t.show(zzx);
        t.testwork(wjh);
        t.testwork(zzx);
    }
    public void show(Emplotee e){
        System.out.println(e.getAnnual());
    }
    public void testwork(Emplotee e){
        if(e instanceof  Worker){//判断对象e是否属于Worker
            ((Worker) e).work();
        }
        else if (e instanceof  manager)
        {
             ((manager) e).manage();
        }
        else{
            System.out.println("NULL");
        }
    }
}

package com.Poly.polyparameter;

public class Emplotee {
    private String name;
    private  double salary;

    public Emplotee(String name, double salary) {
        this.name = name;
        this.salary = salary;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public double getSalary() {
        return salary;
    }

    public void setSalary(double salary) {
        this.salary = salary;
    }

    //得到年工资的方法
    public double getAnnual(){
        return 12*salary;
    }
}

package com.Poly.polyparameter;

public class Worker extends Emplotee{

    public Worker(String name, double salary) {
        super(name, salary);
    }

    public void work(){
        System.out.println("普通员工 "+getName()+ "working...");
    }

    @Override
    public double getAnnual() {//普通员工没有奖金
        return super.getAnnual();
    }
}

package com.Poly.polyparameter;

public class manager extends Emplotee {
    public double bonus;

    public manager(String name, double salary, double bonus) {
        super(name, salary);
        this.bonus = bonus;
    }

    public double getBonus() {
        return bonus;
    }

    public void setBonus(double bonus) {
        this.bonus = bonus;
    }

    public void manage() {
        System.out.println("manager" + getName() + " managing...");
    }

    @Override
    public double getAnnual() {
        return super.getAnnual() + bonus;
    }

}
```







### 如何查看源码

光标停在方法上 按 CTRL+B



### Object类



![image-20220906170402558](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220906170402558.png)



#### equals方法



##### ==和equals的对比



**==是一个比较操作符**

1.==：既可判断基本类型 又可判断引用类型

2.==：如果判断基本类型 判断的是值是否相等

3.==：如果判断引用类型 判断的是地址是否相等 即判断的是不是同一个对象



**equals方法**



4.equals：是Object类中的方法 只能判断引用类型

5.默认判断的是地址是否相等 子类中往往重写该方法 用于判断内容是否相等。

比如Integer，String【看看String和Integer的equals的源代码】

String已经重写了equals 判断两个字符串是否相同



**Object的equals方法**

默认判断比较对象地址是否相等 即两个对象是不是同一个对象



**Integer的equals方法**

重写了Object的equals方法 变成了判断两个值是否相等



**equals练习**



**如何重写equals方法**



练习一：判断两个对象的属性是否相同

```java
package com.use;

public class Test {
    public static void main(String[] args) {
        Person person1 = new Person("wjh", 19, '女');
        Person person2= new Person("wjh", 19, '女');

        System.out.println(person1.equals(person2));
        //未重写时 是Object中的类 object中的equals判断两个对象是否相同


    }
}
class Person{
    private String name;
    private int age;
    private char gender;

    //重写equals方法
    public boolean equals (Object obj){
        if(this==obj){
            return true;//相同对象返回真
        }
        //类型判断
        if(obj instanceof Person){//是Perosn类才比较
            //进行向下转型 取得该对象的属性
            Person p=(Person)obj;
            return this.name.equals(p.name)&&this.age==p.age&&this.gender==p.gender;
        }
        return false;//不是Person类则直接返回false;
    }

    public Person(String name, int age, char gender) {
        this.name = name;
        this.age = age;
        this.gender = gender;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public char getGender() {
        return gender;
    }

    public void setGender(char gender) {
        this.gender = gender;
    }
}

```





```java
public class EqualsExercise02 {
    public static void main(String[] args) {

        Person_ p1 = new Person_();
        p1.name = "hspedu";

        Person_ p2 = new Person_();
        p2.name = "hspedu";

        System.out.println(p1==p2); //False ==判断引用类型看是不是同一个对象
        System.out.println(p1.name .equals( p2.name));//T  p1.name是字符串 已经重写了 判断的是字符是否相等
        System.out.println(p1.equals(p2));//False p1是对象 属于Object类 判断是否为同一对象

        String s1 = new String("asdf");

        String s2 = new String("asdf");
        System.out.println(s1.equals(s2));//T  s1是String类型 已经重写 判断的是字符是否相等
        System.out.println(s1==s2); //F  ==判断引用类型是否为同一对象

    }
}

class Person_{//类
    public String name;
}

```







![image-20220907080425147](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220907080425147.png)







#### hashcode



![image-20220907081203110](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220907081203110.png)

1.提高具有哈希结构的容器的效率

2.两个引用 如果指向的是同一个对象 则哈希值肯定是一样的

3.两个引用 如果指向的是不同对象 则哈希值是不一样的

4.哈希值主要根据地址号来的 不能完全将哈希值等价于地址

5.后面在集合中hashcode如果需要的话 也需要重写



```java
package com.Object;

public class HashCode_ {
    public static void main(String[] args) {

        AA aa = new AA();
        AA aa2 = new AA();
        System.out.println(aa.hashCode());
        System.out.println(aa2.hashCode());

        AA aa3 = aa;
        System.out.println(aa3.hashCode());

    }
}
class AA{}
```



![image-20220907081608782](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220907081608782.png)



#### toString方法



**基本介绍**

默认返回：全类名+@+哈希值的十六进制【查看Object的toString方法】

子类往往重写toString方法 用于返回对象的属性信息



重写toString方法 打印对象或拼接对象时 都会自动调用该对象的toString形式



当直接输出一个对象时 toString方法会被默认调用



**![image-20220907082324657](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220907082324657.png)**





#### finalize

在实际开发中几乎不用 更多的是为了面试

1.当对象被回收时 系统自动调用该对象的finalize方法 子类可以重写该方法 做一些释放资源的操作

2.什么时候被回收：当某个对象没有任何引用时 则jvm就认为这个对象是一个垃圾对象 就会使用垃圾回收机制来销毁该对象

在销毁该对象之前 会先调用finalize方法

3.垃圾回收机制的调用 是由系统决定(即有自己GC的算法) 也可以通过System.gc( )主动触发垃圾回收机制



```java
package com.Object;

public class Finalize {
    //演示finalize的使用
    public static void main(String[] args) {

        Car car1 = new Car("宝马");
        car1=null;//此时对象空间就是一个垃圾，垃圾回收器就会回收销毁对象前会调用该对象的finalize方法
        //程序员可以在finalize中 写自己的业务逻辑代码(比如释放资源：数据库连接 或者打开文件..)
        //如果程序员不重写 那么就会调用Object类的finalize 即默认处理
        //如果重写了 则可以实现自己的业务逻辑
        System.gc();
        System.out.println("程序退出...");
    }
}
class Car{
    private String name;

    public Car(String name) {
        this.name = name;
    }

    //重写finalize

    @Override
    protected void finalize() throws Throwable {
        System.out.println("delete Car..."+name);
        System.out.println("释放了资源...");
    }

}
```



### 断点调试





![image-20220907092205007](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220907092205007.png)





#### 断点调试的快捷键



F7（跳入） F8（跳过） shift + F8（跳出） F9（resume，执行到下一个断点）

F7：跳入方法内

F8：逐行执行代码

shift + F8:跳出方法





![image-20220907103555535](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220907103555535.png)



### 本章练习



![image-20220907201311413](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220907201311413.png)



```java
package com.Homework;

public class Homework01 {

    public static void main(String[] args) {
         Person []persons=new Person[3];//创建对象数组
         persons[0] = new Person("wjh", 19, "English");
         persons[1] = new Person("zzx", 18, "Computer");
         persons[2] = new Person("wly", 17, "broadcast");

        Person tmp=null;
        for (int i = 0; i < persons.length-1; i++) {
            for(int j=0;j< persons.length-1-i;j++){

                if(persons[j].getAge()>persons[j+1].getAge()){
                    tmp=persons[j];
                    persons[j]=persons[j+1];
                    persons[j+1]=tmp;
                }
            }
        }
        for (int i = 0; i < persons.length; i++) {
            System.out.println(persons[i]+"\t");
        }
    }
}

class Person {
    private String name;
    private int age;
    private String job;

    public Person(String name, int age, String job) {
        this.name = name;
        this.age = age;
        this.job = job;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public String getJob() {
        return job;
    }

    public void setJob(String job) {
        this.job = job;
    }
    //public  int[] Arraylist(int []persons){}//注意这一行的格式

    @Override
    public String toString() {//需要重写toString
        return "Person{" +
                "name='" + name + '\'' +
                ", age=" + age +
                ", job='" + job + '\'' +
                '}';
    }
}
```



![image-20220907211509909](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220907211509909.png)





```java
package com.Homework;

public class Homework03 {
    public static void main(String[] args) {

        Professor p1=new Professor("wjh",19,"英语老师",100000,1.3);
        Professor2 p2=new Professor2("zzx",18,"混子",10000,1.2);
        p1.introduce();
        p2.introduce();
    }


}

class Teach{
    private String name;
    private int age;
    private String post;
    private double salary;

    private double grade;

    public Teach(String name, int age, String post, double salary,double grade) {
        this.name = name;
        this.age = age;
        this.post = post;
        this.salary = salary;
        this.grade=grade;
    }

    public double getSalary() {
        return salary;
    }

    public void setSalary(double salary) {
        this.salary = salary;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public String getPost() {
        return post;
    }

    public void setPost(String post) {
        this.post = post;
    }

    public double getGrade() {
        return grade;
    }

    public void setGrade(double grade) {
        this.grade = grade;
    }

    public void introduce(){
        System.out.println("老师姓名为："+name+" 年龄： "+age+" 职位： "+post+
                " 薪水： "+salary+"grade: "+grade);
    }
}

class Professor extends Teach {


    public Professor(String name, int age, String post, double salary,double grade) {
        super(name, age, post, salary,grade);

    }

    @Override
    public void introduce() {
        System.out.println("教授信息");
        super.introduce();
    }
}
class Professor2 extends Teach{


    public Professor2(String name, int age, String post, double salary,double grade) {
        super(name, age, post, salary,grade);
    }

    public void introduce() {
        System.out.println("副教授信息");
        super.introduce();
    }


}
```





![image-20220908080837510](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220908080837510.png)





```java
package com.Homework;

import jdk.nashorn.internal.ir.CallNode;

public class Homework04 {
    public static void main(String[] args) {
        Employee wjh = new Employee("wjh", 100, 30);
        maneger zzx = new maneger("zzx", 200, 30, 1.2,1000);
        wjh.print();
        zzx.print();


    }
}

class Employee{
    private String name;
    private double salary;
    private int day;

    public Employee(String name, double salary, int day) {
        this.name = name;
        this.salary = salary;
        this.day = day;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public double getSalary() {
        return salary;
    }

    public void setSalary(double salary) {
        this.salary = salary;
    }

    public int getDay() {
        return day;
    }

    public void setDay(int day) {
        this.day = day;
    }

    public void print(){
        System.out.println("员工 "+getName()+"工资为： "+salary*day);
    }

}

class maneger extends Employee{
    private double grade;
    private int bonus;

    public maneger(String name, double salary, int day, double grade, int bonus) {
        super(name, salary, day);
        this.grade = grade;
        this.bonus = bonus;
    }

    public int getBonus() {
        return bonus;
    }

    public void setBonus(int bonus) {
        this.bonus = bonus;
    }

    public double getGrade() {
        return grade;
    }

    public void setGrade(double grade) {
        this.grade = grade;
    }

    @Override
    public void print() {
        System.out.println("经理 "+getName()+"工资为： "+getSalary()*getDay()*grade+bonus);
    }
}
```





![image-20220908082551966](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220908082551966.png)



```java
package com.Homework;

public class Homework05 {
    public static void main(String[] args) {
        Worker worker = new Worker(100);
        Teacher teacher = new Teacher(300, 1000);
        worker.print();
        teacher.print();

    }
}

class Employee01{
    private double salary;

    public Employee01(double salary) {
        this.salary = salary;
    }

    public double getSalary() {
        return 12*salary;
    }

    public void setSalary(double salary) {
        this.salary = salary;
    }

    public void print(){

        System.out.println("员工工资为： "+getSalary());
    }
}

class Worker extends Employee01{
    public Worker(double salary) {
        super(salary);
    }


    @Override
    public void print() {
        super.print();
    }
}

class Teacher extends Employee01{
    private double ClassSalary;

    public Teacher(double salary, double classSalary) {
        super(salary);
        ClassSalary = classSalary;
    }

    public double getClassSalary() {
        return ClassSalary;
    }


    public double getSalary() {
        return super.getSalary();
    }

    public void print(){

        System.out.println("老师工资为："+(getSalary()+getClassSalary()));//注意增加一个括号计算 否则变成拼接
    }

}

```





![image-20220908090433858](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220908090433858.png)



**this从本类开始访问 本类访问过父类就不再访问**

**super从父类开始访问**

**私有属性子类无法访问**



![image-20220908091343268](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220908091343268.png)





**属性没有动态绑定机制 因此在调用Test方法时 将Rose换成了john**



![image-20220908102653952](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220908102653952.png)



```java
package com.Homework;

public class Homework09 {
    public static void main(String[] args) {
        LablePoint l1=new LablePoint("BB",3213,532);
        
    }
}

class Point{
     private double x;    
     private double y;

    public Point(double x, double y) {
        this.x = x;
        this.y = y;
    }
}
class LablePoint extends Point{
    private String lable;

    public LablePoint( String lable,double x, double y) {
        
        super(x, y);
        this.lable = lable;
    }
   
}

```





![image-20220908103241853](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220908103241853.png)



```java
package com.Homework;

public class Homework10 {
    public static void main(String[] args) {

        Docator docator1= new Docator("wjh", "Teacher", '女', 1000);
        Docator docator2 = new Docator("wjh", "Teacher", '女', 100);
        System.out.println(docator1.equals(docator2));
    }
}
class Docator{
    private String name;
    private String job;
    private char gennder;
    private double salary;

    public Docator(String name, String job, char gennder, double salary) {
        this.name = name;
        this.job = job;
        this.gennder = gennder;
        this.salary = salary;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getJob() {
        return job;
    }

    public void setJob(String job) {
        this.job = job;
    }

    public char getGennder() {
        return gennder;
    }

    public void setGennder(char gennder) {
        this.gennder = gennder;
    }

    public double getSalary() {
        return salary;
    }

    public void setSalary(double salary) {
        this.salary = salary;
    }

    public boolean equals(Object obj){
       if(this==obj)
       {
           return true;
       }
       if(!(obj instanceof Docator))
       {
           return false;
       }
       //向下转型
        Docator docator=(Docator)obj;
       return this.name.equals(docator.name)&&this.salary==docator.salary&&
               this.job.equals(docator.job)&&this.gennder==docator.gennder;
    }
}
```





![image-20220908110407132](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220908110407132.png)





![image-20220908110547422](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220908110547422.png)





![image-20220908110605830](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220908110605830.png)



```java
package com.Homework;

public class Homework13 {
    public static void main(String[] args) {



        Person13 []persons=new Person13[4];
        persons[0]=new Student13("wjh", '女', 17, 20030914);
        persons[1]=new Student13("wly", '女', 16, 20030914);
        persons[2]=new Teacher13("lhh", '男', 20, 1);
        persons[3]=new Teacher13("zzx", '男', 18, 1);


        Homework13 h1=new Homework13();
        h1.Bubble(persons);

        for (int i = 0; i < persons.length; i++) {
            System.out.println(persons[i]);
        }
        for (int i = 0; i < persons.length; i++) {
            h1.test(persons[i]);//遍历每一个对象
        }
    }

    public void test(Person13 p){
        if(p instanceof Student13)//如果运行类型是Students
        {
            ((Student13) p).study();//注意向下转型格式
        } else if (p instanceof Teacher13) {
            ((Teacher13) p).teach();
        }
        else {
            System.out.println("输入有误！！！");
        }
    }

    public void Bubble(Person13 persons[]){
        Person13 tmp=null;
        for (int i = 0; i < persons.length-1; i++) {
            for (int j = 0; j < persons.length-1-i; j++) {
                if(persons[j].getAge()>persons[j+1].getAge()){
                    tmp=persons[j];
                    persons[j]=persons[j+1];
                    persons[j+1]=tmp;
                }
            }
        }
    }


}

class Person13{

    private String name;
    private char sex;
    private int age;

    public Person13(String name, char sex, int age) {
        this.name = name;
        this.sex = sex;
        this.age = age;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public char getSex() {
        return sex;
    }

    public void setSex(char sex) {
        this.sex = sex;
    }

    public int getAge() {
        return age;
    }

    public void setAge(int age) {
        this.age = age;
    }

    public void Play(){
        System.out.println("play....");
    }

    public String Basicprint(){
        return "姓名： "+name+" 性别： "+sex+" 年龄： "+age;
    }

    @Override
    public String toString() {
        return
                "name:" + name + ' ' +
                " sex:" + sex +
                " age:" + age;
    }
}
class Student13 extends Person13{
    private int id;

    public Student13(String name, char sex, int age, int id) {
        super(name, sex, age);
        this.id = id;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public void Play() {
        System.out.println("学生爱玩王者荣耀");
    }

    public void study(){
        System.out.println("studying.....");
    }

    public void print(){

        System.out.println(super.Basicprint()+" id: "+id);
    }

    @Override
    public String toString() {
        return super.toString()+
                "  id=" + id;
    }
}

class Teacher13 extends Person13{
    private int work_age;

    public Teacher13(String name, char sex, int age, int work_age) {
        super(name, sex, age);
        this.work_age = work_age;
    }

    public int getWork_age() {
        return work_age;
    }

    public void setWork_age(int work_age) {
        this.work_age = work_age;
    }

    public void Play() {
        System.out.println("老师爱玩贪玩蓝月");
    }

    public void teach(){
        System.out.println("teaching.....");
    }
    public void print(){
        System.out.print(super.Basicprint());
        System.out.println(" WorkAge: "+getWork_age());
    }

    @Override
    public String toString() {
        return super.toString()+
                "  work_age=" + work_age;
    }
}
```





![image-20220908122115764](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220908122115764.png)



**每个构造函数前隐藏一个super( ); 有其他函数就能将其覆盖**



![image-20220908124342496](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220908124342496.png)











## 项目



### 零钱通



![image-20220907111157574](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220907111157574.png)





**先使用过程编程 后面改成OOP版本 体会OOP编程带来的好处**



![image-20220907111421388](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220907111421388.png)





```java
package com.Project.smallchange.OOP;

//调用OPP中的对象 显示菜单即可
public class smallchangesysAPP {
    public static void main(String[] args) {
        new smallchangesysOOP().mainMenu();
    }
}

```



```java
package com.Project.smallchange.OOP;


import java.text.SimpleDateFormat;
import java.util.Date;
import java.util.Scanner;

//将各个功能对应一个方法
public class smallchangesysOOP {




        boolean loop = true;
        Scanner scanner = new Scanner(System.in);
        String key = "";

        //完成零钱通明细
        //思路： 1.把收益入账和消费 保存到数组  2.可以使用对象  3.简单的话使用String拼接

        String details = "------------零钱通明细--------------";


        //3.完成收益入账
        //定义新的变量(功能驱动程序员增加新的变化和代码)

        double money = 0;
        double balance = 0;
        Date date = null;//date是import java.util.Date类型 表示日期
        SimpleDateFormat sdf = new SimpleDateFormat("yyyy-MM-dd HH:mm");//可以用于日期格式化

        //4.消费
        //定义新变量 保存消费的原因
        String note = "";

        public void mainMenu() {
            do {
                System.out.println("=========零钱通菜单OOP==========");
                System.out.println("\t\t\t1 零钱通明细");
                System.out.println("\t\t\t2 收益入账");
                System.out.println("\t\t\t3 消费");
                System.out.println("\t\t\t4 退 出 ");
                System.out.println(" 请选择(1-4)");

                key = scanner.next();//接收输入的数字

                //使用switch分支
                switch (key) {
                    case "1":
                       this.detail();
                        break;
                    case "2":
                        this.income();
                        break;
                    case "3":
                        this.pay();

                        break;
                    case "4":
                       this.exist();
                        break;

                    default:
                        System.out.println("选择有误！");

                }
            } while (loop);
        }
        //零钱通明细
        public void detail() {
            System.out.println(details);
        }

        //收益入账
        public void income() {
            System.out.print("收益入账金额：");
            money = scanner.nextDouble();
            //money的值应该校验
            //找出不正确金额的条件 给出提示
            if (money <= 0) {
                System.out.println("请输入正确的收益！");
                return;//退出方法不在执行
            }
            balance += money;
            //拼接收益入账信息到detail
            date = new Date();//获取当前日期
            details += "\n收益入账\t+" + money + "\t" + sdf.format(date) + "\t" + balance;
             }

             //消费
            public void pay() {
            System.out.println("消费金额：");
            money = scanner.nextDouble();
            //money的值应该校验

            if(money<=0&&money>balance)
            {
                System.out.println("消费应在0-"+balance);
                return;
            }
            System.out.print("请输入消费说明：");
            note = scanner.next();
            balance -= money;
            //拼接信息
            date = new Date();//获取当前日期
            details += "\n\t" +note + "\t-" + money + "\t" + sdf.format(date) + "\t" + balance;
        }

        public void exist(){
            String choice="";
            while(true){//输入是y/n才能继续执行
                System.out.println("你确定退出吗？y/n");
                choice=scanner.next();
                if("y".equals(choice)||"n".equals(choice)){
                    break;
                }
            }
            if(choice.equals("y")){
                loop = false;
            }
            System.out.println("已退出...");
        }

}

```



### **房屋出租系统**



![image-20220908161646494](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220908161646494.png)



<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220908161703533.png" alt="image-20220908161703533" style="zoom:91%;" />



<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220908161737687.png" alt="image-20220908161737687" style="zoom:80%;" />



<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220908161754007.png" alt="image-20220908161754007" style="zoom:90%;" />



<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220908161915535.png" alt="image-20220908161915535" style="zoom:80%;" />



<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220908162038967.png" alt="image-20220908162038967" style="zoom:78%;" />





<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220908162109340.png" alt="image-20220908162109340" style="zoom:92%;" />





```java
package RentalHousing.App;

import RentalHousing.view.Houseview;

public class HouseRentApp {
    public static void main(String[] args) {
       new Houseview().menu();//创建程序入口
        System.out.println("========你已经退出系统========");

    }
}

```





```java
package RentalHousing.domain;


/*
    House类对象表示一个房屋信息
 */
public class House {

    private int id;
    private String name;
    private String phone;
    private String address;
    private int rent;
    private String state;

    //构造器

    public House(int id, String name, String phone, String address, int rent, String state) {
        this.id = id;
        this.name = name;
        this.phone = phone;
        this.address = address;
        this.rent = rent;
        this.state = state;
    }

    public int getId() {
        return id;
    }

    public void setId(int id) {
        this.id = id;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getPhone() {
        return phone;
    }

    public void setPhone(String phone) {
        this.phone = phone;
    }

    public String getAddress() {
        return address;
    }

    public void setAddress(String address) {
        this.address = address;
    }

    public int getRent() {
        return rent;
    }

    public void setRent(int rent) {
        this.rent = rent;
    }

    public String getState() {
        return state;
    }

    public void setState(String state) {
        this.state = state;
    }

    //为了方便输出对象信息 实现toString

    @Override
    public String toString() {
        return id +
                "\t\t" + name  +
                "\t\t" + phone +
                "\t\t" + address +
                "\t"+ rent +
                "\t" + state;
    }
}

```



```java
package RentalHousing.utils;

import java.util.Scanner;

public class Utility {
    //
// Source code recreated from a .class file by IntelliJ IDEA
// (powered by FernFlower decompiler)
//
        private static Scanner scanner;

        public Utility() {
        }

        public static char readMenuSelection() {
            while(true) {
                String str = readKeyBoard(1, false);
                char c = str.charAt(0);
                if (c == '1' || c == '2' || c == '3' || c == '4' || c == '5') {
                    return c;
                }

                System.out.print("选择错误，请重新输入：");
            }
        }

        public static char readChar() {
            String str = readKeyBoard(1, false);
            return str.charAt(0);
        }

        public static char readChar(char defaultValue) {
            String str = readKeyBoard(1, true);
            return str.length() == 0 ? defaultValue : str.charAt(0);
        }

        public static int readInt() {
            while(true) {
                String str = readKeyBoard(10, false);

                try {
                    int n = Integer.parseInt(str);
                    return n;
                } catch (NumberFormatException var3) {
                    System.out.print("数字输入错误，请重新输入：");
                }
            }
        }

        public static int readInt(int defaultValue) {
            while(true) {
                String str = readKeyBoard(10, true);
                if (str.equals("")) {
                    return defaultValue;
                }

                try {
                    int n = Integer.parseInt(str);
                    return n;
                } catch (NumberFormatException var4) {
                    System.out.print("数字输入错误，请重新输入：");
                }
            }
        }

        public static String readString(int limit) {
            return readKeyBoard(limit, false);
        }

        public static String readString(int limit, String defaultValue) {
            String str = readKeyBoard(limit, true);
            return str.equals("") ? defaultValue : str;
        }

        public static char readConfirmSelection() {
            System.out.println("请输入你的选择(Y/N): 请小心选择");

            while(true) {
                String str = readKeyBoard(1, false).toUpperCase();
                char c = str.charAt(0);
                if (c == 'Y' || c == 'N') {
                    return c;
                }

                System.out.print("选择错误，请重新输入：");
            }
        }

        private static String readKeyBoard(int limit, boolean blankReturn) {
            String line = "";

            while(scanner.hasNextLine()) {
                line = scanner.nextLine();
                if (line.length() == 0) {
                    if (blankReturn) {
                        return line;
                    }
                } else {
                    if (line.length() >= 1 && line.length() <= limit) {
                        break;
                    }

                    System.out.print("输入长度（不能大于" + limit + "）错误，请重新输入：");
                }
            }

            return line;
        }

        static {
            scanner = new Scanner(System.in);
        }
    }



```



```java
package RentalHousing.view;

import RentalHousing.domain.House;
import RentalHousing.service.HouseService;
import RentalHousing.utils.Utility;

/*
    1.显示界面
    2.接受用户输入
    3.调用HouseService完成对房屋信息的个各种操作
 */
public class Houseview {
    private boolean loop = true;
    private char key = ' ';//中间要有空格
    private HouseService houseService = new HouseService(10);


    //根据id修改房屋信息
    public void update(){
        System.out.println("===========修改房屋信息============");
        System.out.println("===========请输入待修改的房间编号(-1表示退出)============");
        int updateId=Utility.readInt();
        if(updateId==-1){
            System.out.println("===========放弃修改房屋信息============");
            return;
        }

        //根据输入得到updateId 查找对象
        //返回的是引用类型 就是数组的元素
        //在后面对house.setxxx(),就会修改HouseService中的元素！！！！
        House house = houseService.findById(updateId);
        if(house==null){
            System.out.println("===========修改的房屋编号不存在============");
            return;
        }

        System.out.println("姓名("+house.getName()+"): ");
        String name=Utility.readString(8,"");//如果用户直接回车表示不修改该信息默认""
        if(!"".equals(name)){
            house.setName(name);
        }

        System.out.println("电话：("+house.getPhone()+"):");
        String phone=Utility.readString(18);
        if(!"".equals(phone)){
            house.setPhone(phone);
        }
        System.out.println("地址：("+house.getAddress()+"):");
        String address=Utility.readString(18);
        if(!"".equals(address)){
            house.setAddress(address);
        }
        System.out.println("租金：（"+house.getRent()+"):");
        int rent =Utility.readInt(-1);
        if(rent!=-1){
            house.setRent(rent);
        }
        System.out.println("状态：("+house.getState()+"):");
        String state=Utility.readString(3,"");
        if(!"".equals(state)){
            house.setState(state);
        }
        System.out.println("===========修改房屋信息成功============");
    }

    //根据id完成信息查找
    public void findHouse(){
        System.out.print("===========查找房屋信息============");
        System.out.println("请输入需要查找的房间编号： ");
        int findid=Utility.readInt();
        House house=houseService.findById(findid);
        if(house!=null){
            System.out.println(house);
        }else{
            System.out.println("查找的房间Id不存在！");
        }
    }



    //完成退出确认
    public void exit(){
        char c=Utility.readConfirmSelection();
        if(c=='Y'){
            loop = false;
        }

    }


    //编写delHouse 接收输入的id 调用Service的delete方法
    public void delHouse() {
        System.out.println("============删除房屋信息===========");
        System.out.print("===========请输入待删除的房间编号(-1退出)============");
        int delId = Utility.readInt();
        if (delId == -1) {
            System.out.println("============放弃删除房屋信息===========");
            return;
        }
        //System.out.println("请确认是否删除(Y/N),小心选择");
        char choice = Utility.readConfirmSelection();//该方法本身就有循环判断的逻辑 必须输Y/N
        if(choice=='Y'){
            if(houseService.del(delId)){
                System.out.println("============删除房屋信息成功===========");
            }

            else{
                System.out.println("============房屋信息不存在===========");
            }
        }
        else{
            System.out.println("============放弃删除房屋信息===========");
        }
    }


    //编写listHouses()显示房屋列表
    public void listHouse() {
        System.out.println("============房屋列表===========");
        System.out.println("编号\t\t房主\t\t电话\t\t地址\t\t月租\t\t状态(已出租/未出租)");
        House[] houses = houseService.list();//得到所有房屋信息
        for (int i = 0; i < houses.length; i++) {//问题：
            if (houses[i] == null) {
                break;
            }
            System.out.println(houses[i]);
        }
        System.out.println("=========房屋列表显示完毕=============");
    }

    public void addHouse() {
        System.out.println("=========添加房屋=============");
        System.out.println("姓名：");
        String name = Utility.readString(8);
        System.out.println("电话： ");
        String phone = Utility.readString(12);
        System.out.println("地址： ");
        String address = Utility.readString(16);
        System.out.println("月租： ");
        int rent = Utility.readInt();
        System.out.println("状态： ");
        String state = Utility.readString(3);

        //创建一个新的House对象 id任意分配
        House newHouse = new House(0, name, phone, address, rent, state);
        if (houseService.add(newHouse)) {
            System.out.println("==========添加房屋成功===========");
        } else {
            System.out.println("==========添加房屋失败===========");
        }


    }


    //显示一个主菜单
    public void menu() {


        do {
            System.out.println("==========房屋出租系统===========");
            System.out.println("\t\t\t1 新 增 房 源");
            System.out.println("\t\t\t2 查 找 房 屋");
            System.out.println("\t\t\t3 删 除 房 屋 信 息");
            System.out.println("\t\t\t4 修 改 房 屋 信 息");
            System.out.println("\t\t\t5 显 示 房 屋 信 息");
            System.out.println("\t\t\t6  退         出 ");
            System.out.println("请输入你的选择(1-6)");
            key = Utility.readChar();
            switch (key) {
                case '1':
                    addHouse();
                    break;
                case '2':
                    findHouse();
                    break;
                case '3':
                    delHouse();
                    break;
                case '4':
                    update();
                    break;
                case '5':
                    listHouse();
                    break;
                case '6':
                    exit();
                    break;
            }
        } while (loop);

    }

}

```



```java
package RentalHousing.service;

import RentalHousing.domain.House;
import RentalHousing.view.Houseview;

/*
    1.相应HouseView的调用
    2.完成对房屋信息的各种操作
 */
public class HouseService {
        private House[] houses;//保存house对象

        private int housenumber=1;
        private int IdCounter=1;
        public HouseService(int size){//构造器 当创建HouseService对象 指定数组大小
                //new houses
                houses=new House[size];
                //为了配合测试列表信息 初始化一个House对象

                houses[0]=new House(1,"zzx","112","江南名都",2000,"未出租");
        }

        //find方法

        public House findById(int findid){

                //遍历数组

                for (int i = 0; i < housenumber; i++) {
                        if(findid==houses[i].getId()){
                                return houses[i];
                        }
                }
                return null;
        }

        //del方法 删除一个房屋信息
        public boolean del(int delId){

                //先找到删除的房屋信息对应的下表
                int index = -1;
                for (int i = 0; i < housenumber; i++) {
                        if(delId==houses[i].getId()){
                                index=i;
                        }
                }
                //如果找不到
                if(index==-1){
                        return false;
                }
                //如果找到
               for(int i=index;i<housenumber-1;i++){
                       houses[i]=houses[i+1];
               }
               houses[--housenumber]=null;
               return true;

        }


        public boolean add(House newHouse) {
                //判断是否还能不能添加

                if (housenumber >= houses.length) {//已满
                        System.out.println("数组已满 不能添加");
                        return false;
                }

                //把newHouse对象加在数组最后
                houses[housenumber++] = newHouse;//后置++的应用
                //housenumber++;

                //设置一个id自增长的机制 然后更新newHouse的id
                newHouse.setId(++IdCounter);
                return true;
        }

        //list方法 返回houses
        public House[] list(){
                return houses;
        }

}

```





## 面向对象高级



### 类变量和类方法



#### 类变量/静态变量(static)



##### 类变量的引出

![image-20220912090100619](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220912090100619.png)



```java
public class ChildGame {
    public static void main(String[] args) {

        Child c1=new Child("庄智鑫");
        c1.count++;
        Child c2 = new Child("万佳惠");
        c2.count++;

        System.out.println("c1.count= "+c1.count);
        System.out.println("c2.count= "0+c2.count);
        System.out.println("共有"+Child.count+"小孩加入游戏");
    }
}

class Child{
    priString name;
    //定义一个类变量/静态变量
    //该变量会被Child类的所有类对象实例共享
    public static int count=0;
    public Child(String name) {
        this.name = name;
    }
    public void join(){
        System.out.println(name+" 加入了游戏...");
    }
}

```



##### 类变量内存布局



<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220912091109797.png" alt="image-20220912091109797" style="zoom:50%;" />



static变量是对象共享  不管static变量在哪里 static变量是同一个类所有对象共享  **static类变量 在类加载的时候就生成了**



##### **什么是类变量**

类变量也叫静态变量/静态属性  是**该类的对象共享的变量** 任何一个该类的对象去访问他时 取到的都是相同值

同样任何一个该类的对象去修改他时 修改的也是同一个变量

**语法**：**访问修饰符 static  数据类型 变量名；**



##### 如何访问类变量



```java
package com.zzx.static_;

public class VisitStatic {
    public static void main(String[] args) {

        //类名.类变量名
        //类变量是随着类的加载而创建 所以即使没有创建对象实例也可以访问
        System.out.println(A.name);
        
        //通过对象名.类变量名
        A a = new A();
        System.out.println(a.name);

    }
}

class A{
    public static String name="庄智鑫";
}
```





##### 类变量使用细节



![image-20220912103700416](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220912103700416.png)

![image-20220912104310869](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220912104310869.png)





#### 类方法



##### **类方法基本介绍**

访问修饰符 static 数据返回类型 方法名( ){ }



##### 类方法的调用

使用方式：类名.类方法名/对象名.类方法名



##### **类方法的经典使用场景**



![image-20220912105804190](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220912105804190.png)





##### 类方法注意事项



1.类方法和普通方法都是随着类的加载而加载 将结构信息存储在方法区：

2.**类方法中无this参数 普通方法中隐含this参数**

3.类方法可以通过类名调用 也可以通过对象调用

4.类方法中不允许使用和对象有关的关键字 比如this和super 

5.**类方法中只能访问静态变量或静态方法**

6.普通成员方法 既可以访问普通变量方法 也可以访问静态变量方法

**小结**：静态方法 只能访问静态的成员 非静态的方法 可以访问静态成员和非静态成员（必须遵循访问权限）





#### 深入理解main方法



![image-20220912163725384](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220912163725384.png)



静态方法中的规则在main函数中通用 **因为main本质也是一个静态方法**





### 代码块



**基本介绍**

代码块又称初始化块 属于类中的成员【即是类中的一部分】 类似于方法 将逻辑语句封装在方法体中 通过{ }包围起来

**但是和方法不同 没有方法名 没有返回 没有参数 只有方法体 而且不用通过对象或类显式调用 而是加载类时 或创建对象的隐式调用**



**基本语法**

[修饰符]{

代码

}；



注意：

1.修饰符可选 **要写只能写static**

2.代码块分为两类 **使用static修饰的叫静态代码块 没有的叫普通代码快/非静态代码块**

3.逻辑语句可以为任何逻辑语句(输入 输出 方法调用 循环 判断)

4.；可写可不写





**代码块的好处**



1.**相当于另一种形式的构造器**(对构造器的补充机制)**可以做初始化操作**

2.如果多个构造器中都有重复的语句 可以抽取到初始化块中 提高代码的重用性



```java
package com.zzx.CodeBlock_;

public class CodeBlock01 {
    public static void main(String[] args) {
        Movie movie=new Movie("你好");
    }
}
class Movie{
    private String name;
    private double price;
    private String director;

    //3个构造器->重载
    //三个构造器都有相同的语句 此时将相同的语句放入到一个代码块中
   /* public Movie(String name) {
        System.out.println("1");
        System.out.println("2");
        System.out.println("3");
        this.name = name;
    }

    public Movie(String name, double price) {
        System.out.println("1");
        System.out.println("2");
        System.out.println("3");
        this.name = name;
        this.price = price;
    }

    public Movie(String name, double price, String director) {
        System.out.println("1");
        System.out.println("2");
        System.out.println("3");
        this.name = name;
        this.price = price;
        this.director = director;
    }*/
    
    //代码块调用的优先级大于构造器
    {
        System.out.println("1");
        System.out.println("2");
        System.out.println("3");
    }
    public Movie(String name) {
        System.out.println("name被调用");
        this.name = name;
    }

    public Movie(String name, double price) {

        this.name = name;
        this.price = price;
    }

    public Movie(String name, double price, String director) {

        this.name = name;
        this.price = price;
        this.director = director;
    }
}
```



**注意事项1**

1.static代码块也叫静态代码块 作用就是对类进行初始化1 而且随着类的加载而进行 并且只会执行一次

如果是普通代码块 每创建一个对象就执行

**2.类什么时候被加载【重要 背】**

**（1）创建对象实例时(new)**

**（2）创建子类对象实例 父类也会被加载**

**（3）使用类的静态成员时（静态属性 静态方法）**

**（4）static代码块是在类加载时执行的 而且只会执行一次**



3.**普通的代码块 在创建对象实例时 会被隐式的调用 被创建一次 就会调用一次 是构造器的补充**

如果只是使用类的静态成员时 普通代码块并不会执行



```java
package com.zzx.CodeBlock_;

public class CodeBlockDetail {

    public static void main(String[] args) {
        //1.创建对象实例
        A a = new A();
        //创建子类对象实例 父类也会被加载 父类先被加载
        //3.使用类的静态成员
        System.out.println(Cat.n);
    }
}

class B{
    static{
        System.out.println("B的静态代码块");
    }
}
class A extends B{
    
    static{
        System.out.println("A的静态代码块");
    }
}

class Cat{
    public static int n=900;
    static{
        System.out.println("Cat的静态代码被执行");
    }
}

```



**注意事项2**



4.创建一个对象时 在一个类调用顺序是：

（1）调用静态代码块和静态属性初始化(注意：**静态代码块和静态属性初始化调用的优先级一样** 如果有多个

静态代码块和多个静态变量初始化 则按他们定义的顺序调用)

（2）调用普通代码块和普通属性的初始化（注意：**普通代码块和普通属性初始化的优先级一样** 如果有多个

普通代码块和多个普通属性初始化 则按他们定义的顺序调用)）



5.**构造方法[构造器]的最前面其实隐含了super( )和调用普通代码块** 

 **静态相关的代码块/属性初始化 在类加载时就执行完毕 因此是优先普通代码块执行的**



![image-20220912194732508](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220912194732508.png)



#### 代码块练习



<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220912200255269.png" alt="image-20220912200255269" style="zoom:80%;" />







### 单例设计模式



1.静态方法和属性的经典使用

2.设计模式是在大量的实践中总结和理论化之后优选的代码结构 编程风格 以及解决问题的思考方式

设计模式就像棋谱 免去了我们在思考和摸索



**什么是单例**



1.所谓类的单例设计模式 就是采用一定的方法保证在整个软件系统中 对某个类**只能存在一个对象实例**

并且该类只提供一个取得其对象实例的方法

2.分为两种模式： 饿汉式 懒汉式



**演示饿汉式和懒汉式单例模式的实现**

**饿汉式**

1.**构造器私有化->防止直接new 一个对象**

2.**类的内部创建对象 该对象是静态的**

3.**向外暴露一个静态的公共方法**



**懒汉式**

**1.构造器私有化**

**2.定义一个静态属性对象**

**3.提供一个public的static方法 可以返回Cat对象** 

**4.只有当用户使用才返回一个Cat对象 后面再次调用会返回上次创建的对象**



```java
package com.zzx;

public class SingleTon02 {
    public static void main(String[] args) {
        System.out.println(Cat.n1);//不会调用构造器
        Cat instance = Cat.getInstance();
        System.out.println(instance);
        Cat instance2 = Cat.getInstance();
        System.out.println(instance);//返回一样的对象
    }
}

//在程序运行中 只能创建一只猫
class Cat{
    private String name;
    public static int n1=1;
    private static Cat cat;
    //1.构造器私有化
    //2.定义一个静态属性对象
    //3.提供一个public的static方法 可以返回Cat对象
    //4.只有当用户使用才返回一个Cat对象 后面再次调用会返回上次创建的对象
    private Cat(String name) {
        System.out.println("构造器被调用");
        this.name = name;
    }

    public static  Cat getInstance(){
        if(cat==null){
            cat=new Cat("wjh");
        }
        return cat;
    }

    @Override
    public String toString() {
        return "Cat{" +
                "name='" + name + '\'' +
                '}';
    }
}
```





![image-20220912210830293](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220912210830293.png)





### final关键字

final：不可更改的



![image-20220913103905587](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220913103905587.png)



![image-20220913104527219](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220913104527219.png)



![image-20220913105336757](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220913105336757.png)





### 抽象类



![image-20220913110453556](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220913110453556.png)



#### 抽象类基本介绍



1.用abstract关键字来修饰一个类时 这个类就是抽象类

​	访问修饰符 abstract 类名{ }

2.用abstract关键字来修饰一个方法时 这个方法就是抽象方法

​	访问修饰符 abstract 返回类型 方法名(参数列表)；//没有方法体

3.抽象类的价值更多作用是在于设计 设计者设计好后 让子类继承并实现抽象类

4.抽象类是考官爱问的考点 在框架和设计模式中使用的比较多



**抽象类使用细节**



1.抽象类不能被实例化

2.抽象类不一定要包含abstract方法 也就是说抽象类可以没有abstract方法 

3.一旦类中包含abstract方法 一定要声明为抽象类

4.abstract只能修饰类和方法 不能修饰属性和其他的

5.抽象类可以有任意成员（抽象类还是类） 比如非抽象方法 构造器 静态属性等等等

6.抽象方法不能有主体

7.如果一个类继承了抽象类 则它必须实现抽象类的**所有**抽象方法 **除非它自己也声明为abstract类**

8.抽象方法不能使用private final static来修饰 因为这些关键字与子类重写相违背



#### 抽象类最佳实践-模板设计模式





<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220913120412140.png" alt="image-20220913120412140" style="zoom:200%;" />



<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220913153412861.png" alt="image-20220913153412861" style="zoom:67%;" />





### 接口



<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220913153517173.png" alt="image-20220913153517173" style="zoom: 89%;" />



<img src="C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220913160435147.png" alt="image-20220913160435147" style="zoom:80%;" />



![image-20220913161156047](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220913161156047.png)

**在接口中抽象方法可以省略abstract** 

在JDK8后 可以有默认实现方法 需要使用default关键字修饰





**接口使用细节**



**1.接口不能被实例化**

**2.接口中所有的方法是public方法 接口中抽象方法 可以不用abstract修饰**

**3.一个普通类实现接口 就必须将该接口的所有方法都实现 可以使用alt+enter快速实现**

**4.抽象类实现接口 可以不实现接口方法**

**5.一个类同时可以实现多个接口**

**6.接口中的属性只能是final的 而且是public static final修饰符** **比如  int n=1; 等价于 public static final int n=1;(必须初始化)**

**7.接口中属性的访问形式 ：接口名.属性名**

**8.接口不能继承其他的类 但是可以继承多个别的接口**

​	**interface A extends B，C{ }**

**9.接口的修饰符只能是public和默认 这一点和类的修饰符是一样的**



![image-20220913174633753](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220913174633753.png)



b.a   A是public的

A.a 默认有static 直接用类名访问

B.a  B中实现了A 类比继承 因此也能访问



#### 接口和继承



![image-20220913195250012](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220913195250012.png)



**接口和继承解决的问题不同**



继承：解决代码复用性和可维护性

接口：设计 设计好各种规范 让其他类去实现这些方法 更加的灵活



**接口比继承更灵活**



继承满足的是is-a的关系 而接口只需满足like-a的关系

**接口在一定程度上实现代码解耦**【即接口规范性+动态绑定】



#### 接口多态特性



**接口的多态特性**



1.**多态参数**

在前面的USB案例 既可以接收手机对象 又可以接收相机对象 就体现了接口多态

2.**多态数组**

演示一个案例 给USB数组中存放Phone和相机对象 Phone还有一个特有的方法call（）请遍历USB数组

如果是Phone对象 除了调用USB接口定义的方法外 还需要调用Phone特有的特殊方法call

3.接口存在**多态传递**现象



```java
package com.zzx.interface_;

public class InterfacePolyPass {
    public static void main(String[] args) {
        IG ig=new Teacher();//接口类型的变量可以指向实现该接口对象的实例
        IH ih=new Teacher();//如果IG继承了IH接口 而Teacher实现了IG接口
        //那么实际上相当于Teacher也实现了IH接口
    }
}

interface IH{}
interface IG extends IH{}
class Teacher implements IG{
    
}

```





**练习**



![image-20220914091533799](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220914091533799.png)



**访问接口用A.x;   访问父类用super.x;**



### 内部类（重要）



**基本介绍**

一个类的内部又完整的嵌套了另一个类结构  被嵌套的类称为**内部类**

嵌套的其他类的类称为**外部类**   是我们的第五大成员**【属性 方法 构造器 代码块 内部类】**

内部类的最大的特点就是**可以直接访问私有属性** **并且可以体现类与类之间的包含关系**



**基本语法**

class Outer{//外部类

class Inner{//内部类

​	}

}

class Other {/外部其他类

}



```java
package com.zzx.Innerclass;

public class Innerclass01 {
    public static void main(String[] args) {
        
    }
}
class Outer{//外部类
    private int n1=100;

    public Outer(int n1) {
        this.n1 = n1;
    }

    public void m1(){
        System.out.println("m1()");
    }
    
    {
        System.out.println("代码块...");
    }
    class Inner{//在Outer类的内部
        
    }
}

```



#### 内部类的分类



定义在外部类的局部位置上（比如方法内）

1.**局部内部类（有类名）**

2.**匿名内部类（没有类名  重点!!!!）**



定义在外部类的成员位置上

**1.成员内部类(没用static修饰)**

**2.静态内部类（使用static修饰）**

​         

#### 局部内部类



说明：局部内部类是定义在外部类的局部位置 比如方法中 并且有类名

1.可以直接访问外部类的所有成员 包含私有的

2.**不能添加访问修饰符** 因为他的地位就是一个局部变量 **局部变量是不能使用修饰符的**

但是可以使用final修饰 因为局部变量也可以使用final

3.作用域：**仅仅在定义它的方法或代码块中**

4.局部内部类---访问--->外部类的成员【访问方式：直接访问】

5.外部类---访问--->局部内部类的成员

访问方式：**创建对象 再访问(注意：必须在作用域内)**



```java
package com.zzx.Innerclass;

public class LocalInnerClass {
    public static void main(String[] args) {
        Outer02 outer02 = new Outer02();
        outer02.m2();

    }
}

class Outer02{
    private int n1=100;
    private void m3(){
        System.out.println("Outer m3()");
    }
    public void m2(){
        //局部内部类是定义在外部类的局部位置 通常在方法中
       final class Inner02{//局部内部类 本质还是类
            public void f1(){
                System.out.println("n1= "+n1);
                m3();
            }
        }
    }
}
```



6.外部其他类--->不能访问---->局部内部类(因为局部内部类地位是一个局部变量)

7.如果外部类和局部内部类的成员重名时 默认**遵循就近原则** 如果想访问外部类的成员

则可以使用(**外部类名.this.成员**)去访问  **外部类名.this本质是外部类的对象** 

**即哪个对象调用了内部类所在的方法   外部类名.this就是哪个对象**

System.out.println("外部类的n2= "+外部类名.this.n2)；





#### 匿名内部类的使用（重要）



**（1）本质仍是内部类  （2）该类没有名字  （3）同时还是一个对象**



说明：匿名内部类是定义在外部类的局部位置 比如方法中 并且没有类名(由系统分配)

1.**匿名内部类的基本语法**

new 类或接口（参数列表）{

类体

}；



```java
package com.zzx.Innerclass;

public class AnonymousInnerClass {
    public static void main(String[] args) {

        Outer04 outer04 = new Outer04();
        outer04.method();

    }
}
class Outer04{//外部类
    private int n1=10;//属性
    public void method(){//方法
    //基于接口的匿名内部类
     //1.需求：想使用接口IA 并创建对象
     //2.传统方式 写一个类 实现该接口 并创建对象
     //3。若需求：只是使用一次Tiger/Dog类 后面不再使用

     //4.可以使用匿名内部类来简化开发
        /*IA tiger=new Tiger();//接口类型可以指向实现该接口的类的对象实例
        tiger.cry();*/

        //Tiger的编译类型是IA 运行类型是匿名内部类Outer04$1
        /*底层会分配类名Outer04$1
        class Outer04$1 implements IA{
            @Override
            public void cry(){
                System.out.println("芝士老虎");
            }
        }
         */

        //jdk底层在创建内部类Outer04$1 立即马上就创建了Outer04$1实例 并把地址返回给tiger
        //体现出对象的特征
        //匿名内部类使用一次 就不能再使用
        IA tiger=new IA(){
            public void cry() {
                System.out.println("芝士老虎");
            }
        };

        //基于类的匿名内部类
        //Father编译类型father 运行类型为匿名类型
        //底层会创建匿名内部类
        /*
        class Outer04$2 implements Father{
        public void test(){
                System.out.println("匿名内部类重写了test方法");
            }
        }
         */
        //同时也直接返回了father的匿名内部类对象
        Father father=new Father("zzx"){//zzx这个参数列表会传递给构造器
            @Override
            public void test() {
                System.out.println("匿名内部类重写了test方法");
            }
        };
        System.out.println("fether的运行类型= "+father.getClass());
        father.test();

        Animal animal=new Animal(){
            @Override
            public void eat() {
                System.out.println("吃东西");
            }
        };
        animal.eat();
    }
}



interface IA{//接口
    public void cry();
}

class Tiger implements IA{
    @Override
    public void cry() {
        System.out.println("芝士老虎");
    }
}

class Dog implements IA{
    @Override
    public void cry() {
        System.out.println("芝士小狗");
    }
}

class Father{//类
    public Father(String name){//构造器
        super();
    }

    public void test(){//方法

    }
}
abstract class Animal{
    public void eat(){}

}

```





##### 匿名内部类使用细节



1.**匿名内部类的语法比较奇特 它既是一个类的定义 同时它本身又是一个对象**

**2.因此从语法上看 它既有定义类的特征 也有创建对象的特征** 

**jdk底层在创建内部类Outer04$1 立即马上就创建了Outer04$1实例 并把地址返回给接口的实例对象**

**3.可以直接访问外部类的所有成员 包含私有的**

**4.不能添加访问修饰符 因为它的地位就是一个变量**

**5.作用域：仅仅在定义它的方法或代码块中**

**6.匿名内部类---->访问----->外部类成员【访问方式 直接访问】**

**7.外部其他类---->不能访问---->匿名内部类（因为匿名内部类地位是一个局部变量）**

**8.如果外部类和匿名内部类的成员重名时 内部类访问的话 默认遵循就近原则**

**如果想访问外部类成员 则可以使用（外部类名.this.成员）去访问**

**哪个对象调用了内部类所在的方法   外部类名.this就是哪个对象**





##### 匿名内部类实践





```java
package com.zzx.Innerclass;



public class InnerClassExercise01 {
    public static void main(String[] args) {
        f1(new IL(){//匿名内部类本质还是一个对象
            @Override
            public void show() {
                System.out.println("芝士雪豹");
            }
        });
        //传统方法
        f1(new Car());
    }

    //静态方法 形参是接口类型
    public static void f1(IL il){
        il.show();
    }
}

interface IL{
    void show();
}

class Car implements IL{
    @Override
    public void show() {
        System.out.println("芝士猴子");
    }
}
```





![image-20220915104229086](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220915104229086.png)





```java
package com.zzx.Innerclass;

public class InnerClassExercise02 {
    public static void main(String[] args) {
        CellPhone cellPhone1 = new CellPhone();

        cellPhone1.alarmclock(new Bell() {
            @Override
            public void ring() {
                System.out.println("懒猪起床了");
            }
        });
        CellPhone cellPhone2 = new CellPhone();
        cellPhone2.alarmclock(new Bell() {
            @Override
            public void ring() {
                System.out.println("上课了");
            }
        });


    }
}


interface Bell{
    void ring();
}

class CellPhone{

    public void alarmclock(Bell bell){//形参是Bell接口类型
        bell.ring();//动态绑定
    }

}
```





#### 成员内部类



说明：成员内部类是**定义在外部类的成员位置 并且没有static修饰**

**1.可以直接访问外部类的成员 包括私有的**

**2.可以添加任意访问修饰符（public protected 默认 private）因为它的地位就是外部类的一个成员**

**3.作用域：和外部类的其他成员一样 为整个类体比如前面的案例 在外部类的成员方法中创建成员内部类对象再调用方法**

**4.成员内部类---->访问---->外部类（比如 属性）[访问方式：直接访问]**

**5.外部类---->访问---->内部类(说明) 访问方式：创建对象再访问**

**6.外部其他类---->访问---->成员内部类**

**7.如果外部类和内部类的成员重名时 内部类访问的话 默认遵循就近原则 如果想访问外部类成员 则可以使用（外部类.this.成员）去访问外部类的成员**





```java
package com.zzx.Innerclass;

public class MemberInnerClass {
    public static void main(String[] args) {

        Outer08 outer08 = new Outer08();
        outer08.t1();
        //外部其他类 使用成员内部类的2种方式

        //1.new Inner08()是Outer08的对象实例outer08的成员 是一个语法不用过于纠结
        Outer08.Innter08 inner08=outer08.new Innter08();
        //2.在外部类中编写一个方法 返回Inner08对象
        Outer08.Innter08 inner08Instance=outer08.getInner08Instance();
        inner08Instance.say();
    }
}

class Outer08{//外部类
    private int n1=10;
    public String name="蔡徐坤";
    class Innter08{//成员内部类 放在成员的位置
        public void say(){
            System.out.println("Outer08的 n1 = "+n1+"\"Outer08的 name= "+name );
        }
    }

    //返回一个Inner08实例
    public Innter08 getInner08Instance(){
        return new Innter08();
    }

    //写一个方法
    public void t1(){
        //使用成员内部类
        Innter08 inner08=new Innter08();
        inner08.say();
    }
}
```





#### 静态内部类





**说明：静态内部类是定义在外部类的成员位置 并且有static修饰**

**1.可以直接访问外部类的所有静态成员 包含私有的 但不能直接访问非静态成员**

**2.可以添加任意访问修饰符 因为它的地位就是一个成员**

**3.作用域：同其他的成员 为整个类体**

**4.静态内部类--->访问--->外部类（比如静态属性）【访问方式：直接访问所有静态成员】**

**5.外部类---->访问---->静态内部类 访问方式：创建对象 再访问**

**6.外部其他类--->访问--->静态内部类**

**7.如果外部类和静态内部类的成员重名时 静态内部类访问的时 默认遵循就近原则**

**如果像访问外部类的成员 则可以使用(外部类名.成员)去访问** **因为静态成员可以用类直接访问**

```java
package com.hspedu.innerclass;

public class StaticInnerClass01 {
    public static void main(String[] args) {
        Outer10 outer10 = new Outer10();
        outer10.m1();

        //外部其他类 使用静态内部类
        //方式1
        //因为静态内部类，是可以通过类名直接访问(前提是满足访问权限)
        Outer10.Inner10 inner10 = new Outer10.Inner10();
        inner10.say();
        //方式2
        //编写一个方法，可以返回静态内部类的对象实例.
        Outer10.Inner10 inner101 = outer10.getInner10();
        System.out.println("============");
        inner101.say();

        Outer10.Inner10 inner10_ = Outer10.getInner10_();
        System.out.println("************");
        inner10_.say();
    }
}

class Outer10 { //外部类
    private int n1 = 10;
    private static String name = "张三";
    private static void cry() {}
    //Inner10就是静态内部类
    //1. 放在外部类的成员位置
    //2. 使用static 修饰
    //3. 可以直接访问外部类的所有静态成员，包含私有的，但不能直接访问非静态成员
    //4. 可以添加任意访问修饰符(public、protected 、默认、private),因为它的地位就是一个成员
    //5. 作用域 ：同其他的成员，为整个类体
    static class Inner10 {
        private static String name = "韩顺平教育";
        public void say() {
            //如果外部类和静态内部类的成员重名时，静态内部类访问的时，
            //默认遵循就近原则，如果想访问外部类的成员，则可以使用 （外部类名.成员）
            System.out.println(name + " 外部类name= " + Outer10.name);
            cry();
        }
    }

    public void m1() { //外部类---访问------>静态内部类 访问方式：创建对象，再访问
        Inner10 inner10 = new Inner10();
        inner10.say();
    }

    public Inner10 getInner10() {
        return new Inner10();
    }

    public static Inner10 getInner10_() {
        return new Inner10();
    }
}


```



**练习**



![image-20220916102533195](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220916102533195.png)



结果均为5

Test t=new Test( ); 调用构造器中的输出语句 默认为5

而t.new lnner( );又创建了一个新的类对象 默认值为5因此输出仍然是5



![image-20220917112836341](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220917112836341.png)



静态对象是共享的  访问和修改都是同一个



#### 练习



![image-20220917112918412](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220917112918412.png)





![image-20220922084557280](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220922084557280.png)



```java
package com.zzx_.Homework;

/**
 * @author 芝士蔡徐坤
 * @version 1.0
 */
public class Homework06 {

    public static void main(String[] args) {
        Person wjh = new Person("万佳惠", new Horse());
        wjh.common();
        wjh.passRiver();

    }
}

class Person{
    private String name;
    private Vehicles vehicles;

    public Person(String name, Vehicles vehicles) {
        this.name = name;
        this.vehicles = vehicles;
    }
    //把具体的需求 封装成方法
    public void passRiver(){
        if(!(vehicles instanceof Boat)){
            vehicles = VehiclesFactory.getBoat();
        }
        vehicles.work();
    }
    public void common(){
        //判断属性是否为已经存在
        if(!(vehicles instanceof Horse)){
          vehicles = VehiclesFactory.getHorse();
        }

        vehicles.work();

    }
}
interface Vehicles{
    public void work();
}

class Horse implements Vehicles{
    @Override
    public void work() {
        System.out.println("一般情况下使用马儿");
    }
}

class Boat implements Vehicles{
    @Override
    public void work() {
        System.out.println("过河的时候使用船");
    }
}
class VehiclesFactory{

    private static Horse horse=new Horse();//饿汉式
    
    private VehiclesFactory(){}
    public static Horse getHorse(){
        //return new Horse();
        return horse;
    }
    public static Boat getBoat(){
        return new Boat();
    }
}

```



## 枚举和注解

 

要求创建季节对象 请设计并完成



```java
package com.zzx_.enum_;

/**
 * @author 芝士蔡徐坤
 * @version 1.0
 */
public class Enumeration01 {
    Season spring=new Season("春天","温暖");
    Season summer=new Season("夏天","炎热");
    Season autumn=new Season("秋天","凉爽");
    Season winter=new Season("冬天","寒冷");
    //因为对于季节而言 它的对象时固定的四个 不会有更多的
    //不能体现季节时固定的对象 因此这样的设计不好
    //这样的设计不好=>枚举类【枚：一个一个 举：例举 即把具体的对象一个一个列举出来】
}
class Season{
    private String name;
    private String desc;//描述

    public Season(String name, String desc) {
        this.name = name;
        this.desc = desc;
    }

    public String getName() {
        return name;
    }

    public void setName(String name) {
        this.name = name;
    }

    public String getDesc() {
        return desc;
    }

    public void setDesc(String desc) {
        this.desc = desc;
    }
}
```

**分析问题**

创建Season对象有如下特点

1.季节的值是有限的几个值(Spring summer autumn winter)

2.只读 不可修改



**解决方案**-**枚举**

**1.枚举是一组常量的集合**

**2.枚举属于一种特殊的类 里面只包含一组有限的特定的对象**



### 枚举的两种实现方式



**1.自定义类实现枚举**

**2.使用enum关键字实现枚举**



#### 自定义类实现枚举



```java
package com.zzx_.enum_;

import com.sun.xml.internal.ws.api.model.wsdl.WSDLOutput;

/**
 * @author 芝士蔡徐坤
 * @version 1.0
 */
public class Enumeration02 {
    public static void main(String[] args) {
        System.out.println(Season.AUTUMN);
        System.out.println(Season.SPRING);
    }
}

//演示自定义枚举实现
class Season{
    private String name;
    private String desc;//描述

    //固定了四个对象
    public final static Season SPRING=new Season("春天","温暖");
    public final static Season SUMMER=new Season("夏天","炎热");
    public final static Season AUTUMN=new Season("秋天","凉爽");
    public final static Season WINTER=new Season("冬天","寒冷");

    //1.将构造器私有化 防止直接new
    //2.去掉setXXX防止属性被修改
    //3.在Season内部创建固定的对象
    //4.可以再加入final修饰符优化 防止类的加载
    private Season(String name, String desc) {
        this.name = name;
        this.desc = desc;
    }

    public String getName() {
        return name;
    }


    public String getDesc() {
        return desc;
    }

    @Override
    public String toString() {
        return "Season{" +
                "name='" + name + '\'' +
                ", desc='" + desc + '\'' +
                '}';
    }
}

```



#### **使用enum关键字实现枚举**



**如果使用了枚举类**

**1.使用关键字enum替代class**

**2.用WINTER("冬天","寒冷");替代**

**3.如果有多个对象用,间隔即可**

**4.如果用enum实现枚举 要求将常量对象写在最前面(语法规定)**

```java
package com.zzx_.enum_;

/**
 * @author 芝士蔡徐坤
 * @version 1.0
 */
public class Enumeration03 {
    public static void main(String[] args) {
        System.out.println(Season3.AUTUMN);
        System.out.println(Season3.WINTER);
    }
}
enum Season3{

    //如果使用了枚举类
    //1.使用关键字enum替代class
    //2.用WINTER("冬天","寒冷");替代
    //3.如果有多个对象用,间隔即可
    //4.如果用enum实现枚举 要求将常量对象写在最前面(语法规定)
    SPRING("春天","温暖"),
    SUMMER("夏天","炎热"),
    AUTUMN("秋天","凉爽"),
    WINTER("冬天","寒冷");

    private String name;
    private String desc;//描述

    private Season3(String name, String desc) {
        this.name = name;
        this.desc = desc;
    }

    public String getName() {
        return name;
    }


    public String getDesc() {
        return desc;
    }

    @Override
    public String toString() {
        return "Season{" +
                "name='" + name + '\'' +
                ", desc='" + desc + '\'' +
                '}';
    }
}

```





##### enum关键字实现枚举注意事项





**通过javap反编译**

![image-20220916112302064](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220916112302064.png)



![image-20220916112506301](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220916112506301.png)





![image-20220916115925733](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220916115925733.png)



![image-20220916120600116](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220916120600116.png)





![image-20220916122323557](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220916122323557.png)

```java

package com.hspedu.enum_;

public class EnumMethod {
    public EnumMethod() {
    }

    public static void main(String[] args) {
        Season2 autumn = Season2.AUTUMN;
        System.out.println(autumn.name());
        System.out.println(autumn.ordinal());
        Season2[] values = Season2.values();
        System.out.println("===遍历取出枚举对象(增强for)====");
        Season2[] var3 = values;
        int var4 = values.length;

        for(int var5 = 0; var5 < var4; ++var5) {
            Season2 season = var3[var5];
            System.out.println(season);
        }

        Season2 autumn1 = Season2.valueOf("AUTUMN");
        System.out.println("autumn1=" + autumn1);
        System.out.println(autumn == autumn1);
        System.out.println(Season2.AUTUMN.compareTo(Season2.SUMMER));
    }
}

```



**练习**



```java
package com.zzx_.enum_;

/**
 * @author 芝士蔡徐坤
 * @version 1.0
 */
public class EnumExercise02 {
    public static void main(String[] args) {
        //1.获取所有的枚举对象
        Week3[] weeks=Week3.values();//
        for(Week3 week:weeks){//将weeks每个对象一个一个给week
            System.out.println(week);
        }
    }
}
enum Week3{


    MONDAY("周一"),
    TUESDAY("周二"),
    WEDNESDAY("周三"),
    THUERSDAY("周四"),
    FRIDAY("周五"),
    SATURDAY("周六"),
    SUNDAY("周日");
    private String day;

    Week3(String day) {
        this.day = day;
    }

    @Override
    public String toString() {
        return "今天是" + day;
    }
}
```



**enum细节**



1.使用enum关键字后 **就不能再继承其他类了** 因为enum会隐式继承Enum 而java是单继承机制

2.枚举类和普通类一样 **可以实现接口** 如下形式

enum类名 implements 接口1 接口2{ }





### 注解



#### @Override

![image-20220917094528550](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220917094528550.png)

![image-20220917094602484](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220917094602484.png)

![image-20220917094919292](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220917094919292.png)





如果写了@Override注解 编译器就会检查该方法是否真的重写了父类的方法 

如果重写了 编译通过 如果没有 则编译错误



#### @Deprecated

![image-20220917095157939](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220917095157939.png)

@Deprecated 修饰某个元素 表示该元素已经过时

即不推荐使用 但是仍然可以使用



#### @SupperssWarnings



1.当我们不希望看到这些警告时 可以使用SupperWarning抑制警告

2.再{" "}中 可以写入你希望抑制的警告信息

3.作用范围是和你放置的位置相关  比如@SupperWarning放置再main方法中 抑制范围就在main方法



#### 元注解



![image-20220917101229788](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220917101229788.png)

![image-20220917101244095](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20220917101244095.png)































































































































