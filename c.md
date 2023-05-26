# C语言

    #include <stdio.h>
    int main()
    {
    /* 我的第一个 C 程序 */
    printf("Hello, World! \n");
    return 0;
    }
- 所有的 C 语言程序都需要包含 main() 函数。 代码从 main() 函数开始执行。
- /* ... */ 用于注释说明。
- printf() 用于格式化输出到屏幕。printf() 函数在 "stdio.h" 头文件中声明。
- stdio.h 是一个头文件 (标准输入输出头文件) , #include 是一个预处理命令，用来引入头文件。 当编译器遇到 printf() 函数时，如果没有找到 stdio.h 头文件，会发生编译错误。
- return 0; 语句用于表示退出程序。    
<br><br>

## 接下来我们讲解一下上面这段程序：

- 程序的第一行 #include <stdio.h> 是预处理器指令，告诉 C 编译器在实际编译之前要包含 stdio.h 文件。
- 下一行 int main() 是主函数，程序从这里开始执行。
- 下一行 /*...*/ 将会被编译器忽略，这里放置程序的注释内容。它们被称为程序的注释。
- 下一行 printf(...) 是 C 中另一个可用的函数，会在屏幕上显示消息 "Hello, World!"。
- 下一行 return 0; 终止 main() 函数，并返回值 0。
<br><br><br>

# 关于C
- 大多数先进的软件都是使用 C 语言实现的。
- 当今最流行的 Linux 操作系统和 RDBMS（Relational Database Management System：关系数据库管理系统） MySQL 都是使用 C 语言编写的。
<br><br>

## 为什么要使用 C？
C 语言最初是用于系统开发工作，特别是组成操作系统的程序。由于 C 语言所产生的代码运行速度与汇编语言编写的代码运行速度几乎一样，所以采用 C 语言作为系统开发语言。下面列举几个使用 C 的实例：

操作系统 语言编译器 汇编器 文本编辑器 打印机 网络驱动器 现代程序 数据库 语言解释器 实体工具
<br><br>

## C 程序
一个 C 语言程序，可以是 3 行，也可以是数百万行，它可以写在一个或多个扩展名为 ".c" 的文本文件中，例如，hello.c。您可以使用 "vi"、"vim" 或任何其他文本编辑器来编写您的 C 语言程序。
<br><br><br>

# C数据类型
| 类型 | 描述 |
|:--------| :---------| 
| 基本数据类型 | 它们是算术类型，包括整型（int）、字符型（char）、浮点型（float）和双精度浮点型（double）。 |
| 枚举类型 | 它们也是算术类型，被用来定义在程序中只能赋予其一定的离散整数值的变量。 |
| void 类型 | 类型说明符 void 表示没有值的数据类型，通常用于函数返回值。 |
| 派生类型 | 包括数组类型、指针类型和结构体类型。 |
<br>


## C 语言中有两种类型转换：
**隐式类型转换** ：隐式类型转换是在表达式中自动发生的，无需进行任何明确的指令或函数调用。它通常是将一种较小的类型自动转换为较大的类型，例如，将int类型转换为long类型或float类型转换为double类型。隐式类型转换也可能会导致数据精度丢失或数据截断。

**显式类型转换** ：显式类型转换需要使用强制类型转换运算符（type casting operator），它可以将一个数据类型的值强制转换为另一种数据类型的值。强制类型转换可以使程序员在必要时对数据类型进行更精确的控制，但也可能会导致数据丢失或截断。

    double d = 3.14159;
    int i = (int)d; // 显式将double类型转换为int类型

<br><br>

# C变量
## C 中的变量声明
变量声明向编译器保证变量以指定的类型和名称存在，这样编译器在不需要知道变量完整细节的情况下也能继续进一步的编译。变量声明只在编译时有它的意义，在程序连接时编译器需要实际的变量声明。

**变量的声明有两种情况：**
1. 一种是需要建立存储空间的。例如：int a 在声明的时候就已经建立了存储空间。
2. 另一种是不需要建立存储空间的，通过使用extern关键字声明变量名而不定义它。 例如：extern int a 其中变量 a 可以在别的文件中定义的。
3. 除非有extern关键字，否则都是变量的定义。
<br><br>

## 实例

        #include <stdio.h>
        // 函数外定义变量 x 和 y
        int x;
        int y;
        int addtwonum()
        {
            // 函数内声明变量 x 和 y 为外部变量
            extern int x;
            extern int y;
            // 给外部变量（全局变量）x 和 y 赋值
            x = 1;
            y = 2;
            return x+y;
        }
        int main()
        {
            int result;
            // 调用函数 addtwonum
            result = addtwonum();
            printf("result 为: %d",result);
            return 0;
        }

### 结果：result为：3        
<br>

**如果需要在一个源文件中引用另外一个源文件中定义的变量，我们只需在引用的文件中将变量加上 extern 关键字的声明即可。**

addtwonum.c 文件代码：

    #include <stdio.h>
    /*外部变量声明*/
    extern int x ;
    extern int y ;
    int addtwonum()
    {
        return x+y;
    }

test.c 文件代码：

    #include <stdio.h>
    /*定义两个全局变量*/
    int x=1;
    int y=2;
    int addtwonum();
    int main(void)
    {
        int result;
        result = addtwonum();
        printf("result 为: %d\n",result);
        return 0;
    }

### 当上面的代码被编译和执行时，它会产生下列结果：    

    $ gcc addtwonum.c test.c -o main
    $ ./main
    result 为: 3
<br><br>

## C 中的左值（Lvalues）和右值（Rvalues）
### C 中有两种类型的表达式：
1. 左值（lvalue）：指向内存位置的表达式被称为左值（lvalue）表达式。左值可以出现在赋值号的左边或右边。
2. 右值（rvalue）：术语右值（rvalue）指的是存储在内存中某些地址的数值。右值是不能对其进行赋值的表达式，也就是说，右值可以出现在赋值号的右边，但不能出现在赋值号的左边。
<br><br><br>

# C常量
## 整数常量
### 整数常量可以是十进制、八进制或十六进制的常量。前缀指定基数：0x 或 0X 表示十六进制，0 表示八进制，不带前缀则默认表示十进制。

### 整数常量也可以带一个后缀，后缀是 U 和 L 的组合，U 表示无符号整数（unsigned），L 表示长整数（long）。后缀可以是大写，也可以是小写，U 和 L 的顺序任意。

**下面列举几个整数常量的实例：**
|  |  |
|:--------| :---------| 
|212 |        /* 合法的 */
|215u|        /* 合法的 */
|0xFeeL|      /* 合法的 */
|078|         /* 非法的：8 不是八进制的数字 */
|032UU|       /* 非法的：不能重复后缀 */

**整数常量可以带有一个后缀表示数据类型，例如：**

    int myInt = 10;
    long myLong = 100000L;
    unsigned int myUnsignedInt = 10U;
<br><br>

## 定义常量
### 在 C 中，有两种简单的定义常量的方式：
1. 使用 #define 预处理器。
2. 使用 const 关键字。    

### define 预处理器

        #include <stdio.h>
        #define LENGTH 10   
        #define WIDTH  5
        #define NEWLINE '\n'
        int main()
        {
            int area;  
            area = LENGTH * WIDTH;
            printf("value of area : %d", area);
            printf("%c", NEWLINE);
            return 0;
        }    

### const 关键字

    #include <stdio.h>
    int main()
    {
        const int  LENGTH = 10;
        const int  WIDTH  = 5;
        const char NEWLINE = '\n';
        int area;  
        area = LENGTH * WIDTH;
        printf("value of area : %d", area);
        printf("%c", NEWLINE);
        return 0;
    }
运行结果：value of area : 50    
*注意，把常量定义为大写字母形式，是一个很好的编程习惯。*
<br><br><BR>

# C存储类
- 存储类定义 C 程序中变量/函数的的存储位置、生命周期和作用域。
- 这些说明符放置在它们所修饰的类型之前。
- 下面列出 C 程序中可用的存储类：auto register static extern
<BR><BR>

## auto 存储类
### auto 存储类是所有局部变量默认的存储类。定义在函数中的变量默认为 auto 存储类，这意味着它们在函数开始时被创建，在函数结束时被销毁。
<BR>

### auto是C语言的一个关键字，关键字主要用于声明变量的生存期为自动，即将不在任何类、结构、枚举、联合和函数中定义的变量视为全局变量，而在函数中定义的变量视为局部变量。这个关键字不怎么多写，因为所有的变量默认就是auto的。

    {
    int mount;
    auto int month;
    }
上面的实例定义了两个带有相同存储类的变量，auto 只能用在函数内，即 auto 只能修饰局部变量。
<BR><BR>

## register 存储类
register 存储类用于定义存储在寄存器中而不是 RAM 中的局部变量。这意味着变量的最大尺寸等于寄存器的大小（通常是一个字），且不能对它应用一元的 '&' 运算符（因为它没有内存位置）。

register 存储类定义存储在寄存器，所以变量的访问速度更快，但是它不能直接取地址，因为它不是存储在 RAM 中的。在需要频繁访问的变量上使用 register 存储类可以提高程序的运行速度。

    {
    register int  miles;    
    }

*寄存器只用于需要快速访问的变量，比如计数器。还应注意的是，定义 'register' 并不意味着变量将被存储在寄存器中，它意味着变量可能存储在寄存器中，这取决于硬件和实现的限制。*
<BR><BR>

## static 存储类
static 存储类指示编译器在程序的生命周期内保持局部变量的存在，而不需要在每次它进入和离开作用域时进行创建和销毁。因此，使用 static 修饰局部变量可以在函数调用之间保持局部变量的值。

static 修饰符也可以应用于全局变量。当 static 修饰全局变量时，会使变量的作用域限制在声明它的文件内。

全局声明的一个 static 变量或方法可以被任何函数或方法调用，只要这些方法出现在跟 static 变量或方法同一个文件中。

静态变量在程序中只被初始化一次，即使函数被调用多次，该变量的值也不会重置。

以下实例演示了 static 修饰全局变量和局部变量的应用：

    #include <stdio.h>
    /* 函数声明 */
    void func1(void);
    static int count=10;        /* 全局变量 - static 是默认的 */
    int main()
    {
        while (count--) {
            func1();
        }
        return 0;
    }
    void func1(void)
    {
    /* 'thingy' 是 'func1' 的局部变量 - 只初始化一次
    * 每次调用函数 'func1' 'thingy' 值不会被重置。
    */                
        static int thingy=5;
        thingy++;
        printf(" thingy 为 %d ， count 为 %d\n", thingy, count);
    }

## ？？？？
*实例中 count 作为全局变量可以在函数内使用，thingy 使用 static 修饰后，不会在每次调用时重置。*    
<BR><BR>

## extern 存储类
extern 存储类用于定义在其他文件中声明的全局变量或函数。当使用 extern 关键字时，不会为变量分配任何存储空间，而只是指示编译器该变量在其他文件中定义。

extern 存储类用于提供一个全局变量的引用，全局变量对所有的程序文件都是可见的。当您使用 extern 时，对于无法初始化的变量，会把变量名指向一个之前定义过的存储位置。

当您有多个文件且定义了一个可以在其他文件中使用的全局变量或函数时，可以在其他文件中使用 extern 来得到已定义的变量或函数的引用。可以这么理解，extern 是用来在另一个文件中声明一个全局变量或函数。

extern 修饰符通常用于当有两个或多个文件共享相同的全局变量或函数的时候，如下所示：

第一个文件：main.c

    #include <stdio.h>
    int count ;
    extern void write_extern();
    int main()
    {
       count = 5;
       write_extern();
    }
第二个文件：support.c

    #include <stdio.h>
    extern int count;
    void write_extern(void)
    {
       printf("count is %d\n", count);
    }

在这里，第二个文件中的 extern 关键字用于声明已经在第一个文件 main.c 中定义的 count。现在 ，编译这两个文件：

        $ gcc main.c support.c
这会产生 a.out 可执行程序，当程序被执行时，它会产生下列结果：count is 5

<br><br>

# C运算符
## 杂项运算符↦ sizeof & 三元

| 运算符 | 描述 | 实例 |
|:--------| :---------:| :---------:|
| sizeof() | 返回变量的大小。 | sizeof(a) 将返回 4，其中 a 是整数。 |
| & | 返回变量的地址。 | &a; 将给出变量的实际地址。|	
| * | 指向一个变量。|*a; 将指向一个变量。 |	
| ? : | 条件表达式 | 如果条件为真 ? 则值为 X : 否则值为 Y |
