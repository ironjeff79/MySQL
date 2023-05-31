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
    
### 实例

    #include <stdio.h>
    int main()
    {
        int a = 4;
        short b;
        double c;
        int* ptr;
 
        /* sizeof 运算符实例 */
        printf("Line 1 - 变量 a 的大小 = %lu\n", sizeof(a) );
        printf("Line 2 - 变量 b 的大小 = %lu\n", sizeof(b) );
        printf("Line 3 - 变量 c 的大小 = %lu\n", sizeof(c) );
 
        /* & 和 * 运算符实例 */
        ptr = &a;    /* 'ptr' 现在包含 'a' 的地址 */
        printf("a 的值是 %d\n", a);
        printf("*ptr 是 %d\n", *ptr);}		
		
<BR><BR>

# C循环
## for嵌套实例

    #include <stdio.h>
    int main ()
    {
        /* 局部变量定义 */
        int i, j;
        for(i=2; i<100; i++) {
            for(j=2; j <= (i/j); j++)
                if(!(i%j)) break; // 如果找到，则不是质数 (这里有点奇怪)
            if(j > (i/j)) printf("%d 是质数\n", i);
        }
        return 0;
    }
		
<BR><BR>

# C函数
### C 标准库提供了大量的程序可以调用的内置函数。例如，函数 strcat() 用来连接两个字符串，函数 memcpy() 用来复制内存到另一个位置。
<BR>

## 定义函数

    return_type function_name( parameter list )
    {
        body of the function
    }

### 在 C 语言中，函数由一个函数头和一个函数主体组成。下面列出一个函数的所有组成部分：
<br>

**返回类型：** 一个函数可以返回一个值。return_type 是函数返回的值的数据类型。有些函数执行所需的操作而不返回值，在这种情况下，return_type 是关键字 void。  
<Br> 

**函数名称：** 这是函数的实际名称。函数名和参数列表一起构成了函数签名。
<BR>

**参数：** 参数就像是占位符。当函数被调用时，您向参数传递一个值，这个值被称为实际参数。参数列表包括函数参数的类型、顺序、数量。参数是可选的，也就是说，函数可能不包含参数。
<Br>

**函数主体：** 函数主体包含一组定义函数执行任务的语句。

### 实例

    /* 函数返回两个数中较大的那个数 */
    int max(int num1, int num2) 
    {
        /* 局部变量声明 */
        int result; 
        if (num1 > num2) {
            result = num1;
        } else {
            result = num2;
        }
        return result; 
    }

<br><br>

## 函数参数
如果函数要使用参数，则必须声明接受参数值的变量。这些变量称为函数的**形式参数**。  
形式参数就像函数内的其他局部变量，在进入函数时被创建，退出函数时被销毁。  
当调用函数时，有两种向函数传递参数的方式：
| 调用类型 | 描述 | 
|:--------| :---------:| 
| 传值调用 | 该方法把参数的实际值复制给函数的形式参数。在这种情况下，修改函数内的形式参数不会影响实际参数。|
| 引用调用 | 通过指针传递方式，形参为指向实参地址的指针，当对形参的指向操作时，就相当于对实参本身进行的操作。|
<BR><BR>


# C作用域规则
## 任何一种编程中，作用域是程序中定义的变量所存在的区域，超过该区域变量就不能被访问。C 语言中有三个地方可以声明变量：

- 在函数或块内部的局部变量
- 在所有函数外部的全局变量
- 在形式参数的函数参数定义中
<br><br>

## 全局变量
在程序中，局部变量和全局变量的名称可以相同，但是在函数内，如果两个名字相同，会使用局部变量值，全局变量不会被使用。下面是一个实例

    #include <stdio.h>
    /* 全局变量声明 */
    int g = 20;
    int main ()
    {
        /* 局部变量声明 */
        int g = 10; 
        printf ("value of g = %d\n",  g);
        return 0;   
    }
上面代码的执行结果是&emsp;&emsp;value of g = 10    

*全局变量与局部变量在内存中的区别：  
全局变量保存在内存的全局存储区中，占用静态的存储单元；  
局部变量保存在栈中，只有在所在函数被调用时才动态地为变量分配存储单元。*
<BR><BR>


# C数组
## 声明
        type arrayName [ arraySize ];

## 实例 声明数组，数组赋值，访问数组
    #include <stdio.h>
 
    int main ()
    {
        int n[ 10 ]; /* n 是一个包含 10 个整数的数组 */
        int i,j;
       /* 初始化数组元素 */         
        for ( i = 0; i < 10; i++ )
        {
            n[ i ] = i * 3; /* 设置元素 i 为 i * 3 */
        }
       /* 输出数组中每个元素的值 */
        for (j = 0; j < 10; j++ )
        {
            printf("Element[%d] = %d\n", j, n[j] );
        }
       return 0;
    }        
<BR><BR>


# C enum（枚举）    
## 枚举变量的定义
### 我们可以通过以下三种方式来定义枚举变量
<br>

1.先定义枚举类型，再定义枚举变量

    enum DAY
    {
          MON=1, TUE, WED, THU, FRI, SAT, SUN
    };
    enum DAY day;
    
2.定义枚举类型的同时定义枚举变量    

    enum DAY
    {
         MON=1, TUE, WED, THU, FRI, SAT, SUN
    } day;

3.省略枚举名称，直接定义枚举变量

    enum
    {
        MON=1, TUE, WED, THU, FRI, SAT, SUN
    } day;

## 实例

    #include <stdio.h>
 
    enum DAY
    {
        MON=1, TUE, WED, THU, FRI, SAT, SUN
    };
 
    int main()
    {
        enum DAY day;
        day = WED;
        printf("%d",day);
        return 0;   
    }
<BR><BR>    

	# C 指针
## 什么是指针？
### 指针也就是内存地址，指针变量是用来存放内存地址的变量。就像其他变量或常量一样，您必须在使用指针存储其他变量地址之前，对其进行声明。指针变量声明的一般形式为：
    type *var_name;

## 如何使用指针？
### 使用指针时会频繁进行以下几个操作：定义一个指针变量、把变量地址赋值给指针、访问指针变量中可用地址的值。这些是通过使用一元运算符 * 来返回位于操作数所指定地址的变量的值。下面的实例涉及到了这些操作： 
<br>

## 实例 

    #include <stdio.h>
    int main ()
    {
        int  var = 20;   /* 实际变量的声明 */
        int  *ip;        /* 指针变量的声明 */
        ip = &var;  /* 在指针变量中存储 var 的地址 */
        printf("var 变量的地址: %p\n", &var  );
 
        /* 在指针变量中存储的地址 */
        printf("ip 变量存储的地址: %p\n", ip );
 
        /* 使用指针访问值 */
        printf("*ip 变量的值: %d\n", *ip );
        return 0;
    }
### 执行结果
var 变量的地址: 0x7ffeeef168d8  
ip 变量存储的地址: 0x7ffeeef168d8  
*ip 变量的值: 20  
<BR><BR>

## C 中的 NULL 指针
### 在变量声明的时候，如果没有确切的地址可以赋值，为指针变量赋一个 NULL 值是一个良好的编程习惯。赋为 NULL 值的指针被称为空指针。  
### NULL 指针是一个定义在标准库中的值为零的常量。请看下面的程序：

实例

    #include <stdio.h>
 
    int main ()
    {
        int  *ptr = NULL;
        printf("ptr 的地址是 %p\n", ptr  );
        return 0;
    }

### 在大多数的操作系统上，程序不允许访问地址为 0 的内存，因为该内存是操作系统保留的。然而，内存地址 0 有特别重要的意义，它表明该指针不指向一个可访问的内存位置。但按照惯例，如果指针包含空值（零值），则假定它不指向任何东西。
### 如需检查一个空指针，您可以使用 if 语句，如下所示：
    if(ptr)     /* 如果 p 非空，则完成 */
    if(!ptr)    /* 如果 p 为空，则完成 */
<br><BR>

## 递增一个指针
### 我们喜欢在程序中使用指针代替数组，因为变量指针可以递增，而数组不能递增，数组可以看成一个指针常量。下面的程序递增变量指针，以便顺序访问数组中的每一个元素：

    #include <stdio.h>
    const int MAX = 3;
    int main ()
    {
        int  var[] = {10, 100, 200};
        int  i, *ptr;
        /* 指针中的数组地址 */
        ptr = var;
        for ( i = 0; i < MAX; i++)
    {    
           printf("存储地址：var[%d] = %p\n", i, ptr );
           printf("存储值：var[%d] = %d\n", i, *ptr );
           /* 指向下一个位置 */
           ptr++;
        }
        return 0;
    }
### 执行结果  
存储地址：var[0] = 0x7ffd62b0f174  
存储值：var[0] = 10  
存储地址：var[1] = 0x7ffd62b0f178  
存储值：var[1] = 100  
存储地址：var[2] = 0x7ffd62b0f17c  
存储值：var[2] = 200    
<BR><BR>

## 指针的比较
### 指针可以用关系运算符进行比较，如 ==、< 和 >。如果 p1 和 p2 指向两个相关的变量，比如同一个数组中的不同元素，则可对 p1 和 p2 进行大小比较。
### 下面的程序修改了上面的实例，只要变量指针所指向的地址小于或等于数组的最后一个元素的地址 &var[MAX - 1]，则把变量指针进行递增：

    #include <stdio.h>
    const int MAX = 3;
    int main ()
    {
        int  var[] = {10, 100, 200};
        int  i, *ptr;
       /* 指针中第一个元素的地址 */
        ptr = var;
        i = 0;
        while ( ptr <= &var[MAX - 1] )
        {
           printf("存储地址：var[%d] = %p\n", i, ptr );
           printf("存储值：var[%d] = %d\n", i, *ptr );
           /* 指向上一个位置 */
           ptr++;
           i++;
         }
        return 0;
    }

## 传递指针给函数

    #include <stdio.h>
    #include <time.h>
    void getSeconds(unsigned long *par);
    int main ()
    {
        unsigned long sec;
        getSeconds( &sec );
       /* 输出实际值 */
        printf("Number of seconds: %ld\n", sec );
        return 0;
    }
    void getSeconds(unsigned long *par)
    {
       /* 获取当前的秒数 */
        *par = time( NULL );
       return;
    }  
## 运行结果 Number of seconds: 1685350228          

<BR><BR>

# C语言随机函数：rand（）和srand()
## 一、rand()函数
### 1、rand()函数原理
rand()函数用于产生一个随机数，其内部实现是用线性同余法实现的，是伪随机数，由于周期较长，因此在一定范围内可以看成是随机的。调用rand()函数会得到一个在0-RAND_MAX。
**RAND_MAX在头文件stdlib.h中定义。**
### 2、调用方法
想要使用rand()函数产生一个（a，b）区间的数num，可以使用以下两种方式：
1. num=a+(b-a+1)*rand()/(RAND-MAX+1.0)；
2. a+rand%(b-a+1)；  

注意公式（1）用的是“/”，而公式（2）是“%”。
下面使用两种写一个简单函数：例如要随机产生1-10之间的数。
<BR><BR><BR>

# C 函数指针与回调函数
## 函数指针
函数指针是指向函数的指针变量。
通常我们说的指针变量是指向一个整型、字符型或数组等变量，而函数指针是指向函数。
函数指针可以像一般函数一样，用于调用函数、传递参数。
函数指针变量的声明：
    
    typedef int (*fun_ptr)(int,int); // 声明一个指向同样参数、返回值的函数指针类型

## 实例

    #include <stdio.h>  
    int max(int x, int y)
    {
        return x > y ? x : y;
    }
    int main(void)
    {
        /* p 是函数指针 */
        int (* p)(int, int) = & max; // &可以省略
        int a, b, c, d;

        printf("请输入三个数字:");
        scanf("%d %d %d", & a, & b, & c);
        
        /* 与直接调用函数等价，d = max(max(a, b), c) */
        d = p(p(a, b), c); 
        printf("最大的数字是: %d\n", d);
        return 0;
    }
### 运行结果
请输入三个数字:1 2 3  
最大的数字是: 3
<BR><BR>

## 回调函数
### 函数指针作为某个函数的参数

函数指针变量可以作为某个函数的参数来使用的，回调函数就是一个通过函数指针调用的函数。
简单讲：回调函数是由别人的函数执行时调用你实现的函数。  

*你到一个商店买东西，刚好你要的东西没有货，于是你在店员那里留下了你的电话，过了几天店里有货了，店员就打了你的电话，然后你接到电话后就到店里去取了货。在这个例子里，你的电话号码就叫回调函数，你把电话留给店员就叫登记回调函数，店里后来有货了叫做触发了回调关联的事件，店员给你打电话叫做调用回调函数，你到店里去取货叫做响应回调事件。*

### 实例
实例中 populate_array() 函数定义了三个参数，其中第三个参数是函数的指针，通过该函数来设置数组的值。  
实例中我们定义了回调函数 getNextRandomValue()，它返回一个随机值，它作为一个函数指针传递给 populate_array() 函数。
populate_array() 将调用 10 次回调函数，并将回调函数的返回值赋值给数组。

    #include <stdlib.h>  
    #include <stdio.h>

    void populate_array(int *array, size_t arraySize, int (*getNextValue)(void))
    {
        for (size_t i=0; i<arraySize; i++)
            array[i] = getNextValue();
    }
 
    // 获取随机值
    int getNextRandomValue(void)
    {
        return rand();
    }
    int main(void)
    {
        int myarray[10];
        /* getNextRandomValue 不能加括号，否则无法编译，因为加上括号之后相当于传入此参数时传入了 int , 而不是函数指针*/
        populate_array(myarray, 10, getNextRandomValue);
        for(int i = 0; i < 10; i++) {
            printf("%d ", myarray[i]);
        }
        printf("\n");
        return 0;
    }
### 运行如果
1804289383 846930886 1681692777 1714636915 1957747793 424238335 719885386 1649760492 596516649 1189641421 
<BR><BR><BR>

# C字符串
## C 中有大量操作字符串的函数：
<br>

| 函数 |   目的 | 
|:--------| :---------| 
| strcpy(s1, s2); | 复制字符串 s2 到字符串 s1。|
|strcat(s1, s2);| 连接字符串 s2 到字符串 s1 的末尾。|
|strlen(s1);|返回字符串 s1 的长度。|
|strcmp(s1, s2);|如果 s1 和 s2 是相同的，则返回 0；如果 s1<s2 则返回小于 0；如果 s1>s2 则返回大于 0。|
|strchr(s1, ch);|返回一个指针，指向字符串 s1 中字符 ch 的第一次出现的位置。|
|strstr(s1, s2);|返回一个指针，指向字符串 s1 中字符串 s2 的第一次出现的位置。|
<Br>

## 实例

    #include <stdio.h>
    #include <string.h>
    int main ()
    {  char str1[10] = "抹茶";
       char str2[10] = "星冰乐";
       char str3[10];
        int lea ;
 
        /* 复制 str1 到 str3 */
       strcpy(str3, str1);
       printf("strcpy( str3, str1) :  %s\n", str3 );
 
        /* 连接 str1 和 str2 */
       strcat( str1, str2);
       printf("strcat( str1, str2):   %s\n", str1 );
 
       /* 连接后，str1 的总长度 */
       lea = strlen(str1);
       printf("strlen(str1) :  %d\n", lea );
       return 0;
    }

### 运行结果
strcpy( str3, str1) :  抹茶  
strcat( str1, str2):   抹茶星冰乐  
strlen(str1) :  15（5个字符）
<br><Br>

# C 结构体
## C 数组允许定义可存储相同类型数据项的变量，结构是 C 编程中另一种用户自定义的可用的数据类型，它允许您存储不同类型的数据项。

## 结构体中的数据成员可以是基本数据类型（如 int、float、char 等），也可以是其他结构体类型、指针类型等。
<br>

### 结构体的成员可以包含其他结构体，也可以包含指向自己结构体类型的指针，而通常这种指针的应用是为了实现一些更高级的数据结构如链表和树等。

    //此结构体的声明包含了其他的结构体
    struct COMPLEX
    {
        char string[100];
        struct SIMPLE a;
    };
    
    //此结构体的声明包含了指向自己类型的指针
    struct NODE
    {
        char string[100];
        struct NODE *next_node;
    };

## 访问结构成员
为了访问结构的成员，我们使用成员访问运算符（.）。成员访问运算符是结构变量名称和我们要访问的结构成员之间的一个句号。您可以使用 struct 关键字来定义结构类型的变量。下面的实例演示了结构的用法：

    #include <stdio.h>
    #include <string.h>

    struct Books
    {
        char  title[50];
        char  author[50];
        char  subject[100];
        int   book_id;
    };
 
    int main( )
    {
        struct Books Book1;        /* 声明 Book1，类型为 Books */
        struct Books Book2;        /* 声明 Book2，类型为 Books */
 
        /* Book1 详述 */
        strcpy( Book1.title, "C Programming");
        strcpy( Book1.author, "Ali"); 
        strcpy( Book1.subject, "C Tutorial");
        Book1.book_id =001;
 
        /* Book2 详述 */
        strcpy( Book2.title, "SQL");
        strcpy( Book2.author, "Tom");
        strcpy( Book2.subject, "SQL Tutorial");
        Book2.book_id = 002;
 
        /* 输出 Book1 信息 */
        printf( "Book 1 title : %s\n", Book1.title);
        printf( "Book 1 author : %s\n", Book1.author);
        printf( "Book 1 subject : %s\n", Book1.subject);
        printf( "Book 1 book_id : %d\n", Book1.book_id);
 
        /* 输出 Book2 信息 */
        printf( "Book 2 title : %s\n", Book2.title);
        printf( "Book 2 author : %s\n", Book2.author);
        printf( "Book 2 subject : %s\n", Book2.subject);
        printf( "Book 2 book_id : %d\n", Book2.book_id);
 
        return 0;
        }
### 运行结果
Book 1 title : C Programming  
Book 1 author : Ali  
Book 1 subject : C Tutorial  
Book 1 book_id : 1  
Book 2 title : SQL  
Book 2 author : Tom  
Book 2 subject : SQL Tutorial  
Book 2 book_id : 2  
<BR><br>

# C 共用体
### 共用体是一种特殊的数据类型，允许您在相同的内存位置存储不同的数据类型。您可以定义一个带有多成员的共用体，但是任何时候只能有一个成员带有值。共用体提供了一种使用相同的内存位置的有效方式。
## 定义共用体
### 为了定义共用体，您必须使用 union 语句，方式与定义结构类似。union 语句定义了一个新的数据类型，带有多个成员。union 语句的格式如下：
    union [union tag]
    {
      member definition;
      member definition;
      ...
      member definition;
    } [one or more union variables];

### union tag 是可选的，每个 member definition 是标准的变量定义，比如 int i; 或者 float f; 或者其他有效的变量定义。	
