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

