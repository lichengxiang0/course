# C++  
	C++的变量对大小写敏感  
	有效的标识符是字母、数字或者下划线。  
	C++能够操作的最小内存单元是一个字节（byte）
	
## 数据类型  
	名称      字节数     描述           范围  
	char   1	   8位bits	有符号：-128到127；无符号：0到255  
	
	short   2      16位bits
	
	
	......  
	
	
## 变量的范围  
	C++和C语言的不同：C++的变量可以在任意处定义变量，C语言只能在文件的开头定义文件。但是为了方便后面的debug，我们通常遵守C语言的习惯，都放在程序的开头  

## 操作运算符  
	C++的=号可以这样用  
```  
a=2+(b=5);  
```  
等同于：  
```  
b=5;
a=2+b;  
```  
最终的结果是7  
下面在C++中写也是对的  
```  
a=b=c=5;  
```  


## 基本输入输出  
	在C++的iostream函数库中，cin给输入使用，cout给输出使用，cerr和clog显示出错信息  
	<< 叫做插入运算符  

```C++  
#incluude <iostream>  
#include <string>
#include <sstream>
using namespace std;

int main()
{
	string mystr;  
	float price = 0;
	getline(cin,mystr);
	stringstream(mystr)>>price;
	cout<<price<<endl;
	return 0;
}
```  

通过getline函数，键盘输入赋值给mystr，在用getline函数提取mystr的值给price  



## 数组  
两种方法初始化字符串mystring:  
char mystring[]={'H','e','l','l','o','\0'};  
char mystring[]="Hello";  
注：双引号表示一串连续字符的常量，它的结尾总是自动加上一个空字符（'\0'）  

C++的输入捕获  
当cin被用来输入字符序列值时，它通常与函数getline一起使用。方法如下：  
cin.getline( char buffer[],int length,char delimiter='\n' );  
*  buffer:存储输入烦人地址，例如一个数组名  
* length:缓存buffer的最大容量  
* delimiter:判断用户输入结束的字符，默认值是换行符  
下面是一个例子  

```C++
#include <iostream>  
using namespace std;

int main()
{
	char mybuffer[100];
	cout<<"What's your name?";  
	cin.getline(mybuffer,100);  
	cout<<"Hello"<<mybuffer<<".\n";
	cout<<"Which is your favorite team?";
	cin.getline(mybuffer,100);  
	cout<<"I like"<<mybuffer<<"too.\n";  
	return 0;
}

```
运行的结果:  
What's your name? Juan  
Hello Juan.  
Which is your favourite team? Inter Milan  
I like Inter Milan too.  

注意：  
我们也可以用这种方式获取用户输入：  
```C++  
	cin>>mybuffer
```  
这种方式也可以工作，但是它有以下极限性是cin.getline所没有的：  
- 它只能接收单独的词（而不是完整的句子），因为这种方法以任何空白符为分隔符，包括空格space,跳跃符tabulators，换行符newlines和回车符arriage returns。  
- 它不能给buffer制定容量，这使得程序不稳定，如果用户输入超出数组长度，输入信息会被丢失。  
因此，建议在需要用cin来输入字符串时，使用cin.getline来代替cin>>.  

## 字符串和其它数据类型的转换  
	用上面的方法：cin.getline(mybuffer,100);很容易获取到键盘的输入，并存储到数组mybuffer中，但是字符串数组可能包含有其它数据类型的内容，所以函数库cstdlib(stdlib.h)提供了三个有用的函数：  
* atoi:将字符串string转化为整形int  
* atol:将字符串string转化为长整型long  
* atof:将字符串string转化为浮点型float  

```C++  
#include <iostream>
#include <stdlib.h>
using namespace std;

int main()
{
	char mybuffer[100];
	float price;
	int quantity;
	cout << "Enter price:";
	cin.getline(mybuffer,100);
	price = atof(mybuffer);
	cout << "Enter quantity:";
	cin.getline(mybuffer,100);
	quantity = atoi(mybuffer);
	cout << "Total price:" << price*quantity<<endl;

	return 0;
}
```  
运行结果：  
Enter price:2.75  
Enter quantity:21  
Total price:57.75  

## 字符串操作函数  
列举4个常用的处理字符串的函数：  
- strcat: char* strcat (char* dest, const char* src); //将字符串src 附加到字符串dest 的末尾，返回dest。  

- strcmp: int strcmp (const char* string1, const char* string2); //比较两个字符串string1 和string2。如果两个字符串相等，返回0。  

- strcpy: char* strcpy (char* dest, const char* src); //将字符串src 的内容拷贝给dest，返回dest 。  

- strlen: size_t strlen (const char* string); //返回字符串的长度。  

## 指针  
### 地址操作符  
地址操作符：& ，又称为去引操作符。例如：  
```C++
	ted=&andy  
```  
将变量andy的地址赋值给变量ted,这时，我们指的不再是变量的内容，而是它在内存中的地址。  
假设andy被放在内存地址1776的单元中，然后我们有下列代码：  
```C++
	andy=25;  
	fred=andy;  
	ted=&andy;  
```
  fred和andy的值都是25，ted的值是1776.  
### 引用操作符  
使用指针的时候，我们可以通过在指针标识符的前面加星号（*）来存储该指针指向的变量所存储的数值，翻译为“所指向的数值”。例子：  
```C++
	beth = ted;//beth等于ted(1766)    
	beth = *ted;//beth等于ted所指向的数值25  
```  
***注：***  
__地址或反引用操作符（&）__  
	它被用作一个变量前缀，可以被翻译为“...的地址”，因此：&variable1可以被读作variable1的地址。  
__引用操作符（*)__  
 	表示地址所指向的内容。可以被翻译为“...指向的数值”，*mypointer可以被读作“mypoint指向的数值”。   
  
  下面举两个例子，第一个例子要简单点，第二个稍微复杂。  
  
```C++
#include <iostream>
using namespace std;

int main()
{
	int value1=5,value2=15;  
	int *mypointer;  
	mypointer=&value1;  
	*mypointer = 10;
	mypointer=&value2;
	*mypointer=20;
	cout<<"value1=="<<value1<<"value2=="<<value2<<endl;  
	return 0;
}

```  
运行结果：  
value1==10/value2==20  

/*************************************************/  
```C++
#include <iostream>  
using namespace std;  

int main()
{
	int value1=5,value2=15;  
	int *p1,*p2;  
	p1=&value1;  
	p2=&value2;  
	*p1=10;  
	*p2=*p1;  
	p1=p2;  
	*p1=20;  
	cout<<"value1=="<<value1<<"value2=="<<value2<<endl;  
	return 0;  
}

```  
运行结果：  
	value1==10/value2==20  
	
### 空指针  
void指针可以指向任意类型的数据，但是不可以被直接引用（不可以对他们使用引用星号*），因为它的长度是不固定的，因此，必须使用类型转换操作或赋值操作来把void指针指向一个具体的数据类型。  
用处之一是给函数传递通用参数：

```C++  
#include <iostream>
using namespace std;


void increase(void* data, int type)
{
	switch (type)
	{
	case sizeof(char) : (*((char *)data))++; break;
	case sizeof(short) : (*((short *)data))++; break;
	case sizeof(long) : (*((long *)data))++; break;
	default:break;
	}
}

int main()
{
	char a = 5;
	short b = 9;
	long c = 12;

	increase(&a, sizeof(a));
	increase(&b, sizeof(b));
	increase(&c, sizeof(c));
	cout << (int)a << "," << b << "," << c << endl;

	return 0;
}

```  

运行结果：  
6,10,13  


### 函数指针  
C++允许对指向函数的指针进行操作。它最大的作用是把一个函数作为参数传递给另外一个函数。声明一个函数指针像声明一个函数原型一样，除了函数的名字需要被扩在括号内并在前面加星号asterisk（*）。例如：  
```C++
#include <iostream>
using namespace std;

int addition(int a, int b)
{
	return (a + b);
}
int subtraction(int a, int b)
{
	return (a - b);
}

int (* minu)(int, int) = subtraction;
int operation(int x, int y, int(*functocall)(int, int))
{
	int g;
	g = (*functocall)(x,y);
	return(g);
}

int main()
{
	int m, n;
	m = operation(7,5,addition);
	n = operation(20,m,minu);
	cout << n << endl;

	return 0;
}
```  
运行结果为8  

在这个例子中，minu是一个全局指针，指向一个有两个整形参数的函数，它被赋值指向函数subtraction.  
这里int(*minu)(int,int)实际上是在定义一个指针变量，这个指针的名字叫做minu，这个指针的类型实际上是指向一个函数，函数的类型是有两个整形参数并返回一个整形值。  

## 动态内存分配  
到目前为止，程序中只用了声明变量、数组和其它对象（object）所需要的内存空间，这些内存空间的大小都在程序执行之前都已经确定。但是如果我们需要的内存大小是一个变量，其大小只有在我们程序运行时才能确定，有时候也需要根据用户输入来决定必须的内存空间，这是问题就来了，所以我们必须使用动态内存分配。  
	为此，C++集成了操作符new和delete.  
	
### 动态内存管理的函数  
- 函数malloc  
函数原型：void * malloc( size_t nbytes );  
其中nbyte是我们想要给指针分配的内存字节数。这个函数返回一个void*类型的指针，因此我么需要用类型转换来把它转换成目标所需要的数据类型。例如：  
```C++
char * ronny;
ronny=(char *)malloc(10);
```  
当我们想要给char以外的类型（不是一个字节的长度）的数值分配内存时，我们需要用元素数乘以每个元素的长度来确定所需要的内存大小。我们可以用操作符sizeof  
```C++  
int * bobby;
bobby=(int *)malloc(5*sizeof(int));  
```  
- 函数calloc  
calloc与malloc在操作上非常相似，他们主要的区别是在原型上：  
```C++
void * calloc(size_t nelements,size_t size);  
```  
第一个参数netements是元素的个数，第二个参数size被用来表示每个元素的长度。  
```C++
int * bobby;  
bobby=(int *)calloc(5,sizeof(int));  
```  
注意：malloc和calloc的另一点不同在于calloc会将所有的元素初始化为0.  

- 函数realloc  
改变已经被分配给一个指针的内存长度。  
```C++
void * realloc( void * pointer,size_t size );
```  
参数pointer用来传递一个已经被分配内存的指针或一个空指针。  
参数size用来指明新的内存长度。

- 函数free  
释放前面malloc,calloc或realloc所分配的空间。  
```C++
void free(void * pointer);
```  

## 数据结构  
一个数据结构是组合到同一定义下的一组不同类型的数据，各个数据类型的数据长度可能不同。例如：  
```C++
struct products
{
	char name[30];  
	float price;  
};
products apple;
products orange,melon;  
``` 
也可以这样声明：  
```C++
struct products
{
	char name[30];  
	float price;  
}apple,orange,melon;
``` 
下面是一个关于电影的例子：  
```C++
#include <iostream>
#include <string.h>
#include <stdlib.h>
using namespace std;

struct movies_t
{
	char title[50];
	int year;
}mine, yours;

void printmovie(movies_t movie);

int main()
{
	char buffer[50];
	strcpy_s( (mine.title), "2001 A Space Odyssey");
	mine.year = 1968;
	cout << "Enter title:";
	cin.getline(yours.title, 50);
	cout << "Entry years:";
	cin.getline(buffer, 50);
	yours.year = atoi(buffer);
	cout << "My favorite movie is:\n";
	printmovie(mine);
	cout << "And yours:\n";
	printmovie(yours);

	return 0;
}

void printmovie(movies_t movie)
{
	cout << movie.title;
	cout << "(" << movie.year << ")\n";
}

```
运行结果：  
Enter title:Alien  
Entry years:1979  
My favorite movie is:  
2001 A Space Odyssey(1968)  
And yours:  
Alien(1979)  
请按任意键继续. . .  


## 友元函数  
为了实现允许一个外部函数访问class的private和protected成员，必须在class内部用关键词friend声明外部函数原型，以指定允许函数共享class的成员。下面是一个例子：  
```C++  
#include <iostream>
using namespace std;

class CRectangle
{
	int width, height;
public:
	void set_values(int ,int);
	int area(void) 
	{
		return (width*height); 
	}
	friend CRectangle duplicate(CRectangle);

};

void CRectangle::set_values(int a, int b)
{
	width = a;
	height = b;
}

CRectangle duplicate(CRectangle rectparam)
{
	CRectangle rectres;
	rectres.width = rectparam.width * 2;
	rectres.height = rectparam.height * 2;
	return (rectres);
}

int main()
{
	CRectangle rect, rectb;
	rect.set_values(2,3);
	rectb = duplicate(rect);
	cout << rectb.area() << endl;
}


```  
运行的结果: 
```C 
	24  
```  

## 友元类  
```C++
#include <iostream>
using namespace std;

class CSquare;

class CRectangle
{
	int width, height;
public:
	int area(void)
	{
		return (width*height);
	}
	void convert(CSquare a);
};

class CSquare
{
private:
	int side;
public:
	void set_side(int a)
	{
		side = a;
	}
	friend class CRectangle;
};

void CRectangle::convert(CSquare a)
{
	width = a.side;
	height = a.side;
}

int main()
{
	CSquare sqr;
	CRectangle rect;
	sqr.set_side(4);
	rect.convert(sqr);
	cout << rect.area()<<endl;
	return 0;
}

```  
运行结果：
```C  
	16  
```  

这里说明一点，class之前包含一个CSquare的声明，应为我们在CRectangle引用了CSquare，而CSquare定义在后面，如果不声明，则在CRectangle是不可见的。  

