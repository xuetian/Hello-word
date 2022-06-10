## 指针的含义（指针P= =地址）
- ==指针是一个变量，其值为另一个变量的地址==，即，内存位置的直接地址。就像其他变量或常量一样，您必须在使用指针存储其他变量地址之前，对其进行声明。
- 要理解指针就要先理解计算机的内存。计算机内存会被划分为按顺序编号的内存单元。每个变量都是存储在内存单元中的，称之为地址。
- 每一个变量都有一个内存位置，每一个内存位置都定义了可使用==**&**运算符访问的地址，它表示了在内存中的一个地址==。
- 定义一个指针变量、把变量地址赋值给指针、访问指针变量中可用地址的值。这些是通过使用==**一元运算符*** 来返回位于操作数所指定地址的变量的值==。
```C
#include <stdio.h>

int main ()
{
    int var = 20;   /* 实际变量的声明 此时的 VAR 这个变量是存在某个地址的，地址对应某个内存单元，该单元中存储了数据20 */
    int *ip;         /* 指针变量的声明 定义了一个指针 即一个内存单元的地址变量 */

    ip = &var;      /* 在指针变量中存储 var 的地址 就是将地址值赋值给指针这个变量*/

    /* 在指针变量中存储的地址 利用&符号直接输出了var所存储的数据的内存单元的地址*/
    printf("Address of var variable: %p\n", &var );
    
    /* 在指针变量中存储的地址 ip代表的是这个赋值到的地址的值 所以输出的是地址值 */
    printf("Address stored in ip variable: %p\n", ip );
    
    /* 使用指针访问值 *ip代表的是定义到这个内存单元之后，内存单元中所存储的数据的值也就是将20赋值给var中20这个值 */
    printf("Value of *ip variable: %d\n", *ip );

    return 0;
}
```
>var 变量的地址: 0x7ffeeef168d8
ip 变量存储的地址: 0x7ffeeef168d8
*ip 变量的值: 20

- ip=&var    内存中的地址值
- *ip  变量数据值
## 数组指针(指向数组首位的指针)
#### 声明数组
声明一个类型为 double 的包含 10 个元素的数组 **balance**，声明语句如下：

    double balance[10];

#### 初始化数组
在 C 中，您可以逐个初始化数组，也可以使用一个初始化语句，如下所示：
double balance[5] = {1000.0, 2.0, 3.4, 7.0, 50.0};
> - 大括号 { } 之间的值的数目不能大于我们在数组声明时在方括号 [ ] 中指定的元素数目。
>- 如果您省略掉了数组的大小，数组的大小则为初始化时元素的个数。因此，如果

    double balance[] = {1000.0, 2.0, 3.4, 7.0, 50.0};
为数组中某个元素赋值的实例：
![[Pasted image 20220610112650.png]]
    balance[4] = 50.0;
#### 指向数组首位的指针
##### 整型数组指针
- 数组名是一个指向数组中第一个元素的常量指针
- ==**balance** 是一个指向 &balance[0] 的指针，即数组 balance 的第一个元素的地址==。因此，下面的程序片段把 **p** 赋值为 **balance** 的第一个元素的地址：
```C
double *p;
double balance[10];

p = balance = &balance[0]; //balance是一个指向数组balance第0个地址的指针

```
![[Drawing 2022-06-10 13.51.58.excalidraw.svg]]  

    指向数组地址的指针
    p = balance = &balance[0]
    (p+1)=(balance+1)=&balance[1]
    (p+i)=(balance+i)=&balance[i]
	取指针地址中的数值
    *p=*balance=balance[0]=1000.0
    *(p+1) =*(balance+1)=balance[1]=2.0
    *(p+i) =*(balance+i)=balance[i]=p[i]
四种方式输出数组数值
```C
#include <stdio.h> 
int main () 
{ /* 带有 5 个元素的整型数组 */ 
	double balance[5] = {1000.0, 2.0, 3.4, 17.0, 50.0}; 
	double *p; 
	int i; 
	p = balance; //指针P指向balance数组第0个数据地址
	
	printf( "使用指针的数组值\n"); 
	for ( i = 0; i < 5; i++ ) 
	{ 
		printf("*(p + %d) : %f\n", i, *(p + i) ); 
	} 
	
	printf( "使用 balance指针作为地址的数组值\n"); 
	for ( i = 0; i < 5; i++ ) 
	{ 
		printf("*(balance + %d) : %f\n", i, *(balance + i) ); 
	} 
	
	printf( "使用 balance数组作为地址的数组值\n"); 
	for ( i = 0; i < 5; i++ ) 
	{ 
		printf("balance[%d]) : %f\n", i, balance[i] ); 
	} 
	
	printf( "使用 p[i] 作为地址的数组值\n"); 
	for ( i = 0; i < 5; i++ ) 
	{ 
		printf("p[%d]) : %f\n", i, p[i] ); 
	}
	return 0; 
}
```
![[Pasted image 20220610145459.png]]
##### 字符型数组指针
###### 字符数组
=== multi-column-start: ID_nhzz
```column-settings
Number of Columns: 2
Largest Column: standard
border:off
```

```C
#include <stdio.h>

int main ()

{
	char string[]="i love China!";
	
	printf("%s\n",string);
	
	printf("%c\n",string[7]);
	
	return 0;
	
}
```
![[Pasted image 20220610222112.png]]

=== end-column ===

```C
#include <stdio.h>
int main ()

{
    char string[]="i love China!";
    for (int i = 0; *(string+i)!='\0'; i++)
    { printf("%c",*(string+i));}
    printf("%c\n");
    printf("%c\n",*(string+7));
    return 0;

}
```
![[Pasted image 20220610222112.png]]

=== multi-column-end
>字符数组输出字符串和指针输出字符
###### 字符指针

=== multi-column-start: ID_si03
```column-settings
Number of Columns: 2
Largest Column: standard
border:off
```

```C
#include <stdio.h>

int main ()

{
	char *string="i love China!";
	
	printf("%s\n",string);
	
	
	
	return 0;
	
}
```
![[Pasted image 20220610222112.png]]

=== end-column ===

```C
#include <stdio.h>
int main ()
{
	char *string="i love China!";
	for (int i = 0; *(string+i)!='\0'; i++)
	{ printf("%c",*(string+i));}
	printf("%c\n");
	printf("%c\n",*(string+7));
	return 0;

}
```
![[Pasted image 20220610222112.png]]

=== multi-column-end
>字符指针输出字符串和指针输出字符

| i          |            | l          | o          | v          | e          |           | C         | h          | i          | n           | a           | !           | \0          |
| --------- | --------- | --------- | --------- | --------- | --------- | --------- | --------- | --------- | --------- | ---------- | ---------- | ---------- | ---------- |
| s[0] | s[1] | s[2] | s[3] | s[4] | s[5] | s[6] | s[7] | s[8] | s[8] | s[10] | s[11] | s[12] | s[13] |
| s+i          |           |           |           |           |           |           |           |           |           |            |            |            |            |
## 指针数组（指针类型的数组）
**指针数组和数组指针的区别**
- **数组指针**这个指针指向一个数组的首地址
- **指针数组**：指针的数组，实际是一个数组，长度由数组本身决定，这个数组的所有元素都是指针类型，存放的都是地址。
#### 整型指针数组
```C
#include <stdio.h>

const int MAX = 3;

int main ()

{

   int  var[] = {10, 100, 200};

   int i, *ptr[MAX];

   for ( i = 0; i < MAX; i++)

   {

      ptr[i] = &var[i]; //所存的是数组各数据的地址

   }

   for ( i = 0; i < MAX; i++)

   {

      printf("Value of var[%d] = %d\n", i, *ptr[i] );//取所存数组各数据地址对应的值

   }

   return 0;

}
```
![[Pasted image 20220610155818.png]]
#### 字符型指针数组
##### 单指针字符型指针数组

=== multi-column-start: ID_qmpc
```column-settings
Number of Columns: 2
Largest Column: standard
```

```C
#include <stdio.h>
const int MAX = 4;
int main ()
{
   const char *names[] = {
                   "Zara Ali",
                   "Hina Ali",
                   "Nuha Ali",
                   "Sara Ali",
   };
   int i = 0;
   for ( i = 0; i < MAX; i++)
   {
      printf("Value of names[%d] = %s\n", i, *(names+i) );//*(names+i)=names[i]
   }
   return 0;  
}
```
字符型指针数组元素即指针指向字符串首地址，输出该指针字符型元素即字符串

=== end-column ===

```C
#include <stdio.h>
const int MAX = 4;
int main ()
{
   const char *names[] = {
                   "Zara Ali",
                   "Hina Ali",
                   "Nuha Ali",
                   "Sara Ali",
   };
   int i = 0;
   for ( i = 0; i < MAX; i++)
   {
      printf("Value of names[%d] = %d\n", i, *(names+i) );//*(names+i)=names[i]
   }
   return 0;  
}
```

指针型数组中元素都是指针即地址，输出数值型元素即地址

=== multi-column-end


##### 双重指针字符型指针数组

=== multi-column-start: ID_14nb
```column-settings
Number of Columns: 2
Largest Column: standard
```

```C
#include <stdio.h>
const int MAX = 4;
int main ()
{
    const char *names[] = {
                   "Zara Ali",
                    "Hina Ali",
                    "Nuha Ali",
                    "Sara Ali",
    };
    int i = 0;
    char **p;
    p = names;
    for ( i = 0; i < MAX; i++)
    {
     printf("Value of names[%d] = %s\n", i, *(p+i) );
    }
    return 0;
}
```

=== end-column ===

```C
#include <stdio.h>
const int MAX = 4;
int main ()
{
    const char *names[] = {
                   "Zara Ali",
                    "Hina Ali",
                    "Nuha Ali",
                    "Sara Ali",
    };
    int i = 0;
    char **p;
    p = names;
    for ( i = 0; i < MAX; i++)
    {
     printf("Value of names[%d] = %d\n", i, *(p+i) );
    }
    return 0;
}
```

=== multi-column-end
