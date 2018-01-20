# 2.

# Linux Basic
- File Structure and Inode
理解inode首先要理解以下两个部分
第一是文件在硬盘上的存储，硬盘（磁盘）的最小存储单位是“扇区”（sector）, each sector store around 0.5KB;
OS在读取硬盘时，一般一次连续读取多个sector，也就是一个“块”(block), 一般是4KB，也就是8个sector.

第二呢，就是文件，任何文件实际都是binary code，那么他们都存储在块里 （硬盘数据区）

但是除了纯粹的文件内容，我们还需要知道文件的一些 meta data（data that describe data），比如文件的大小，创建日期，权限等等。
那么 这些metadata的存放区域就是inode,当然也在硬盘里 (inode table区域)。

- Hard Link & Soft Link
Unix/Linux系统允许，多个文件名指向同一个inode号码。
这意味着，可以用不同的文件名访问同样的内容；对文件内容进行修改，会影响到所有文件名；但是，删除一个文件名，不影响另一个文件名的访问。这种情况就被称为"硬链接"

"软链接"（soft link）或者"符号链接（symbolic link）和shortcut很像
- Permissions


# C Basics, Data Types, printf, scanf, 
## C Basic Structure
C 程序主要包括以下部分：
- 预处理器指令
- 函数
- 变量
- 语句 & 表达式
- 注释

##All about Data 数据
计算机中存储的数据可以分为两种：静态数据和动态数据。
- 静态数据是指一些永久性的数据，一般存储在硬盘中
- 动态数据指在程序运行过程中，动态产生的临时数据，一般存储在内存中
1 KB = 1024 B，1 MB = 1024 KB，1 GB = 1024 MB，1 TB = 1024 GB

### 数据类型
基本类型的话就俩：整数类型和浮点类型。

# Escape Sequence

```c
#include <stdio.h>
#include <float.h>
#include <limits.h>
int main()
{   
   printf("int 存储大小 : %lu \n", sizeof(int));
   printf("float 存储最大字节数 : %lu \n", sizeof(float));
   printf("float 最小值: %E\n", FLT_MIN );
   printf("float 最大值: %E\n", FLT_MAX );
   printf("int 最小值: %d\n", INT_MAX );
   printf("int 最大值: %d\n", INT_MIN );
   printf("精度值: %d\n", FLT_DIG );
   int a = 0x1D;
   int b = 0b110; // 十进制数：6
      
   int c = 021; // 十进制数：17
      
   int d = 12; // 十进制数：12
      
   int e = 0x1D; // 十进制数：29      
   printf("变量a的值为%d", a);  
   return 0;
}
```
打印乘法口诀 （printf）
```c
#include <stdio.h>
int main(int argc, char *argv[]){
  int i,j;
  for (i=1; i<=9; i++){
      for (j=1; j<=i; j++){
         printf ("%d*%d=%d;",i,j,i*j);
       }
      printf ("\n");
    }
  return 0;
}
```
# C array, pointers
数组它可以存储一个固定大小的相同类型元素的顺序集合。
所有的数组都是由连续的内存位置组成。最低的地址对应第一个元素，最高的地址对应最后一个元素。

### Pointer
C语言的特点以及难点就是指针啦，通过指针，可以简化一些C编程任务的执行，还有一些任务，如动态内存分配，没有指针是无法执行的。

每一个变量都有一个内存位置，每一个内存位置都定义了可使用连字号(&)运算符访问的地址，它表示了在内存中的一个地址

回想一下，我们之前是通过变量名来直接引用变量，然后进行赋值：
```c
char a;
a = 10;
```
实际上是对变量所在的存储空间进行写入或取出数据。就上面的代码而言，系统会自动将变量名a转换为变量的存储地址，根据地址找到变量a的存储空间，然后再将数据10以2进制的形式放入变量a的存储空间中
a - > a的地址 -> data
这个叫做直接引用

假如我们把a的地址存在另一个变量里面
a -> a的地址 -> data
b -> b的地址 -> a的地址
根据 变量名b 获取 变量b 的地址ffc2，取出变量b中存储的内容ffc1，也就是变量a的地址，再根据变量a的地址ffc1找到a的存储空间，然后修改里面的数据
我们说变量b就是个"指针变量"，我们可以说指针变量b指向变量a。

# 一维数组与指针
既然数字变量可以被指针指，那么同样的，数组及其数组元素都占有存储空间，都有自己的地址，因此指针变量可以指向整个数组，也可以指向数组元素

## 二维数组
1> 数组a的地址是ffc1，数组a[0]的地址也是ffc1，即a = a[0]；

2> 元素a[0][0]的地址是ffc1，所以数组a[0]的地址和元素a[0][0]的地址相同，即a[0] = &a[0][0]；
3> 最终可以得出结论：a = a[0] = &a[0][0]，以此类推，可以得出a[1] = &a[1][0]

```c
#include <stdio.h>
int main(){
    char a = 'A'; // A的ASCII值为65
    int b = 66;
    printf("Value of A: %d\n", a );
    printf("char b is: %c\n", b );
    printf("16进制:%x\n", &a);
    printf("10进制:%d\n", &a);
    char *pointer_to_a = &a;
    int *pointer_to_b = &b;
    printf("16进制:%x\n", pointer_to_a);
    printf("10进制:%d\n", pointer_to_b);
    printf("Value inside origin:%d\n", *pointer_to_b);
    *pointer_to_b = a;
    printf("Value inside after:%d\n", *pointer_to_b);
    // 1-D array
    int array_example[3];
    int array_example2[2] = {8, 10};
    /* Wrong
    int a[]; // 没有指定元素个数，错误
    int i = 9;
    int a[i]; // 用变量做元素个数，错误
    */
    //C语言中编译器是不会对数组下标越界进行检查的，所以自己访问数组元素时要小心
    int initialize_array[] = {2, 5, 7}; //OK, 因为初始化

    /*2-D array  类型  数组名[行数][列数]*/ 
    int two_d_array[2][3]; // 共2行3列，6个元素
    //a = a[0] = &a[0][0]，以此类推，可以得出a[1] = &a[1][0]
    //如果只初始化了部分元素，可以省略行数，但是不可以省略列数
    int two_d_array1[][3] = {1, 2, 3, 4, 5, 6};
    //int two_d_array1[][3] = {{1, 2, 3}, {3, 5}, {}};
    // 为啥呢，因为不知道行数会有很多不确定性
    //int two_d_array1[2][] = {1, 2, 3, 4, 5, 6}; // 错误写法
    printf("16进制:%x\n", two_d_array1);
    printf("16进制:%x\n", two_d_array1[0]);
    printf("16进制:%x\n", &two_d_array1[0][0]);
}
```
# Pointer & swap
```c
void swap(chat v1, char v2){
    printf("In SWAP Function Space - Before: v1=%d, v2=%d\n", v1, v2);
    char temp;
    temp = v1;
    v1 = v2;
    v2 = temp;
    printf("In SWAP Function Space - After: v1=%d, v2=%d\n", v1, v2);
}

int main(){
    char a = 65, b = 66;
    printf("In Main Function Space - Before: a=%d, b=%d\n", a, b);
    swap(a, b);
    printf("In Main Function Space - After: a=%d, b=%d\n", a, b);
    return 0;
}
```
```c
void swap(char *v1, char *v2) {
       char temp; 
      // 取出v1指向的变量的值
      temp = *v1;    
     // 取出v2指向的变量的值，然后赋值给v1指向的变量
      *v1 = *v2;   
     // 赋值给v2指向的变量
     *v2 = temp;
}
 
 int main()
 {
     char a = 10, b = 9;
     printf("更换前：a=%d, b=%d\n", a, b);
     
     swap(&a, &b);
     
     printf("更换后：a=%d, b=%d", a, b);
     return 0;
 }
```

# LeetCode 7

```c
int reverse(int x) {
    int newN =0, left =0; 
     bool negative = false;
     if(x < 0){
        negative = true;
        x = -x;
     }
    while(x != 0)  {
        left = x%10; 
        if( newN > (INT_MAX - left ) / 10 )  {   
            return 0;}
        
        newN = newN*10 + left;
        x = x/10; 
    }
    if (negative){
        return -newN;
    }
    else{
        return newN; 
    }
}
```

```py
class Solution:  
    # @param {integer} x  
    # @return {integer}  
    def reverse(self, x):  
        flag=1 
        if x<0:
            flag = -1
        if x < 0:
            x = -x
        res=0  
        while x>0:  
            if res*10.0 + x%10 > 2147483647:
                return 0  
            res = res*10+x%10  
            x//=10  
        return res*flag 
```
