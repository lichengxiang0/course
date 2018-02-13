# 韦东山第一期ARM裸机加强版学习笔记 

## 汇编指令和伪指令 
```  
	mov R0, #0x12  //把0x12存入到R0寄存器当中  
```  
ARM汇编指令是32位的，其中mov和R0本身会占两位，mov可以表示简单数，又称为立即数  
如果需要存储的数值是32位，则需要用到伪指令LDR  
```  
	LDR R0, =0x12345678  //把一个32位的数值存储到R0寄存器中  
```  

伪指令执行会被拆开，本质上还是汇编指令  

		注：使用汇编指令是#，使用伪指令是=  
	

## grep查找字符串和find查找文件  



## 总结Tiny6410时钟初始化  
```C  

/* 时钟初始化 */
/*
* 第一步：设置Lock time.一般使用默认值
* 第二步：设置分频系数
* 第三步：设置CPU到异步工作模式
* 第四步：设置fclk
*/
///* 第一步使用默认即可，可以不用设置；直接进行第二步 */
	///*设置分频系数*/
#define CLK_DIV0 0x7e00f020
#define DIV_VAL ( ( 0x0<<0 )|( 0x1<<9 )|( 0x1<<8 )|( 0x3<<12 ) )
	ldr r0, =CLK_DIV0
	ldr r1, =DIV_VAL
	str r1, [r0]
	///* 设置CPU到异步工作模式 */
#define OTHERS 0x7e00f900
	ldr r0, =OTHERS
	ldr r1, [r0]
	bic r1, r1, #0xc0
	str r1, [r0]
	///*第四步，设置FCLK，即设置APLL,MPLL的频率*/
#define MPLL_CON 0X7e00f010
#define APLL_CON 0x7e00f00c
#define CLK_SRC  0x7e00f01c
#define PLL_VAL  ( (1<<31)|(266<<16)|(3<<8)|(1<<0) )
	ldr r0, =APLL_CON
	ldr r1, =PLL_VAL
	str r1, [r0]

	ldr r0, =MPLL_CON
	ldr r1, =PLL_VAL
	str r1, [r0]

	ldr r0, =CLK_SRC
	mov r1, #0x03
	str r1, [r0]

```  

这个时钟初始化需要理解时钟图  