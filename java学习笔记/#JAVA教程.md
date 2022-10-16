# JAVA教程



## Java 基础知识

- JDK = JRE + Java开发工具（如编译工具javac.exe）

- JRE = JVM + **核心类库**

- Java核心类库：Java自带很多实用的包，这些包中定义了很多类库

- 环境变量配置作用：为dos在任意目录，都可以直接使用javac和java命令

- 环境变量配置方法：

  1. 此电脑->属性->高级系统设置->环境变量->设置JAVA_HOME = 指向JDK安装的主目录`D:\JDK8\jdk8`

     /*这里变量是用户变量 如naruto的用户变量：意思是对当前用户生效的环境变量，而系统变量是对所有用户都生效的环境变量*/

  2. 也是在环境变量中找到 path，编辑path变量，添加`%JAVA_HOME%\bin`

     /*这里的%JAVA_HOME%相当于D：\JDK8\jdk8这个路径，用JAVA_HOME是为了后面如果要修改，可以直接修改JAVA_HOME这个变量的路径指向而不是直接修改路径*/

- Java代码编写步骤

  1. 编写代码
  2. javac 编译 ，得到对应的`.class`字节码文件
  3. java 运行 ，本质是将 `.class`文件加载到 JVM 中运行

 ## Java快速入门--hello world

+ hello world 的编译 在cmd中用javac hello.java来编译

- 如果加了中文注释，有可能编译失败，因为格式对不上，在cmd中的属性看使用的是GBK格式，在sublime的file里将save with encoding改为GBK保存之后，即可编译成功

+ cmd中 在编译之后，用java hello 即可运行，不要用java hello.class这样会找不到类，因为java后面就是类名

- cmd使用技巧，上键可以直接调用上一个指令，Tab是快速补全

  

## Java执行流程

- .java文件 通过javac编译生成 .class文件**（字节码文件）**
- 通过java将.class文件装载到**JVM虚拟机**运行文件



## Java开发细节

- java源文件以.java为拓展名，基本组成部分是**类（class）**如hello类

- Java应用程序的执行入口是main（）方法书写格式是

  ```java
  public static void main(String [] args){
      ···
  }
  ```

- 一个源文件最多只能有==一个public类== 若一个类里面有多个类，编译源文件之后这几个类都会被编译成对应的class文件

- 源文件名必须和public类的类名一致（这也是为什么public类只能有一个）

- public类只能有一个，但其他的类不做限制

- **可以将main方法写进非public类中，然后指定运行非public类，这样入口方法就是非public的main方法**

  ```java
  public class Hello{
      public static void main(String [] args){
          System.out.println("hello world");
      }
  }
  class Dog{
      public static void main(String [] args){
          System.out.println("hello dog");
      }
  }
  class Tiger{
     public static void main(String [] args){
          System.out.println("hello tiger");
      }
  }
  ```

  **在cmd中编译源文件之后会形成三个.class文件 分别是Hello.class/Dog.class/Tiger.class**

  **下面可以运行三个主方法**

  1. `java Hello `    输出 `hello world`
  2. `java Dog`输出`hello dog`
  3. `java Tiger`输出`hello tiger`

- **注意不能在去掉main方法就打印，会报错**

  ```java
  class Dog{
      System.out.println("hello dog");
  }
  //这样是绝对错误的！！！
  ```



## 转义字符

- ctrl+/是多行注释的快捷键

- Tab可以快速补全cmd指令，用法就是：输入javac Change 按下Tab 直接补全为 javac ChangeChar.java

- Java常用转义字符

  1. \t：一个制表位，实现对齐的功能**（左对齐）**

     ```java
     System.out.println("北京\t上海\t广州");
     //结果是
     北京	上海	广州
     ```

  2. \n:换行符

     ```java
     System.out.println("jack\nsmith\nmary");
     //输出结果
     jack
     smith
     mary
     ```

  3. \\\：一个\

     ```java
     //System.out.println("D:\javacode") 这里一定会报错，因为\会连着后面的j，要么是变成其他转义字符，要么就是直接报错。
     System.out.println("D:\\javacode");
     //用\\来表示一个\ 这也是为什么磁盘路径是单斜杠，但在代码里写磁盘路径都得用双斜杠，因为两个双斜杠才表示一个单斜杠
     //要是想表是\\双斜杠，就得用\\\\四个斜杠来表示双斜杠
     ```

     

  4. \\"：一个"

     ```java
     System.out.println("我说：“好好学java”");//完全没问题，因为""里面的是中文的“”所以不会有歧义
     输出：我说：“好好学java”
     System.out.println("我说："asdasdasd"");//错误！！，因为""里面的是英文的""起冲突了。
     报错！！
     System.out.println("我说：\"asdasfvs\"");//完全没问题，因为可以用\"表示一个"是字符串一部分
     输出：我说："asdasdasd"
     ```

  5. \\':一个'

     ```java
     System.out.println("我说:\'sadasdasd\'");
     输出：我说'sadasdasd'
     ```

  6. \r:回车**回退到本行第一个字符**

     ```java
     System.out.println("韩顺平教育\r北京");
     输出：北京平教育
     //原因是：先输出韩顺平教育 再回车光标回退到第一个字符 韩，然后输出北京，覆盖了韩顺两个字
     System.out.println("韩顺平教育\r\n北京");
     韩顺平教育
     北京
     ```

     

##  易犯错误

- 找不到文件

  问题：当出现**找不到文件**信息，一般是cmd中文件名写错了

- 公共类与文件名不匹配

  问题：当出现**····是公共的**，一般是主类（公共类）与文件名不一致

- 忘记写分号了

  问题：出现提示信息 第几行需要分号



##  注释

- 单行注释

- 多行注释：多行注释里面切记不要再加入多行煮熟

  ```java
  /*
  	····
  	/*
      ···
  	*/
  */
  这样会出错！！因为/*表示注释开始，*/表示注释结束，这里嵌套多行注释，再遇到第一个*/就表示注释结束，下面的*/就被孤立，会报错！！
  ```

- 文档注释：

  （注释内容可以被JDK提供的工具javadoc所解析，生成一套用网页文件形式体现的该程序的说明文档）

  - 基本格式

  ```java
  /**
   *@author fsbbts 
   *@version  1.0
  */
  文档注释的固定格式：多行注释的形式，第一行多加一个*，此后注释里每写一行都要加* 然后加@author之类的javadoc标签
  ```

  - 如何生成对应的文档注释

    在cmd中输入

    `javadoc -d 目标文件名（文档注释放在哪里）-xx -yy（生成的javadoc标签）源文件名.java`

    例： `javadoc -d d:\\temp -author -version Comment.java`

    **注意，这里的目标文件 的路径用\\**\

    tips：cmd中的cls是清屏指令

  - 生成实例：打开目标文件夹里的index.html即可看到文档注释

##  补充 Typora上传至github

- 在github上创建repository，复制地址
- 打开md文件所在处，右键点击git Bash here（若是在desktop打开的 用cd指令进入md文件所在处）
  1. git clone https://github.com/fsbbts/Java_Note.git 本地与github建立联系
  2. git add *
  3. git commit -m "这里写一些文字说明"
  4. git push -u origin main
- 后续更新
  1. 更新md文件后保存
  2. git add *
  3. git commit -m "文字说明"
  4. git push -u origin main



##  代码规范

1. 类，方法用javadoc来写
2. 非javadoc注释，用单行/多行注释，用以给代码维护者看
3. 整体后移：选中之后按Tab
4. 整体前移：选中之后按shift+Tab
5. 运算符和 = 两边多加一个空格
6. 源文件用 utf-8进行编码，这里是因为在DOS系统中有中文字符不得已用GBK，正常都是用utf-8
7. 编码使用：行尾风格/次行风格



##  DOS命令(不是重点)

**相对路径与绝对路径**

相对路径：从当前目录开始定位，形成一个路径

`..\..\abc2\test200\hello.txt`

绝对路径：从顶级目录d，开始定位，形成一个路径

`d:\abc2\test200\hello.txt`

1. 查看当前目录：`dir`   `dir d:\abc2\test200`
2. 切换根目录 `cd \D c:`
3. 切换到当前目录其他目录下`cd d:\abc2\test200`   `cd ..\..\abc2\test200`
4. 切换到上一级`cd ..`
5. 切换到根目录`cd \`
6. 查看当前目录的所有子目录 `tree d:` `tree d:\abc2`
7. 清屏`cls`
8. 退出DOS `exit`



##  变量

**使用方法：**

```java
//声明变量
int a;
//变量赋值
a = 60;
//输出变量
System.out.println(a);


//实例（包括各类变量）
public class var02{
    public static void main(String[] args){
        int age = 3000;
        double height = 165.0;
        char gender = 'M';
        String name = "wendy"; //注意String 中的大写s
        System.out.println(name);
        System.out.println(gender);
        System.out.println(age);
        System.out.println(height);
//这里不好加中文，因为没有GBK格式 导致编译时会报错
    }
}
```



## “+”的使用

```java
//两边都是数字，做算术加法运算
System.out.println(98 + 19); //输出117

//两边有一边是字符串， 做拼接运算
System.out.println("98" + 19); //输出9819 

```



## 数据类型

- 基本数据类型：数值型， 字符型， 布尔型

  - 数值型：

    - 整数类型（byte[1], short[2], int[4], long[8]）

    - 浮点类型(float[4], double[8])

  - 字符型：

    - char[2] (英文占1B，中文占2B)

  - 布尔型：

    - boolean[1] , 只有true，false

- 引用数据类型：类（class），接口（interface），数组[ ]



## 整数使用

- byte:   `-128~127` （1个字节）
- short: $-2^{15}$~$2^{15} - 1$    -3万~+3万   （2个字节）
- int: $-2^{31}$ ~  $2^{31} - 1$     大概是$10^9$这个量级  （4个字节）
- long: $-2^{63}$ ~ $2^{63} - 1$   大概是$10^{18}$这个量级   （8个字节）

细节：

```java
int n1 = 1L; //报错！long转化成int会造成数据丢失，改为 long n1 = 1L;
```



## 浮点数使用

- float : 4个字节
- double: 8个字节

细节：

1. 浮点数在计算机的存储：1位符号位+8位指数位+23位有效数字（IEEE754标准，针对32位）

2. java中的浮点数常量如1.1，默认是double类型，声明float需要在其后加f/F如1.1f/F,double比float更精确

3. 表示形式：5.12    5.12f  .512    /   5.12e2    5.12E-2

4. **attention!**:8.1/3的结果不是2.7 而是2.666669这是二进制运算的问题，所以在进行浮点数判断相等格外小心！**判断小数相等应该是用两个数相减 结果的绝对值比一个很小的数还小**

   ```java
   if(Math.fabs(a1 - a2) < 1e-8)
   ```

   但是如果直接赋值2.7给a1,a2那么a1 == a2



## Java API文档使用

- API(Application Programming Interface ) 应用程序编程接口

- 中文在线文档https://www.matools.com/api

- java类的组织形式

  ```java
  JDK:里面有包1，包2，包3……
  包里面有：接口，类，异常……
  类里面有：字段，构造器（构造方法），成员方法（方法）
  ```

  

## Char字符使用

- 字符是`''`而不是`""`括起

- `\`表示转义，`'\t'`合起来是转义字符

- 每一个字符对应一个Unicode编码，类似于ASCII码

- char可以参与运算，实质上是整数

  ```java
  System.out.println('a' + 10); //输出的是97+10 => 107 
  char c = 'a' + 10;
  System.out.println((int) c); //输出 107
  System.out.println(c); //输出k
  ```

  

**补充**：ASCII, GBK，Unicode，UTF-8,UTF-32

1. ASCII标准字符集是最开始美国人将他们所有用的字符通过特定编码形成的0~127，总共128个字符，还不满足一个字节存储，所以ASCII码的二进制形式开头都是0
2. 而汉字大概有2万个，用ASCII肯定不够，所以我们就创造了GBK汉字编码字符集，每个汉字用唯一的两个字节的二进制01存储，为了与ASCII区别，GBK汉字的开头是1，留下15位表示汉字，可以表示3万多汉字，足够我们使用，同时GBK兼容ASCII码，英文和数字还是跟原来一样1个字节保存

3. 而如果每个地区都有各自的字符集，那么B字符集打开A字符集文件会出现乱码，为避免这种情况，统一字符集，出现了国际组织制定的Unicode统一码、万国码可以容纳世界上所有的文字，符号，统一进行编码，同样兼容ASCII码

​		Unicode有若干编码方案：

-  UTF-32
  - 固定用4个字节来表示一个字符，4个字节大概是10的9次方，绝对可 以满足包含世界上所有的符号与文字，且固定用4个字节方便解码，固定4个字节的扫，不用担心英文1个字节汉字两个字节的问题了
  - 但是这样太浪费空间了，英文字符原本ASCII码只需要8个bit位，现在需要32位，且前24位都固定为0浪费空间

- UTF-8

  - 采取可变长编码方案，共分为4个长度区：1个字节，2个字节，3个字节，4个字节
  - 汉字占3个字节，英文和数字还是1个字节，兼容ASCII码
  - 对于1个字节的0xxxxxxx，以0开头
  - 对于2个字节的110xxxxx 10xxxxxx
  - 对于3个字节的1110xxxx 10xxxxxx 10xxxxxx
  - 对于4个字节的11110xxx 10xxxxxx 10xxxxxx 10xxxxxx

  通过这种形式，进行编码和解码，编程时默认用UTF-8字符集

  **注意**：1. 字符编码使用的字符集和字符解码使用的字符集必须一致否则出现乱码

  ​            2.英文，数字一般不会出现乱码，因为很多字符集兼容了ASCII码

​       例：用GBK字符集写`a我b`，其二进制表示是`0xxxxxxx 1xxxxxxx xxxxxxxx 0xxxxxxx`

​              用UTF-8解码二进制`0xxxxxxx`解码出a,`1xxxxxxx xxxxxxxx`无法与它的规则对应 解码出？ ？

​                                               `0xxxxxxx`解码出b，最后加上`a??b`



## 布尔类型

- java中的布尔类型是`boolean`,占一个字节，只有两个值`true` , `false`



## 类型转换

1. 自动类型转换：低精度可以自动转换成高精度，反过来报错（因为会精度丢失）

`    double a = 8;`   `int c = 'a';`

- 浮点数默认是double类型

  `float a = 10 + 1.1;//报错！`因为1.1默认是double 转换为float会精度丢失

  将其改为`float a = 10 + 1.1F; 或者 double a = 10 + 10.1;`

- char -> int

- byte -> short -> int

  但是char 和 byte 和short 不能直接自动类型转换

  ```java
  byte b = 10;//只要是-128~127 都可以存
  char a = b;//报错！
  ```

- char，byte，short不能相互转换，但能相互运算，会统一转换成int型再计算

- boolean不参与精度转换
- 运算时，表达式结果自动提升为精度最高的类型



2. 强制类型转换：高精度转换为低精度，会造成精度丢失和数据溢出

   ```java
   int n1 = (int)1.9; //n1 = 1;精度丢失
   byte n2 = 2000;
   //n2 = -48; 2000=11111010000B,截断为1byte得11010000B这是原码，转换为补码得10110000B=-48D
   ```

- char 类型可以保存int常量，但不能保存int变量
- 强制类型只对最近右侧操作数有效，可以加括号改变优先级

**注意：**数据转换最容易出错就是精度丢失

```java
byte c = 10;
c = c - 9;//报错，因为-9已结将表达式的精度转换为int，int再赋值给byte会精度丢失报错
```



## 基本类型和String之间的转换

- 基本类型转换为String：直接后面加上 `+ ""`即可

  ```java
  int n1 = 100;
  String str1 = n1 + "";
  float n2 = 1.1;
  String str2 = n2 + "";
  ```

- String转换为基本类型

  ```java
  int n1 = Integer.parseInteger("123"); //n1 = 123;
  double n2 = Double.parseDouble("1.1"); //n2 = 1.1;
  boolean n3 = Boolean.parseBoolean("true"); //n3 = true;
  ```

- String -> char

  ```java
  String s5 = "123";
  System.out.println(s5.charAt(1)); //输出第一个字符'2'
  ```

- 细节：

  ```java
  String s = "hello"; //这个无法转换成整数，编译不报错，，运行报错，格式不正确，抛出异常！！
  //Expception in thread main...
  ```

- 字符串相加：只要左右有一方是字符串，`+` 就是字符串的拼接

- 字符相加：就是整数相加，返回一个整数



## 第四章 运算符

- 算术运算符：数值类型变量的运算 + ，-，*，/，++，--，%

  ```java
  //除法细节：
  System.out.println(10 / 4); //输出的是2
  System.out.ptintln(10.0 / 4); //输出的是2.5
  double m = 10 / 4; //输出的是2.0
  
  //取模细节： a % b = a - a / b * b;
  System.out.println(10 % 3); //输出1
  System.out.println(10 % -3); //10 - 10 / (-3) * (-3) = 10 - 9 = 1; 
  System.out.println(-10 % 3); //(-10) - (-10) / 3 * 3 = (-10) + 9 = -1;
  System.out.println(-10 % -3);// (-10) - (-10) / (-3) *(-3) = (-10) + 9 = -1;
  
  ```


​		格式化输出：（如保留几位有效数字）跟字符串有关，后面讲

- 关系运算符：

  `instanceof`是否某一个实例是某一个类的对象

  ```java
  if("hsp" instanceof String) //true是的，false不是
  ```

- 逻辑运算符：

1.  &&短路与和&逻辑与 :

    a & b 和 a && b 都只有当a，b都为true时结果才为true

     ```java
     //区别:&&会短路，当第一个为false第二个就不会执行，但是&不管前面是true还是false，都会执行左右两边
     int a = 4, b = 10;
     if(a < 4 && ++b < 50) //因为a < 4 为false且是&& 所以短路 b = 10,不会自增
     if(a < 4 & ++b < 50) //因为是&，所以不管前面a 是否 < 4 ，b都会自增为11
     
     ```

2. ||短路或和|逻辑或：

   a || b 和 a | b只要一个为true，结果为true

   ```java
   //区别：类似于短路与和逻辑与，短路或只要第一个为true就不会执行第二个，逻辑或不管第一个是否true，都会执行第二个
   int a = 4, b = 10;
   if(a == 4 || ++b < 50) // b = 10, 不变
   if(a == 4 | ++b < 50)  // b = 11，自增
   ```

- 所以短路与和短路或的效率比逻辑与和逻辑或的效率要高！

3. 取反 ！：true为false，false为true

4. 异或 ^: 不同为true，相同为false

- 赋值运算符：

  +=， -=， *=，/=, %= 等

- 三元运算符：

  条件表达式 ？表达式1 ：表达式 2

  若条件为true，执行表达式1，运算后的结果就是表达式1的结果

  若条件为false，执行表达式2，运算后的结果就是表达式2的结果

  ```java
  //注意
  int a = 10, b = 1;
  int c = a > b ? a ++ : b--; //这里c为10，a++赋值给c，先赋值再自增
  ```

  **这里表达式1,2最后赋值给c一定要满足类型转换的条件，不能丢失精度**
