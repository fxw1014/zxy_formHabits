## 1. 编程基础

本质上计算机只会执行预先写好的指令，指令是操作数据或者设备。

---

程序就是告诉计算机要操作的数据和执行的指令序列。

---

所有的数据都需要放到内存中进行处理，程序很大一部分就是操作内存中的数据

---

数据在计算机内部是二进制表示的，若用程序直接操作二进制代码，编程难度过大，故高级语言引入了<font color='red'>数据类型和变量的概念</font>

### 1.1 基本类型和变量

### 1.2 赋值

数组的长度在定了之后不可变，如下操作会编译报错，因为length是final修饰的

```java
String[] strs = {"1","2"};
strs.length = 0;//想通过将数组的长度变为0，从达到清空数组的目的
```

### 1.3 基本运算

整数相除的结果总是整数，在以下代码中得到的结果均是整数；

整数相除若结果位有小数是直接舍弃小数位，而不是四舍五入;

> 【注】：2.0应该也是整数吧？哈哈

```java
int x = 5;
int y = 2;
int c = x/y; // 2
double d = x/y; // 2.0
```

### 1.4 条件执行

条件执行依赖于条件跳转指令和无条件跳转执行，如下解释

```java
boolean flag = true;
if(flag){
  sout
}
sout
```

```java
boolean flag = true;
if(flag)则条件跳转到第3行
若不满足上一步跳转条件，则无条件跳转到第5行
```

### 1.5 循环

> * 多次重复执行某些类似的操作，如展示一张张照片，显示一条条聊天记录，播放循环播放音乐,过滤数据等
> * 循环的4中形式
>     1. while
>     2. do/while
>     3. for
>     4. foreach

#### 循环中4中形式

1. while

    该语法与if语法类似,但是通常在循环体中存在循环中断或退出的条件；若没有该条件的就是个死循环了

    ```java
    while(condition){
      //do sth;
    }
    if(condition){
      //do sth;
    }
    ```

2. do/while

    如果不管条件语句是什么，代码块都会至少执行一次，则可以使用do/while循环

    ```java
    do{
      //do sth;
    }while(condition)
    ```

3. for

    需要注意for循环的执行流程,在以下流程中变量步进是在执行循环体之后的；

    1. 执行初始化命令
    2. 判断循环是否满足条件
    3. 若满足循环条件则执行循环体，否跳出循环
    4. <font color ='red'>变量自增或自减（步进）</font>
    5. 无条件跳转到第2步

    ```java
    for(变量初始化;循环判断条件;步进){
      do sth;
    }
    
    for (int i = 0; i < 10; i++) {
      System.out.println(i);
      //i++
    }
    
    for (int i = 0; i < 10; ++i) {
      System.out.println(i);
      //++i
    }
    ```

    

4. foreach

    该遍历过程中不存在索引变量，对于循环体中需要用到索引变量的情况不适用，但这种方式遍历更加简洁；

    ```java
    for(变量类型 变量 : 数组或集合)
    {
      //do sth;
    }
    ```

### 1.6 函数

> 函数：减少重复代码和分解复杂操作，使程序更加简洁，增加代码的可读性。
>
> 函数的返回值：
>
> * 函数需要返回多个相同类型的值，可以使用数组或者集合作为返回类型；
> * 函数需要返回的是一个复合值，如一个人的姓名、性别、年龄、生日等可以用类作为返回值；

---

#### 递归应用

> * 0的阶乘是1

```java
//递归二分查找
 /**
     * 递归操作 需要四个参数
     *
     * @param desArr 需要遍历的数组 有序
     * @param key    需要查找的值
     * @param start  查找开始的范围值
     * @param end    查找结束的范围值
     * @return 查找值在数组中的位置
     */
    public static int binarySearch(int[] desArr, int key, int start, int end) {
        //数组遍历完毕 找不目标数
        if(start > end){
            return -1;
        }
//        得到中间数
        int mid = start + (end - start)/2;
        //判断中间下标对应数组中的值与开始、结尾对应的数组中的值的大小关系
        if(desArr[mid] > key){
            return binarySearch(desArr,key,start,mid-1);
        }else if(desArr[mid] < key){
            return binarySearch(desArr,key,mid + 1,end);
        }else {
            return mid;
        }

    }

//阶乘
 public static int diGuiMulitp(int n){
        if(n <= 1){
            return 1;
        }
        return diGuiMulitp(n - 1) * n;
    }
```

```java
 /**
     * 二分查找非递归-while，由于二分查找在循环体中会操作循环控制变量start,end故使用while循环更好,while形式先定义变量最后返回变量的值，通用的一个操作形式，如本例中的result;
     * @param desArr 需要遍历的数组 有序
     * @param key
     * @param start
     * @param end
     * @return
     */
    public static int binarySearchWhile(int[] desArr, int key, int start, int end){
        int result = -1;
        while(start <= end){
            int mid = start + (end - start)/2;
            if(desArr[mid] > key){
                end = mid -1;
            }else if(desArr[mid] < key) {
                start = mid + 1;
            }else {
                result =  mid;
                break;
            }
        }
        return result;
    }
/**
阶乘的for循环
*/
public static int mulitpWhile(int n){
        int result = 1;
        for (int i = n; i > 1; i--) {
            result = result * i;
        }
        return result;

    }
//阶乘的while循环
public static int mulitpWhile(int n){
        int result = 1;
        while(n > 1){
            result = result * n;
            n--;
        }
        return result;

    }
```

---

#### 冒泡排序

```java
//冒泡排序
 public static void sortBubble(int[] desArr){
        for (int i = 0; i < desArr.length; i++) {
            for (int j = 0; j < desArr.length -1 - i; j++) {
                if (desArr[j]  > desArr[j+1]) {
                    int temp = desArr[j];
                     desArr[j] = desArr[j+1];
                     desArr[j+1] = temp;
                }
            }
        }

    }
```

---

#### int数组->list<Integer>->Integer[]

> [https://blog.csdn.net/ASDQWE09876/article/details/79271992](参考)

```java
//int数组转List<Integer>

List<Integer> integerList = Arrays.stream(intArr).boxed().collect(Collectors.toList());
//List<Integer>转int数组
intArr = integerList.stream().mapToInt(Integer::intValue).toArray();

//int数组转Integer[]
Integer[] integerArr = Arrays.stream(intArr).boxed().toArray(Integer[]::new);
//Integer[]转int[]

intArr  = Arrays.stream(integerArr).mapToInt(Integer::valueOf).toArray();
```

#### 函数调用的参数匹配

1. 是否有原配，即参数类型是否一模一样
2. 是否存在可以自动转换的参数类型，即小转大
    * 高精度 -> 低精度 short、byte、char -> int -> long -> float -> double
    * 子类 -> 父类
        * 参数类型是父类型，传入子类对象可以
    * 接口 -> 实现

#### 函数调用的基本原理

> 程序从main函数开始顺序执行，函数调用可以看作一个无条件跳转，跳转到对应函数的指令处开始执行，碰到return语句或者函数结尾的时候，再执行一次无条件跳转，跳转回调用方，执行调用函数后的下一条指令。
>
> 但这里面有几个问题。1）参数如何传递？2）函数如何知道返回到什么地方？在if/else、for中，跳转的地址都是确定的，但函数自己并不知道会被谁调用，而且可能会被很多地方调用，它并不能提前知道执行结束后返回哪里。3）函数结果如何传给调用方？
>
> 解决思路是使用内存来存放这些数据，函数调用方和函数自己就如何存放和使用这些数据达成一个一致的协议或约定。这个约定在各种计算机系统中都是类似的，存放这些数据的内存有一个相同的名字，叫栈。
>
> 栈是一块内存，但它的使用有特别的约定，一般是先进后出，类似于一个桶，往栈里放数据称为入栈，最下面的称为栈底，最上面的称为栈顶，从栈顶拿出数据通常称为出栈。栈一般是从高位地址向低位地址扩展，换句话说，栈底的内存地址是最高的，栈顶的是最低的。
>
> 栈来存放函数调用过程中需要的数据，包括参数、返回地址，以及函数内定义的局部变量

![image-20210809225628197](assets/image-20210809225628197.png)

!(assets/image-20210809225439288.png)

![image-20210809225551978](assets/image-20210809225551978.png)

##### 【注】：待详细研究。

##  2. 理解数据背后的二进制

> 正整数相乘的结果居然出现了负数
>
> ```java
> 1000000000*1000000000 //-1486618624
> ```
>
> 非常基本的小数运算结果居然不精确
>
> ```java
> 0.1*0.1//0.010000000000000002
> 1.1*1.1//1.2100000000000002
> ```
>
> 字符类型也可以进行算术运算和比较

### 2.1 整数的二进制表示与位运算

#### 十进制的计算规则

123 => 1*10^2 + 2 * 10^1 + 3* 10^0

从右向左，第一位乘以10的0次方，第二位乘以10的1次方...

#### 正整数的二进制表示

1111 => 1*2^3 + 1 * 2^2 + 1*2^1 + 1 * 2^0

​	 => 2^3 + 2^2 + 2^1 + 2^0

#### 负整数的二进制表示

十进制的负数表示就是在前面加一个负数符号-，例如-123。但二进制如何表示负数呢？其实概念是类似的，二进制使用最高位表示符号位，用1表示负数，用0表示正数

##### 整数类型分配的内存大小

整数有4种类型byte、short、int、long，分别占1、2、4、8个字节，即分别占8、16、32、64位

##### 补码表示负数

负数表示并不是我们直觉中将最高位变1，例如byte a=-1，如果只是将最高位变为1，二进制应该是10000001，但实际上，它应该是11111111。

补码表示就是在原码表示的基础上取反然后加1。取反就是将0变为1,1变为0。负数的二进制表示就是对应的正数的补码表示，比如：-1 => 1的原码表示是00000001，取反是11111110，然后再加1，就是11111111。

给定一个负数的二进制表示，要想知道它的十进制值，可以采用相同的补码运算。比如：10010010，首先取反，变为01101101，然后加1，结果为01101110，它的十进制值为110，所以原值就是-110。

> [【秒懂】byte的取值范围为什么是-128~127？](https://www.jianshu.com/p/47761557bab0)

> [两个byte类型的数据相加最后结果为什么是int？即使接收相加结果的变量是byte型也会报错](https://blog.csdn.net/ejiao1233/article/details/82292348)

#### 十六进制

十六进制的表示：二进制写起来太长，为了简化写法，可以将4个二进制位简化为一个0～15的数， 10～15用字符A～F表示，这种表示方法称为十六进制

123 => 0x7B => 7 * 16^1 + 11 * 16^0

​			=> 7 * 16 + 11 * 16

   二进制	=> 0111 1011 

   Hex  	=>  7   B（11）

##### java中十进制、二进制、16进制之间的转换

```java
class Tcal{
    public static void main(String[] args) {
        int a = 0x7B;//16进制
        System.out.println(a);//123
        System.out.println(Integer.toBinaryString(a));//1111011
        System.out.println(Integer.toHexString(a));//7b
    }
}
```

#### 位运算

##### 移位运算

> 无符号右移：>>>
>
> 有符号右移: >> 
>
> 左移：<<

左移 << 向左移动，右边低位补0，高位舍去，左移相当于*2

* 左移 << 不区分有无符号左移，使用同一个符号即可

无符号右移 >>> 向右移动，低位舍去，高位补0，相当于/2

有符号右移 >>> 向右移动，低位舍去，高位原来是1就补1，是0就补0，相当于/2

```java
 byte b = -4;
        System.out.println(b << 2);//左移 负数 -16
        System.out.println(b >> 2);//右移 负数 -1 有符号右移
        /*
        一个变量byte x = -4在进行移位运算时，这个变量是负数，移位运算时无符号位的右移操作,
        最终结果是1073741823 => 2^31 -1，也就是将负数int x = -4，x有32个位进行了右移操作；
        但为什么byte会自动转换为int然后无符号操作呢？
         */
        System.out.println(b >>> 2);//右移 负数 1073741823 无符号右移 2^31 -1

        byte c = 4;
        System.out.println(c << 2);//左移 正数 16
        System.out.println(c >>> 2);//右移 正数 1 无符号右移
        System.out.println(c >> 2);//右移 正数 1 有符号右移
```



##### 逻辑运算

> & : 与操作 
>
> | ： 或操作 
>
> ~ ： 取反操作
>
> ^ :  异或操作 => 相同为0，相反为1

两边的操作数转换成二进制做逻辑运算。

```java
int a = 10;
System.out.println(a & 0x1);//0
System.out.println(a & 1);//0
System.out.println(a & 2);//2
```

### 小数的二进制表示

如下例子中x * y的结果不精确，并非我们直观的0.01这是为什么呢？

> 实际上，不是运算本身会出错，而是计算机根本就不能精确地表示很多数，比如0.1这个数。计算机是用一种二进制格式存储小数的，这个二进制格式不能精确表示0.1，它只能表示一个非常接近0.1但又不等于0.1的一个数。数字都不能精确表示，在不精确数字上的运算结果不精确也就不足为奇了。
>
> 包括0.1+0.1虽然我们看到的结果是0.2但实际上这也是经过计算机处理的结果，不是计算机真正计算的结果。

```java
double x = 0.1;
double y = 0.1;
double s = x * y;
System.out.println(s);//0.010000000000000002
double xx = 0.01;
double yy = 0.01;
double ss = xx * yy;
System.out.println(ss);//1.0 * 10^-4
```

首先我们来看十进制：十进制也只能表示那些可以表述为10的多少次方和的数，比如12.345，实际上表示的是1× 10+2× 1+3× 0.1+4×0.01+5× 0.001，与整数的表示类似，小数点后面的每个位置也都有一个位权，从左到右，依次为0.1,0.01,0.001…即10^(-1),10^(-2),10^(-3)等。

很多数十进制也是不能精确表示的，比如1/3，保留三位小数的话，十进制表示是0.333，但无论后面保留多少位小数，都是不精确的，用0.333进行运算，比如乘以3，期望结果是1，但实际上却是0.999。二进制是类似的，但二进制只能表示那些可以表述为2的多少次方和的数。来看下2的次方的一些例子：2^(-1) = 0.5 , 2^(-2) = 0.25,2^(-3) = 0.125,2^(-4) = 0.0625

> <font color = 'red'>既然使用二进制无法准确的表示某些小数，而计算机底层是二进制存储的，那0.1,0.01在计算机中是如何存储的呢？</font>
>
> * 计算机有一套"舍入"原则，对于无法精确表示的数，会以尽可能接近它的二进制数表示。
>
> 在平常计算中我们如何处理这种不精确的情况呢？
>
> 1. 不需要精确，只需要保留小数点多少位即可；使用四舍五入或者舍掉小数点即可满足要求
> 2. <font color = 'red'>需要精确，如何处理呢？为什么这么处理就精确了呢？</font>
>     * 转换为整数？
>     * 使用java类BigDecimal?

#### 浮点数

> 【参考链接】：
>
> * [计算机是怎么存储数字的](https://www.jianshu.com/p/d52a542bb363)
> * [0.1+0.2!==0.3引发的思考-浮点数的存储和计算](https://juejin.cn/post/6854573211607269384)

0.1 + 0.2 != 0.3

> 计算机根本就不能精确地表示很多数，比如0.1这个数。计算机是用一种二进制格式存储小数的，这个二进制格式不能精确表示0.1，它只能表示一个非常接近0.1但又不等于0.1的一个数。数字都不能精确表示，在不精确数字上的运算结果不精确也就不足为奇了。

计算机在表示浮点数 F,当碰到无法精确表示的情况下，会有一套默认的规则去"四舍五入"表是这个数F，使在计算机中的表示尽可能的接近这个数 F。

十进制整数 => 二进制整数

78 如何使用二进制表示？

对于正整数，数学上有一个转换的公式，就是「除 2 取余，逆序排列」法。具体做法是：用 2 整除十进制整数，可以得到一个商和余数；再用 2 去除商，又会得到一个商和余数，如此进行，直到商为 0 时为止，然后把先得到的余数作为二进制数的低位有效位，后得到的余数作为二进制数的高位有效位，依次排列起来。对于 78 这个十进制整数来说，对应的二进制是 1001110.

十进制小数 => 二进制小数

0.5 如何使用二进制表示？

对于纯小数，也有一个固定的转换法：乘 2 取整，顺序排列。具体做法就是：用 2 乘十进制小数，可以得到积，将积的整数部分取出，再用 2 乘余下的小数部分，又得到一个积，再将积的整数部分取出，如此进行，直到积中的小数部分为零，此时 0 或 1 为二进制的最后一位。对于十进制的 0.5 来说，对应的二进制表示就是 0.1

IEEE 754标准

> 几乎所有的硬件和编程语言表示小数的二进制格式都是一样的。这种格式是一个标准，叫做IEEE 754标准，它定义了两种格式：一种是32位的，对应于Java的float；另一种是64位的，对应于Java的double。
>
> 32位格式中，1位表示符号，23位表示尾数，8位表示指数。64位格式中，1位表示符号，52位表示尾数，11位表示指数。在两种格式中，除了表示正常的数，标准还规定了一些特殊的二进制形式表示一些特殊的值，比如负无穷、正无穷、0、NaN（非数值，比如0乘以无穷大））

### 字符的编码与乱码

#### 字符的编码

分为两大类，一类是非Unicode编码，一列是Unicode编码

常见的非Unicode编码包括ASCII、ISO8859-1、Windows-1252、GB2312、GBK、GB18030和Big5。

Unicode主要做了这么一件事，就是给所有字符分配了唯一数字编号。它并没有规定这个编号怎么对应到二进制表示，这是与上面介绍的其他编码不同的，其他编码都既规定了能表示哪些字符，又规定了每个字符对应的二进制是什么，而Unicode本身只规定了每个字符的数字编号是多少。

那编号怎么对应到二进制表示呢？有多种方案，主要有UTF-32、UTF-16和UTF-8。

#### 字符的乱码

编解码的方式不同导致，有些切换解码就可以，有些则不行，不行的情况下就需要挨个编码去编码解码，但最终不一定可以解决乱码问题。

#### char类型

>  Java中还有Character、String、StringBuilder等类用于文本处理，它们的基础都是char
>
> 为什么字符类型也可以进行算术运算和比较呢？它的本质到底是什么呢？
>
> char本质上是一个固定占用两个字节的无符号正整数，这个正整数对应于Unicode编号，用于表示那个Unicode编号对应的字符。
>
> 由于固定占用两个字节，char只能表示Unicode编号在65 536以内的字符，而不能表示超出范围的字符。那超出范围的字符怎么表示呢？使用两个char。类Character、String有一些相关的方法

##### char的几种赋值方式

```java
char a = 'A';//一个能用ASCII码表示的字符赋给一个字符变量

char a = '马'；

char a = 39532;//第3种赋值方式是直接将unicode十进制的常量赋给字符

char a = 0x9a6c;//将十六进制常量赋给字符

char a = '\u9a6c';//第5种赋值方式是按Unicode字符形式
```

##### char的算数运算

> 由于char本质上是一个固定占用两个字节的无符号正整数，所以可以进行整数能做的一些运算，<font color='red'>在进行运算时会被看做int类型，但由于char占用两个字节，所以运算结果不能直接赋值给char，需要进行强制类型转换，【注】这和byte、short参与整数运算类似</font>

从上述标红字体的描述中得到 => char，byte，short在参与整数运算时都会被看做int类型，即其参与运算最终的结果是int型，如果接受运算结果类型是char,byte,short就需要强制类型转化，否则会报错；以下是一些亲测示例：

```java
//byte,short,char类型参与运算 是看做int型参与运算的，最终结果也是int型
        byte a = 1;
        byte b = 1;
        int c = a + b;//2
        byte c = a + b;//error
        
        char a = '1';
        char b = '2';
        char c = a +b;//error
        int c = a + b;
        
        short a = '1';
        short b = '2';
        short c = a +b;//error
        int c = a + b;
```

> char的加减运算就是按其Unicode编号进行运算，一般对字符做加减运算没什么意义，但ASCII码字符是有意义的。比如大小写转换，大写A～Z的编号是65～90，小写a～z的编号是97～122，正好相差32，所以大写转小写只需加32，而小写转大写只需减32。加减运算的另一个应用是加密和解密，将字符进行某种可逆的数学运算可以做加解密

char的算数运算作用有两方面

1. 大小写字母之间的转换
2. 加密和解密

## 3. 类的基础

### 基础

> 通过private封装和隐藏内部实现细节，避免被误操作，是计算机程序的一种基本思维方式。
>
> p = new Point()；创建了一个实例或对象，然后赋值给了Point类型的变量p，它至少做了两件事：1）分配内存，以存储新对象的数据，对象数据包括这个对象的属性，具体包括其实例变量x和y。2）给实例变量设置默认值，int类型默认值为0。
>
> ❑ Point p = new Point()；是定义数据并设置默认值。
>
> ❑ p.x = 2; p.y = 3；是赋值。
>
> ❑ p.distance()是数据的操作。
>
> 可以看出，对实例变量和实例方法的访问都通过对象进行，通过对象来访问和操作其内部的数据是一种基本的面向对象思维。<font color='red'>本例中，我们通过对象直接操作了其内部数据x和y，这是一个不好的习惯，一般而言，不应该将实例变量声明为public，而只应该通过对象的方法对实例变量进行操作。这也是为了减少误操作，直接访问变量没有办法进行参数检查和控制，而通过方法修改，可以在方法中进行检查(即可以进行一些关联性的校验如非空校验~等等)。</font>

针对红字部分的描述，我今后在创建类时应默认将成员变量设置成private，而后如果需要获取或者操作这个变量值仅通过其对应的成员方法来操作。

在new一个对象的时候，至少会做两件事情1. 给对象分配内存，以存储对象的数据 2. 给实例变量设置默认值，<font color ='red'>在后续的学习中关注一下类中各个成员的初始化顺序。</font>

#### 类和对象的生命周期

> 当通过new创建一个对象的时候，对象产生，在内存中，会存储这个对象的实例变量值，每做new操作一次，就会产生一个对象，就会有一份独立的实例变量。
>
> 每个对象除了保存实例变量的值外，可以理解为还保存着对应类型即类的地址，这样，通过对象能知道它的类，访问到类的变量和方法代码。

讲解的基础的东西

### 类的组合

> 程序是用来解决现实问题的，将现实中的概念映射为程序中的概念，是初学编程过程中的一步跨越。本节通过一些例子来演示如何将一些现实概念和问题通过类以及类的组合来表示和处理，涉及的概念包括图形处理、电商、人之间的血缘关系以及计算机中的文件和目录。

<font color ='red'>在我现阶段的编程中我是否思考过上述观点，我是否可以通过类中的成员变量、类与类之间的关系反推到现实中的业务关系。</font>在javaAPI的类中需要关注的可能就是成员方法，他们并不存在业务属性。

### 类路径

<img src="assets/image-20210815164624454.png" alt="image-20210815164624454" style="zoom:50%;" />



### 程序的编译与连接（运行）

> 从Java源代码到运行的程序，有编译和链接两个步骤。编译是将源代码文件变成扩展名是．class的一种字节码，这个工作一般是由javac命令完成的。链接是在运行时动态执行的，.class文件不能直接运行，运行的是Java虚拟机，虚拟机听起来比较抽象，执行的就是Java命令，这个命令解析．class文件，转换为机器能识别的二进制代码，然后运行。所谓链接就是根据引用到的类加载相应的字节码并执行。

### 模块化的概念

> 在Java 9中，清晰地引入了模块的概念，JDK和JRE都按模块化进行了重构，传统的组织机制依然是支持的，但新的应用可以使用模块。一个应用可由多个模块组成，一个模块可由多个包组成。模块之间可以有一定的依赖关系，一个模块可以导出包给其他模块用，可以提供服务给其他模块用，也可以使用其他模块提供的包，调用其他模块提供的服务。对于复杂的应用，模块化有很多好处，比如更强的封装、更为可靠的配置、更为松散的耦合、更动态灵活等。模块是一个很大的主题，限于篇幅，我们就不详细介绍了。

## 4. 类的继承

### 基础

子类对象不能直接访问父类的私有属性和方法，当然父类对象在类外边也无法访问其私有属性和方法。

重写只针对成员方法，且在调用时存在动态绑定 -> 运行多态；

父类的方法必须是非private才可以被子类重写；

父类引用指向子类对象，调用重写方法是子类中重写的；

> 【注】：继承有什么缺点？



在父类构造函数中调用重载方法，最终输出与结果与预期不符分析，代码如下：

```java
class Base{
    public Base(){
        test();
    }

    public void test(){
        System.out.println("base");
    }
}

class Child extends Base{
    public int a = 1;
    @Override
    public void test(){
        System.out.println("Child");
        System.out.println(a);
        System.out.println("----------");

    }

    public static void main(String[] args) {
        Child child = new Child();
        /*
        在创建子类对象时 调用父类的无参构造方法，
        由于父类的无参构造方法回调用test()方法而test()又被子类重写，
        故此处会调用子类的test()方法，但由于在调用父类构造方法时子类的成员变量赋值语句还没执行，故打印结果是0；
        
        但在实际写代码时不应该在父类的构造函数中调用public的方法，这样很容易造成歧义，降低代码的可读性。
        Child
        0
        Child
        1
         */
        child.test();
    }
}
```

#### 重名与静态绑定

> 静态绑定:静态绑定在程序编译阶段即可决定。通过类型就可判断调用的是子类还是父类的成员变量，静态变量，静态方法；
>
> 动态绑定：态绑定则要等到程序运行时。

当子类和父类中同时存在同名的成员变量，静态变量，静态方法时，最终访问这些内容的变量类型是什么（父类、子类）最终就会调用对应类型的成员变量，静态变量，静态方法；

#### 重载和重写

> 重载是指方法名称相同但参数签名不同（参数个数、类型或顺序不同）
>
> 重写是指子类重写与父类相同参数签名的方法
>
> 当有多个重名函数的时候，在决定要调用哪个函数的过程中，首先是按照参数类型进行匹配的，换句话说，寻找在所有重载版本中最匹配的，然后才看变量的动态类型，进行动态绑定。

重载中类型匹配遵从自动向上转型原则，即"大"可以兼容"小"

* 基本类型：表示范围大的兼容小的
* 引用类型：父类兼容子类

#### 继承访问权限protected

```java
class Base{

    protected int currentStep;
    protected void step1(){}
    protected void step2(){}

    public void action(){
        this.currentStep = 1;
        step1();
        this.currentStep = 2;
        step2();

    }

}

class Child extends Base{
    @Override
    protected void step1(){
        System.out.println("child step " + this.currentStep);
    }
    
    @Override
    protected void step2(){
        System.out.println("child step " + this.currentStep);

    }

    public static void main(String[] args) {
        Child child = new Child();
        child.action();
    }


}
```

> 基类定义了表示对外行为的方法action，并定义了可以被子类重写的两个步骤step1()和step2()，以及被子类查看的变量currentStep，子类通过重写protected方法step1()和step2()来修改对外的行为。
>
> 这种思路和设计是一种设计模式，称之为模板方法。action方法就是一个模板方法，它定义了实现的模板，而具体实现则由子类提供。模板方法在很多框架中有广泛的应用，这是使用protected的一种常见场景。

#### 重写-可见性

即访问权限及抛出异常的范围子类也要比父类大；

> 重写方法时，一般并不会修改方法的可见性。但我们还是要说明一点，重写时，子类方法不能降低父类方法的可见性。不能降低是指，父类如果是public，则子类也必须是public，父类如果是protected，子类可以是protected，也可以是public，即子类可以升级父类方法的可见性但不能降低;
>
> 为什么要这样规定呢？继承反映的是“is-a”的关系，即子类对象也属于父类，子类必须支持父类所有对外的行为，将可见性降低就会减少子类对外的行为，从而破坏“is-a”的关系，但子类可以增加父类的行为，所以提升可见性是没有问题的。

#### 防止继承-final

> 继承是把双刃剑，带来的影响就是，有的时候我们不希望父类方法被子类重写，有的时候甚至不希望类被继承，可以通过final关键字实现

---

### 继承实现的基本原理

#### 类加载过程

静态代码块，实例代码块，构造方法，父类静态代码块，父类实例代码块，父类构造方法调用顺序

```java
class Base {

    public static int s;
    private int a;

    static {
        System.out.println("基类静态代码块，s: " + s);
        s = 1;
    }

    {
        System.out.println("基类实例代码块，a: " + a);
        a = 1;
    }

    public Base(){
        System.out.println("基类构造方法，a: " + a);
        a = 2;
    }

    public void step(){
        System.out.println("base s: " + s + " a :" + a );
    }

    public void action(){
        System.out.println("action method start");
        step();
        System.out.println("action method end");
    }

}

class Child extends Base {
    public static int s;
    private int a;

    static {
        System.out.println("子类静态代码块，s: " + s);
        s = 10;
    }

    {
        System.out.println("子类实例代码块，a: " + a);
        a = 10;
    }

    public Child(){
        System.out.println("子类构造方法，a: " + a);
        a = 20;
    }

    public void step(){
        System.out.println("Child s: " + s + " a :" + a );
    }

    public static void main(String[] args) {
        System.out.println("-- new child()");
        Child child = new Child();
        System.out.println("\n --- child.action()");
        child.action();
        Base b = child;
        System.out.println("---b.action()");
        b.action();
        System.out.println("b.s: " + b.s);
        System.out.println("child.s: " + child.s);

        /*
        将类加载到内存中
        基类静态代码块，s: 0
        子类静态代码块，s: 0
        -- new child()
        基类实例代码块，a: 0
        基类构造方法，a: 1
        子类实例代码块，a: 0
        子类构造方法，a: 10
        --- child.action()
        action method start
        Child s: 10 a : 20
        action method end
        --- b.action()
        action method start
        Child s: 10 a : 20
        action method end
        b.s : 1
        child.s : 10

         */

    }


}
```



> 在Java中，所谓类的加载是指将类的相关信息加载到内存。在Java中，类是动态加载的，当第一次使用这个类的时候才会加载，加载一个类时，会查看其父类是否已加载，如果没有，则会加载其父类。
>
> 1）一个类的信息主要包括以下部分：
>
> * 类变量（静态变量）；
> * 类初始化代码；
>     * 定义静态变量时的赋值语句；
>     * 静态初始化代码块。
> * 类方法（静态方法）；
> * 实例变量；
> * 实例初始化代码；
>     * 定义实例变量时的赋值语句；
>     * 实例初始化代码块；
>     * 构造方法。
> * 实例方法；
> * 父类信息引用。
>
> 2）类加载过程包括：
>
> * 分配内存保存类的信息；
> * 给类变量赋默认值；
> * 加载父类；
> * 设置父子关系；
> * 执行类初始化代码。
>
> 注意，类初始化代码，是先执行父类的，再执行子类的。不过，父类执行时，子类静态变量的值也是有的，是默认值。对于默认值，我们之前说过，数字型变量都是0, boolean是false, char是'\u0000'，引用型变量是null。

对上述引用中

1. char是'\u0000'是一个类似空格的字符；它的unicode编码是'\u0000'
2. <font color ='red'>什么时候给类变量和成员变量赋初值的呢？</font>

3. 存放类的信息，这个区在java中称为方法区。在类加载后，java方法区就有了一份这个类的信息；下图为类信息内存布局，对应类加载过程中的分配内存保存类的信息；给类变量赋默认值；加载父类；设置父子关系；`之后会执行类初始化代码`。
4. <font color ='red'>要注意 类加载过程是上述引用中的2），执行类初始化代码是类加载过程的"最后步骤"</font>

<img src="assets/image-20210816215154431.png" alt="image-20210816215154431" style="zoom:80%;" />

#### 对象创建的过程

以上个代码创建对象为例

> 在类加载之后，new Child()就是创建Child对象，创建对象过程包括：
>
> 1. 分配内存；
> 2. 对所有实例变量赋默认值；
> 3. 执行实例初始化代码。
>     * 定义实例变量时的赋值语句；
>     * 实例初始化代码块；
>     * 构造方法;
>
> 分配的内存包括本类和所有父类的实例变量，但不包括任何静态变量。实例初始化代码的执行从父类开始，再执行子类的。但在任何类执行初始化代码之前，所有实例变量都已设置完默认值。每个对象除了保存类的实例变量之外，还保存着实际类信息的引用。

我转述一下对上述引用的理解：在类加载进内存后，即类实例初始化完成后，创建子类的对象new Child()，首先会判断其有没有父类，若存在父类则先给父类分配内容，然后给子类分配内存，然后对父类、子类的所有实例变量赋默认初值，在之后执行实例初始化代码，即实例变量的赋值语句，实例初始化代码块，构造方法；<font color = 'red'>另外每个对象中保存两部分内容:1. 类的实例变量；2. 实际类信息的引用</font>

#### 方法调用的过程

在涉及继承的方法调用中，当父类引用指向子类的对象 Base b = new Child()；调用重写方法时b.action(),b.step();是从<font color = 'red'>对象的实际类型信息(在对象中保存着该信息)</font>开始查找的,若找不到该方法就回去父类中去找；

动态绑定实现的机制就是根据对象的实际类型查找要执行的方法，子类型中找不到的时候再查找父类。

> 如果继承的层次比较深，要调用的方法位于比较上层的父类，则调用的效率是比较低的，因为每次调用都要进行很多次查找。大多数系统使用一种称为虚方法表的方法来优化调用的效率。
>
> 所谓虚方法表，就是在类加载的时候为每个类创建一个表，记录该类的对象所有动态绑定的方法（包括父类的方法）及其地址，但一个方法只有一条记录，子类重写了父类方法后只会保留子类的。

虚方法表：每个方法在表中对应着方法调用的地址，对"每个方法"需要特别强调，它指的是子类能够调用的所有方法（包括继承自父类的）和父类的所有方法；

#### 变量访问的过程

对象访问变量，不论是对类变量，还是实例变量，均是静态绑定，在编译期就已经决定了；通过类型就可判断调用的是子类还是父类的成员变量，静态变量，静态方法；

---

### 为什么说继承是把双刃剑

> 继承为什么会有破坏力呢？主要是因为继承可能破坏封装，而封装可以说是程序设计的第一原则；另外，继承可能没有反映出is-a关系

继承缺点在于：

1. 继承可能会破坏封装性 

    ​	封装即隐藏实现细节，提供简化接口，使用者不必关系内部的实现，实现的细节可以随时修改，不影响使用；在设计代码时函数、类都用到了封装的思想；

    ​	继承可能会导致子类在继承父类时不得不考虑实现细节，父类在修改内部实现时可能需要考虑子类的功能；从而使程序的构建和维护难度上升；破坏了封装的思想。

2. 继承并没有体现is - a的关系，违背继承的设计初衷?

    > ​	继承关系是设计用来反映is-a关系的，子类是父类的一种，子类对象也属于父类，父类的属性和行为也适用于子类。就像橙子是水果一样，水果有的属性和行为，橙子也必然都有。但现实中，设计完全符合is-a关系的继承关系是困难的。比如，绝大部分鸟都会飞，可能就想给鸟类增加一个方法fly()表示飞，但有一些鸟就不会飞，比如企鹅。在is-a关系中，重写方法时，子类不应该改变父类预期的行为，但是这是没有办法约束的。
    >
    > ​	还是以鸟为例，你可能给父类增加了fly()方法，对企鹅，你可能想，企鹅不会飞，但可以走和游泳，就在企鹅的fly()方法中，实现了有关走或游泳的逻辑。
    >
    > ​	继承是应该被当作is-a关系使用的，但是，Java并没有办法约束，父类有的属性和行为，子类并不一定都适用，子类还可以重写方法，实现与父类预期完全不一样的行为。但对于通过父类引用操作子类对象的程序而言，它是把对象当作父类对象来看待的，期望对象符合父类中声明的属性和行为。如果不符合，结果是什么呢？混乱。

### 如何应对继承的双面性

> 1）避免使用继承；
>
> ​	有三种方法：❑ 使用final关键字；❑ 优先使用组合而非继承；❑ 使用接口。
>
> 2）正确使用继承。

```java
class Base {

    private static final int MAX_NUM = 1000;
    private int[] arr = new int[MAX_NUM];
    private int count;
    public void add(int number){
        if(count < MAX_NUM){
            arr[count ++] = number;
        }

    }

    public void addAll(int[] numbers){
        for (int number : numbers) {
            if(count >= MAX_NUM){
                break;
            }
            //此处使用子类的add方法，比较意外，super.addAll()调用父类的addAll()然后调用子类的add()方法！
            add(number);
        }

    }
}

class Child extends Base {
    private long sum;

    @Override
    public void add(int number){
        super.add(number);
        sum += number;

    }

    public void addAll(int[] numbers){
        super.addAll(numbers);
        for (int number : numbers) {
            sum += number;
        }

    }

    public long getSum(){
        return sum;
    }

    public static void main(String[] args) {
        Child c = new Child();
        c.addAll(new int[]{1,123,13});
        System.out.println(c.getSum());//274
    }
}
```

上述代码的运行结果与预期不符；<font color ='red'>super.addAll()调用父类的addAll()然后调用子类的add()方法！</font>

* <font color = 'red'>引出一个问题：父类的引用和父类的对象有什么关系</font>

采用组合类的方式修改子类代码，解决上述问题

```java
class Child extends Base {
    private long sum;
    private Base base;

    {
        base = new Base();
    }
    @Override
    public void add(int number){
        base.add(number);
        sum += number;

    }

    public void addAll(int[] numbers){
        base.addAll(numbers);
        for (int number : numbers) {
            sum += number;
        }

    }

    public long getSum(){
        return sum;
    }

    public static void main(String[] args) {
        Child c = new Child();
        c.addAll(new int[]{1,123,13});
        System.out.println(c.getSum());//137
    }
}
```

## 5. 类的扩展

> 本章内容：
>
> 接口
>
> 抽象类
>
> 内部类
>
> 枚举

### 接口的本质

> 有些场景中，我们不关心对象的类型，仅仅注重对象的能力，即这个对象的方法；
>
> 比如要拍照，很多时候，只要能拍出符合需求的照片就行，至于是用手机拍，还是用Pad拍，或者是用单反相机拍，并不重要，即关心的是对象是否有拍出照片的能力，而并不关心对象到底是什么类型，手机、Pad或单反相机都可以。
>
> 又如要计算一组数字，只要能计算出正确结果即可，至于是由人心算，用算盘算，用计算器算，用计算机软件算，并不重要，即关心的是对象是否有计算的能力，而并不关心对象到底是算盘还是计算器。
>
> 再如要将冷水加热，只要能得到热水即可，至于是用电磁炉加热，用燃气灶加热，还是用电热水壶加热，并不重要，即重要的是对象是否有加热水的能力，而并不关心对象到底是什么类型。
>
> 在以上场景中类型不重要，重要的是实现功能，即提供方法；

接口是这样的"类"，不注重类型，重点关注"能力","方法"

#### 接口的介绍

> 接口声明了一组能力，但它自己并没有实现这个能力，它只是一个约定。接口涉及交互两方对象，一方需要实现这个接口，另一方使用这个接口，但双方对象并不直接互相依赖，它们只是通过接口间接交互。

当一个类实现了某个接口，那它便拥有了接口指定的"能力"，当类实现多个接口，那它便拥有了多个"能力"

#### 接口的声明

```java
public interface MyComparable {
    public abstract int compareTo(Object other);
//    int compareTo();
}



class Point implements MyComparable{
    private int x;
    private int y;
    public Point(int x,int y){
        this.x = x;
        this.y = y;
    }
    //点到原点之间的距离
    public double distance(){
        return Math.sqrt(x*x + y*y);
    }

    @Override
    public int compareTo(Object other) {
        //1. 判断other类型是否是Point及其子类
        if(!(other instanceof Point)){
            throw new IllegalArgumentException();
        }
        //2. 计算两个点到原点的距离，并比较大小
        Point otherPoint = (Point)other;
        /*double otherDistance = otherPoint.distance();
        double curDistance = distance();
        if(otherDistance > curDistance){
            return -1;
        }else if(otherDistance == curDistance){
            return 0;
        }*/
        //改写上述注释代码定义一个两个点距离原点之差的变量disVar
        double disVar = otherPoint.distance() - distance();
        if(disVar > 0){
            return -1;
        }else if(disVar == 0){
            return 0;
        }
        return 1;
    }

    public static void main(String[] args) {
        Point point = new Point(3, 4);
        Point otherPoint = new Point(4, 5);
        int rst = point.compareTo(otherPoint);
        System.out.println(rst);
    }

}
```

声明接口时，使用implement关键字，在定义接口中的方法不论加不加修饰符其效果都是等价于加了public abstract;

接口中的变量：pubic static final int  a = 2;当声明为int a时，也相当于加上public static final

接口可以多继承

接口也可以使用instanceof来判断对象是否是接口类型；

#### java8中接口的新特性

> 在没有默认方法之前，Java是很难给接口增加功能的，比如List接口（第9章介绍），因为有太多非Java JDK控制的代码实现了该接口，如果给接口增加一个方法，则那些接口的实现就无法在新版Java上运行，必须改写代码，实现新的方法，这显然是无法接受的。函数式数据处理需要给一些接口增加一些新的方法，所以就有了默认方法的概念，接口增加了新方法，而接口现有的实现类也不需要必须实现
>
> 在Java 8中，静态方法和默认方法都必须是public的，Java 9去除了这个限制，它们都可以是private的，引入private方法主要是为了方便多个静态或默认方法复用代码

1. 允许在接口中定义两类新方法：静态方法public static和默认方法 default，它们有方法体

    比如，Java API中，Collection接口有一个对应的单独的类Collections，在Java 8中，就可以直接写在接口中了，比如Comparator接口就定义了多个静态方法。

---

### 抽象类

#### 抽象类诞生的背景

> 抽象方法和抽象类看上去是多余的，对于抽象方法，不知道如何实现，定义一个空方法体不就行了吗？而抽象类不让创建对象，看上去只是增加了一个不必要的限制。
>
> 引入抽象方法和抽象类，是Java提供的一种语法工具，对于一些类和方法，引导使用者正确使用它们，减少误用。使用抽象方法而非空方法体，子类就知道它必须要实现该方法，而不可能忽略，若忽略Java编译器会提示错误。使用抽象类，类的使用者创建对象的时候，就知道必须要使用某个具体子类，而不可能误用不完整的父类。

抽象类就是java提供的一种使用规范；必须实现抽象类的抽象方法；

---

#### 抽象类的相关语法

抽象类可以没有抽象方法。抽象类和具体类一样，可以定义具体方法、实例变量等，它和具体类的核心区别是，抽象类不能创建对象(比如，不能使用new Shape())，而具体类可以。

---

#### 抽象类和接口

##### 异同点

* 共同点
    1. 都不能用于创建对象

* 不同点

    1. 成员不同：在jdk1.7及之前接口中只包含抽象方法和静态变量，而抽象类中可以不包含抽象方法，可以定义成员变量，甚至可以和普通类相同

    2. 用法不同：一个类可以实现多个接口，但只能继承一个抽象类

---

##### 抽象类和接口之间的关系

此处引用书中的描述

> 抽象类和接口是<font color ='red'>配合而非替代关系</font>，它们经常一起使用，接口声明能力，抽象类提供默认实现，实现全部或部分方法，<font color ='red'>一个接口经常有一个对应的抽象类</font>。比如，在Java类库中，有：
>
> * Collection接口和对应的AbstractCollection抽象类。
> * List接口和对应的AbstractList抽象类
> * Map接口和对应的AbstractMap抽象类。
>
> 对于需要实现接口的具体类而言，有两个选择：一个是实现接口，自己实现全部方法；<font color ='red'>另一个则是继承抽象类，然后根据需要重写方法。</font>
>
> 继承的好处是复用代码，只重写需要的部分即可，需要编写的代码比较少，容易实现。不过，如果这个具体类已经有父类了，那就只能选择实现接口了。

抽象类和接口搭配使用；抽象类实现接口并提供接口全部或部分"能力"的默认实现

<font color ='red'>另：通过代码编译发现，抽象类实现接口可以不实现接口的抽象方法，抽象类继承抽象类也是如此</font>



---

### 内部类的本质

> 一般而言，内部类与包含它的外部类有比较密切的关系，而与其他类关系不大，定义在类内部，可以实现对外部完全隐藏，可以有更好的封装性，代码实现上也往往更为简洁。
>
> 内部类只是Java编译器的概念，对于Java虚拟机而言，它是不知道内部类这回事的，<font color= 'red'>每个内部类最后都会被编译为一个独立的类，生成一个独立的字节码文件</font>

内部类最终都会被编译成一个独立与外部类的类，生成一个独立的字节码文件。

---

#### 内部类的分类

内部类分为4类

1. 静态内部类

2. 成员内部类
3. 方法内部类（局部内部类）
4. 匿名内部类

> 方法内部类是在一个方法内定义和使用的；匿名内部类使用范围更小，<font color= 'red'>它们都不能在外部使用；</font>
>
> 成员内部类和静态内部类可以被外部使用，不过它们都可以被声明为private，这样，外部就不能使用了

方法内部类和匿名内部类都不能供外部类使用；

成员内部类和静态内部类可以供外部类使用，但是其声明为private时，外部类便不能访问内部类了<font color= 'red'>不对啊，经验证当静态内部类和成员内部类声明成private外部类也可以访问其内部；</font>；

【注】：对上句中红字描述，作者可能是要说外部外访问内部类private的内部类无法访问，而不是外部类中访问内部类

---

##### 静态内部类

```java
/*
内部类
    * 静态内部类
 */
public class Test {
    //定义外部类的私有静态变量
    private static int outVar = 100;
    //定义静态内部类
    public static class InnerClass{
        //静态类内部定义方法访问外部类类变量
        public void accessOutVar(){
            System.out.println(outVar);
        }
        public static void innerStaticMethod(){
            System.out.println("innerStaticMethod");
        }
    }
    //外部类定义方法创建内部类对象并调用内部类方法访问外部类类变量
    public void test(){
        //直接创建静态内部类对象
        InnerClass ic = new InnerClass();
        //调用静态内部类中的成员方法
        ic.accessOutVar();
        //通过类名调用静态内部类中的静态方法
        InnerClass.innerStaticMethod();
    }

    //main函数测试
    public static void main(String[] args) {
        //在main方法中直接创建内部类的对象
        InnerClass innerClass = new InnerClass();
        //内部类对象调用其成员方法
        innerClass.accessOutVar();
        System.out.println("-------------------");
        //外部类对象调用外部类方法，外部类方法中调用了内部类的方法
        new Test().test();
        //在外部类中通过类名.内部类静态方法名直接调用
        Test.InnerClass.innerStaticMethod();
    }

}
```

静态内部类不能访问外部类的成员变量，成员方法，只能访问外部类的静态变量和静态方法；

---

静态内部实现

静态内部类访问了外部类的私有静态变量，java的实现是为内部类在外部类中声明一个非私有的静态方法；

<img src="assets/image-20210819232656960.png" alt="image-20210819232656960" style="zoom:50%;" />

<img src="assets/image-20210819232710132.png" alt="image-20210819232710132" style="zoom:50%;" />

---



静态内部类的使用场景

* Integer类内部有一个私有静态内部类IntegerCache，用于支持整数的自动装箱。
* 表示链表的LinkedList类内部有一个私有静态内部类Node，表示链表中的每个节点。
* Character类内部有一个public静态内部类UnicodeBlock，用于表示一个Unicode block。

---

##### 成员内部类

> 与静态内部类不同，除了静态变量和方法，成员内部类还可以直接访问外部类的实例变量和方法;
>
> 在外部类内，使用成员内部类与静态内部类是一样的，直接使用即可
>
> 与静态内部类不同，成员内部类对象总是与一个外部类对象相连的，在外部使用时，它不能直接通过new Outer.Inner()的方式创建对象，而是要先将创建一个Outer类对象
>
> 创建内部类对象的语法是“外部类对象．new 内部类()”，如outer.new Inner()。
>
> <font color = 'red'>与静态内部类不同，成员内部类中不可以定义静态变量和方法（final变量例外，它等同于常量），下面介绍的方法内部类和匿名内部类也都不可以。</font>

---

成员内部类实现

<img src="assets/image-20210819233326539.png" alt="image-20210819233326539" style="zoom:33%;" />

<img src="assets/image-20210819233334939.png" alt="image-20210819233334939" style="zoom:30%;" />

---

成员内部类使用场景

> 在Java API的类LinkedList中，它的两个方法listIterator和descendingIterator的返回值都是接口Iterator，调用者可以通过Iterator接口对链表遍历，listIterator和descend-ingIterator内部分别使用了成员内部类ListItr和DescendingIterator，这两个内部类都实现了接口Iterator。

---

##### 方法内部类

> 类Inner定义在外部类方法test中，方法内部类只能在定义的方法内被使用。如果方法是实例方法，则除了静态变量和方法，内部类还可以直接访问外部类的实例变量和方法，如innerMethod直接访问了外部私有实例变量a。
>
> <font color = 'red'>如果方法是静态方法，则方法内部类只能访问外部类的静态变量和方法。方法内部类还可以直接访问方法的参数和方法中的局部变量，不过，这些变量必须被声明为final</font>
>
> 【注】：jdk1.8后方法的参数不用声明成final类型，而方法的局部变量如果要被方法内部类使用则就需要声明为final；

![image-20210819234622657](assets/image-20210819234622657.png)

---

具体为什么需要声明成final，貌似可以从编译后的源文件看出；

【注】：final的数组地址不能变，但数组的内容可以变；对象也是同样，对象的地址不能变，但对象的成员变量可以改变

##### 匿名内部类

###### 语法

```java
new 父类/接口(参数列表){
  //匿名实现部分
}
```

---

###### 匿名内部类实现回调

>  Arrays.sort中传递的Comparator对象，它的compare方法并不是在写代码的时候被调用的，而是在Arrays. sort的内部某个地方回过头来调用的

这是啥回调？？？

---

### 枚举类的本质

