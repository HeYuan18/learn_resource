##占位符
|%|对应类型|
|---|----
|d|int
|c|char 
|s|char *
|f|float,double
|p|指针类型
|lf|double
|lu|unsigned long
>在printf的时候double类型可以用%f或%lf。而scanf的时候double要用%lf

当用%p输出指针地址的时候，格式是**0x**加上十六进制地址值。如果为空指针则打印**(nil)**。  
###格式化串 "%a.bs"  
- 对于a,它表示如果字符串长度小于a,那么右对齐左边补空格，若大于a则原样输出不限制
- 对于b，它表示如果字符串长度超过b，那么只取前b个

##参数压栈顺序
printf的参数压栈顺序是从右到左的，所以：
```c
	char a[] = "abcde";
	char *p = a;
	printf("%c %c\n",*p,*(++p));
```
打印结果为：`b b`
##格式化字符串
```c
printf("%7.2s\n%-5.3s\n","hello","world");
printf("%.4s","jelly");
```
**%7.2s**表示输出的字符串占7个位置，右对齐，左补空格，输出2个字符。  
**%-5.3s**表示输出的字符串占5个位置，左对齐，右补空格，输出3个字符。  
##可变长度的格式化输出
```c
int var = 5;
printf("%*d\n",var,123);
//等价于
printf("%5d\n",123);
```

-----------------
##ANSI控制码
适用于Linux系统。用法比如：
```c
printf("\33[1m hello world\33[0m");
```

|控制码|说明
|---|----
|\33[0m |关闭所有属性    
|\33[1m |设置高亮度 
|\33[4m |下划线 
|\33[5m |闪烁 
|\33[7m |反显 
|\33[8m |消隐 
|\33[nA |光标上移n行 
|\33[nB |光标下移n行 
|\33[nC |光标右移n行 
|\33[nD |光标左移n行 
|\33[y;xH |设置光标位置 
|\33[2J |清屏 
|\33[K |清除从光标到行尾的内容 
|\33[s |保存光标位置 
|\33[u |恢复光标位置 
|\33[?25l |隐藏光标 
|\33[?25h |显示光标
|\33[30m -- \33[37m |设置前景色 
|\33[40m -- \33[47m |设置背景色 

###颜色码
	格式： \033[X ;Y m  ……  \033[0m 
X (字背景颜色范围):40--49  
40:黑 41:深红 42:绿 43:黄色 44:蓝色 45:紫色 46:深绿 47:白色  
Y (字颜色):30--39  
30:黑 31:红 32:绿 33:黄 34:蓝色 35:紫色 36:深绿 37:白色  

##Trick
###printf("5432"+1)
这条语句看似无理，实则有理。输出是**432**。  
"5432"是一个字符串。+1就是指针位置+1。相当于：
```c
char a[] = "5432";
printf("%s",a+1);
```

