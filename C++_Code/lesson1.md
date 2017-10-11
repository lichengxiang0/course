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



