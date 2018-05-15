# 测试文档  

## tailsitter.cpp  
	1. 垂直起降前的过度时间  
	2. 垂直起降前过度阶段2的时间  
	3. 回转型垂直起降时间  
	4. 垂直起降的飞行速度可以切换到防火墙模式  
	5. 开始垂直起降速度混合MC/FW控制  
	6. 在飞行里垂直起降锁住升降附翼  
	7. 过度时间  
	8. 在转换代码中，避免导致零分割的参数  
	

	




# PX4 uORB通信机制  
## 第一步 在msg的文件目录下新建一个my_pencil.msg,添加变量
```C++
uint64 quality  
uint64 color  
uint64 length  
uint64 price  
```
并在msg的目录文件夹下的CMakeLists.txt下添加my_pencil.msg  

## 第二步 公告主题  
在需要用到这个主题的文件中添加头文件：``` #include <uORB/topics/my_pencil.h> ```  
```C++
/* 定义话题结构 */
struct my_pencil_s test_pencil;  
memset(&test_pencil,0,sizeof(test_pencil));  
/* 公告主题 */
orb_advert_t test_pencil_pub = orb_advertise(ORB_ID(my_pencil),&test_pencil);  
/* 赋值 */
test_pencil.quality = 11;  
test_pencil.color = 12;  
test_pencil.length = 13;  
test_pencil.price = 14;  

```
需要注意的是上面这些步骤不能一直放在``` while(1) ```里面，否则会报错。但是发布主题是可以一直放在``` while(1) ```里面的。  
## 第三步 发布主题  

```C++

while(1){
	/* 发布主题 */
	orb_publish(ORB_ID(my_pencil),test_pencil_pub,&test_pencil);
}
```  

在其他函数使用订阅主题时，也不能把订阅函数放在```while(1)```里面，但是```orb_copy```函数可以一直放在```while(1)```里面   
## 第四步 订阅主题  
```C++  

/* 订阅主题 */
int test_pencil_sub_fd = orb_subscribe(ORB_ID(my_pencil));  
struct my_pencil_s pencil_data_copy;  

while(1) {
	/* 复制数据 */  
	orb_copy(ORB_ID(my_pencil),test_pencil_sub_fd,&pencil_data_copy);  
	PX4_WARN("[Pencil] quality color length price:\t%8.4f\t%8.4f\t%8.4f\t%8.4f",
						(double)pencil_data_copy.quality,
						(double)pencil_data_copy.color,
						(double)pencil_data_copy.length,
						(double)pencil_data_copy.price);  
}

``` 
注意在打印数据显示时一定要注意数据类型  
