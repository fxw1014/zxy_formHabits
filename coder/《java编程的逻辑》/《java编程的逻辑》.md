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
> 在平常计算中我们如何处理这种不精确的情况呢？
>
> 1. 不需要精确，只需要保留小数点多少位即可；使用四舍五入或者舍掉小数点即可满足要求
> 2. <font color = 'red'>需要精确，如何处理呢？为什么这么处理就精确了呢？</font>
>     * 转换为整数？
>     * 使用java类BigDecimal?

#### 浮点数

> 待总结：todo

### 字符的编码与乱码

#### 字符的编码

#### 字符的乱码

#### char类型













