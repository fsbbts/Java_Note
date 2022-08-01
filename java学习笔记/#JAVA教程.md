# JAVA教程



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



## Java转义字符

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

     

## Java 易犯错误

- 找不到文件

  问题：当出现**找不到文件**信息，一般是cmd中文件名写错了

- 公共类与文件名不匹配

  问题：当出现**····是公共的**，一般是主类（公共类）与文件名不一致

- 忘记写分号了

  问题：出现提示信息 第几行需要分号



## Java 注释

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
   *@author szd 
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

## Java 补充 Typora上传至github

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
