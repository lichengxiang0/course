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
	
