# Pointer & Dynamic Memory

一、预备知识—程序的内存分配
一个由C/C++编译的程序占用的内存分为以下几个部分
1、栈区（stack）— 由编译器自动分配释放 ，存放函数的参数值，局部变量的值等。其
操作方式类似于数据结构中的栈。
2、堆区（heap） — 一般由程序员分配释放， 若程序员不释放，程序结束时可能由OS回
收 。注意它与数据结构中的堆是两回事，分配方式倒是类似于链表，呵呵。
3、全局区（静态区）（static）—，全局变量和静态变量的存储是放在一块的，初始化的
全局变量和静态变量在一块区域， 未初始化的全局变量和未初始化的静态变量在相邻的另
一块区域。 - 程序结束后由系统释放。
4、文字常量区 —常量字符串就是放在这里的。 程序结束后由系统释放
5、程序代码区—存放函数体的二进制代码。


二、例子程序  
这是一个前辈写的，非常详细  
```c
int a = 42;
char *p1;

int main()  {  
  int b; //栈  
  char s[] = "abc"; //栈  
  char *p2; //栈  
  char *p3 = "123456"; //123456\0在常量区，p3在栈上。  
  static int c =0; //全局（静态）初始化区  
  p1 = (char *)malloc(10);  
  p2 = (char *)malloc(20);  
  //分配得来得10和20字节的区域就在堆区。  
  strcpy(p1, "123456");  
  free(p1);
  free(p2);
  /*123456\0放在常量区，编译器可能会将它与p3所指向的"123456"
优化成一个地方。*/  
}    
```

## String & String Literal
常见的字符串操作函数 **#include <string.h>**
有几个概念需要区分一下：
- 字符串 (string literal)
- char array (存字符串的话是字符串**变量**)
- char pointer （指向字符串常量）
常见错误有：
```c
char s[10];
s = "some string"; 
//s[10] = "sad"; // correct

char *s = "original string";
*s = "revised string 233 long";
*s = "short";
```
因为s是个常量，代表数组的首地址，不能进行赋值运算
如果改成 *s 的话就对了， 或者s[]..

第二个的问题，首先如果真的把长的string放进原来的地址，
那一定会导致内存溢出；其次，string literal在static segment
算是常量 （const），所以没法修改。

那如果真的想修改怎么办？
- 字符串变量， 即  char array
- 一些处理字符串的函数 

## 输入数组，找最大最小数
### 2-D char array example with looping
```c
/*2-D pointer example and loop over string list*/
#include <stdio.h>
int main(int argc, char *argv[])
{
  char *strings[]={"C language",
       "is",
       "easy",
       "only if",
       "keep practicing"};  //使用指针数组创建字符串数组
  char **p,i;
  p=strings;    //指针指向字符串数组首地址
  for (i=0; i<5; i++)
    {
      printf ("%s\n",*(p+i));
    }
  return 0;
}
```

```c
/*Find the minimum and the maximum of Input array*/
#include <stdio.h>
void max_min(int a[],int n,int *max,int *min)
{
  int *p;
  *max = *min = *a;
  for(p = a + 1; p < a + n ; p++){  
      if(*p > *max)
         *max = *p;
      else if(*p < *min)
         *min = *p;
    }
}
int main(int argc, char *argv[])
{
  int i,a[10];
  int max,min;
  printf ("input 10 integer numbers you want to operate:\n");
  for(i=0;i<10;i++)
    scanf("%d",&a[i]);
  max_min(a,10,&max,&min);
  printf ("the maximum number is:%d\n",max);
  printf ("the maximum number is:%d\n",min);
  return 0;
}
```


# Struct
```c
/*链表与插入*/
#include <stdio.h>
#include <malloc.h>
#include <stdlib.h>
struct student
{
  int num;
  struct student *next;
};

struct student *create(int n)
{
  int i;
  struct student *head,*p1,*p2;
  int a;                   
  head=NULL;                 //初始化头节点地址
  printf ("the record:\n");
  for (i=n; i>0; --i){
      p1=(struct student*)malloc(sizeof(struct student));
      scanf("%d",&a);
      p1->num=a;
      if (head==NULL)       //（head/p2)-->(p1/p2)-->...
    {
      head=p1;
      p2=p1;
    }
      else
    {
      p2->next=p1;       //指定后继指针
      p2=p1;
    }
    }
  p2->next=NULL;             //后继指针为空，链表结束
  return head;               //返回头节点
}
struct student *insertnode(struct student *head,char x,int i)
{
  int j=0;
  struct student *p,*s;
  p=head;
  while(p&&j<i-1)     //找到要插入的位置
    {
      p=p->next;
      ++j;            //先对j进行++，然后再用j进行运算
    }
  if(!p||j>i-1)
    exit(1);
  s=(struct student*)malloc(sizeof(struct student));
  s->num=x;
  s->next=p->next;
  p->next=s;
}
int main(int argc, char *argv[])
{
  int n,i;
  int x;
  struct student *q;
  printf ("input the count of the nodes you want to creat:\n");
  scanf("%d",&n);
  q=create(n);
  i=2;
  x=123;
  insertnode(q,x,i);
  printf ("the result is:\n");
  while(q)              //输出插入节点后的链表
    {
      printf ("%d ",q->num);
      q=q->next;
    }
  return 0;
}
```

# A1

```c
int main(int argc, char *argv[]) {
  
  char user[127];
  int pid = 0;
  float cpu = 0;
  float mem = 0;
  int vsz = 0;
  int rss = 0;
  char tty[99];
  char stat[99];
  char start[99];
  char time[99];
  char command[127];
  
  char *mode;
  int found = 0;
  char *user_select;
  int pid_high = 0;
  float cpu_high = -1;
  float mem_high = -1;
  char command_high[127] = "";
  
  if (argc == 1 || argc > 3 ) {
    printf("Invalid number of arguments.\nUsage: hogs [-c | -m] file...\n");
        return 1;
    
  } else {
    
    // Check whether -c or -m
    if (argc == 3) {
      user_select = argv[2];
      if (strcasecmp("-c", argv[1]) == 0) {
        mode = "-c";
      } else if (strcasecmp("-m", argv[1]) == 0) {
        mode = "-m";
      } else {
        printf("Invalid arguments.\nUsage: hogs [-c | -m] file...\n");
        return 1;
      }
      
    // User did not input [-c | -m] argument, default to -c
    } else {
      mode = "-c";
      user_select = argv[1];
    }
    
    // Read stdin
    while (scanf("%s", user) != EOF) {
      scanf("%d", &pid);
      scanf("%f", &cpu);
      scanf("%f", &mem);
      scanf("%d", &vsz);
      scanf("%d", &rss);
      scanf("%s", tty);
      scanf("%s", stat);
      scanf("%s", start);
      scanf("%s", time);
      scanf("%127[^\n]", command);
      
      // User matches
      if (strcmp(user_select, user) == 0) {
        found = 1;
        
        // Current process has higher cpu
        if ((cpu > cpu_high) && (strcmp("-c", mode) == 0)) {
          pid_high = pid;
          cpu_high = cpu;
          strcpy(command_high, command);
          
        // Current process has higher mem
        } else if ((mem > mem_high) && (strcmp("-m", mode)) == 0) {
          pid_high = pid;
          mem_high = mem;
          strcpy(command_high, command);
          
        // Current process has same cpu
        } else if ((cpu == cpu_high) && (strcmp("-c", mode) == 0)) {
          
          // Check which command comes alphabetically first
          if (strcasecmp(command_high, command) > 0) {
            pid_high = pid;
            cpu_high = cpu;
            strcpy(command_high, command);
          }
        
        // Current process has same mem
        } else if ((mem == mem_high) && (strcmp("-m", mode) == 0)) {
          
          // Check which command comes alphabetically first
          if (strcasecmp(command_high, command) > 0) {
            pid_high = pid;
            mem_high = mem;
            strcpy(command_high, command);
          }
        } else {
          //do nothing
        }
      }
    }
    
    // Print only if the user was found at least once
    if (found == 1) {
      if (strcmp("-c", mode) == 0) {
        printf("%d\t%.1f\t%s\n", pid_high, cpu_high, command_high);
      } else {
        printf("%d\t%.1f\t%s\n", pid_high, mem_high, command_high);
      }
    }
    
    return 0; 
  }
}
```


# Stream


### 读写文件
https://github.com/yaouser/C/blob/master/3%E6%96%87%E4%BB%B6%E5%BC%80%E5%8F%91%E6%8A%80%E5%B7%A7/%E6%96%87%E4%BB%B6%E6%93%8D%E4%BD%9C

```c
#include <stdio.h>
int main(int argc, char *argv[])
 {
   int i,flag=1;
   char str[80],filename[50];
   FILE *fp;
   printf ("please input filename:\n");
   scanf("%s",filename);
   if ((fp=fopen(filename,"w"))==NULL)
     {
       printf ("cannot open!\n");
       exit(0);
     }
   while(flag==1)
     {
       printf ("\ninput string:\n");
       scanf("%s",str);
       fprintf(fp,"%s",str);  //将str字符串内容以%s形式写到fp所指文件上
       printf ("continue:?\n");
       if((getchar()=='N')||(getchar()=='n'))
      flag=0;
     }
   fclose(fp);
   fp=fopen(filename,"r");
   while(fscanf(fp,"%s",str)!=EOF)
     {
       for(i=0;str[i]!='\0';i++)
     if((str[i]>='a')&&(str[i]<='z'))
       str[i]-=32;
       //将小写字母转换为大写字母
       printf ("%s\n",str);
     }
   fclose(fp);
   return 0;
 }
```


###修改文件
```c
/*删除文件中的记录*/
#include <stdio.h>
#include <string.h>
 struct emploee  //定义结构体，存放员工工资信息
{
  char name[10];
  int salary;
}emp[20];
main()
{
  FILE *fp1,*fp2;
  int i,j,n,flag,salary;
  char name[10],filename[50];//定义数组为字符类型
  printf ("please input filename:\n");
  scanf("%s",filename); //输入要录入的人数
  printf ("please input the number of emploees:\n");
  scanf("%d",&n);
  printf ("input name and salary:\n");
  for (i=0; i<n; i++)
    {
      printf ("NO%d:\n",i+1);
      scanf("%s%d",emp[i].name,&emp[i].salary);
      //输入员工姓名及工资
    }
  if ((fp1=fopen(filename,"ab"))==NULL)//以追加的方式打开指定的二进制文件
    {
      printf ("can not open the file\n");
      exit(0);
    }
  for (i=0; i<n; i++)
    //将输入的员工信息输出到磁盘文件上
    if(fwrite(&emp[i],sizeof(struct emploee),1,fp1)!=1)
      printf ("error\n");
  fclose(fp1);
  if ((fp2=fopen(filename,"rb"))==NULL)
    {
      printf ("can not open file\n");
      exit(0);
    }    
  printf ("original data:\n");
  //读取磁盘文件上的信息到emp数组中
  for(i=0;fread(&emp[i],sizeof(struct emploee),1,fp2)!=0;i++)
    printf ("%8s%7d\n",emp[i].name,emp[i].salary);
  n=i;
  fclose(fp2);
  printf ("input name which do you want to delete:\n");
  scanf("%s",name);  //输入要删除的员工姓名
  for (flag=1,i=0; flag&&i<n; i++)
    {
      if (strcmp(name,emp[i].name)==0)  //查找与输入姓名相匹配的位置
{
  for (j=i; j<n-1; j++)
    {
      //查找到要删除信息的位置后将后面信息前移
      strcpy(emp[j].name,emp[j+1].name);
      emp[j].salary=emp[j+1].salary;
    }
  flag=0;//标志位置0
 }
    }
  if (!flag)
    n=n-1;  //记录个数减一
  else
    printf ("not found\n");
  printf ("now,the content of file:\n");
  fp2=fopen(filename,"wb");  //以只写方式打开指定二进制文件
  for(i=0;i<n;i++)
    //将数组中的员工工资信息输出到磁盘文件上
    fwrite(&emp[i],sizeof(struct emploee),1,fp2);
  fclose(fp2);
  fp2=fopen(filename,"rb");  //以只读方式打开指定二进制文件
  //以只读方式打开指定二进制文件
  for(i=0;fread(&emp[i],sizeof(struct emploee),1,fp2)!=0;i++)
    //输出员工工资信息
    printf ("%8s%7d\n",emp[i].name,emp[i].salary);
  fclose(fp2);
  return 0;
}
```

## LeetCode 206


Reverse Linked List

### Iterative Algorithm:
```c
/**
 * Definition for singly-linked list.
 * struct ListNode {
 *     int val;
 *     struct ListNode *next;
 * };
 */
struct ListNode* reverseList(struct ListNode* head) {
    
    struct ListNode* next = NULL;
    struct ListNode* cur = NULL;
    struct ListNode* prev = NULL;
    
    if ( head == NULL ) 
    {
        return NULL;
    }
    next = head->next;
    cur = head;
    prev = head;
    while ( next )
    {
        cur->next = next->next;
        next->next = prev;
        prev = next;
        next = cur->next;
    }
    
    return prev;    
}
```
### Recursive one
```c
struct ListNode* reverseList(struct ListNode* head) {
    if(NULL==head||NULL==head->next) return head;

    struct ListNode *p=head->next;
    head->next=NULL;
    struct ListNode *newhead=reverseList(p);
    p->next=head;

    return newhead;
}
```

## Python Version

```py
class Solution:
# @param {ListNode} head
# @return {ListNode}
def reverseList(self, head):
    prev = None
    while head:
        curr = head
        head = head.next
        curr.next = prev
        prev = curr
    return prev
```


```py
class Solution:
# @param {ListNode} head
# @return {ListNode}
def reverseList(self, head):
    return self._reverse(head)

def _reverse(self, node, prev=None):
    if not node:
        return prev
    n = node.next
    node.next = prev
    return self._reverse(n, node)
```