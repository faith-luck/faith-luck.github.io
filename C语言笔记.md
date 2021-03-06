## C语言学习笔记 ##
***

### 第一章   关键字 ###
C语言共有32个关键字；关键字按作用可分为声明、定义变量和函数，表示不同数据类型，表单流程结构，指定存储级别；关键字不能用作标识符。

 * 数据类型
  - 基本数据类型：void、char、int、float、double
  - 基本类型修饰：short、long、signed、unsigned
  - 复杂数据类型：struct、union、enum、typedef、sizeof
 * 存储级别
  - auto:自动变量，由编译器自动分配释放。通常在栈上。
  - static:静态变量，分配在静态变量区。静态函数，作用域为文件内部。
  - register:建议编译器将变量存储到寄存器中。
  - extern:指明变量为外部变量。
  - const:常量
  - volatile：本意是不稳定的，与const合称cv特性，用于可能被其他线程修改的变量。
 * 流程结构
  - 分支结构：if、else、switch、case、default（witch语句中可选）
  - 循环结构：for、do、while
  - 跳转结构：return、continue、break、goto

static 、auto 、external、register 使用例子

以上是c89标准，c99标准中增加了restrict、inline、_Bool等
参考：[C语言关键字详解](https://wenku.baidu.com/view/a7be91a0f524ccbff12184a8.html)
***
### 第二章   数据类型、取值范围 ###
* bit、byte、word 
 >1字节等于8比特，字长（word）与系统硬件，总线总线有关，32位系统字长是4字节，64位系统字长是8字节;  
 32位CPU有4个32位通用寄存器，低16位与16位CPU寄存器兼容。

* 原码、反码、补码的表示及转换关系
>正数反、补码都与原码相同；0的原码和反码有正0和负0的区别；运算中出现负数时先转换成补码再计算；</br>
>原码：如果机器字长为n,最高位是符号位，0表示整数，1表示负数，其他n-1位表示绝对值；</br>
>反码：原码符号位不变，其他位按位取反；</br>
>补码：反码加1；0的补码是唯一的；</br>
>移码：补码符号位取反，不区分正负数；</br>

* 数据类型字长、机器字长、操作系统字长的关系
>C/C++规定int字长和机器字长相同；</br>
>操作系统字长和机器字长未必一致,64位机器可以安装32位操作系统；</br>
>编译器根据操作系统字长来定义int字长；</br>
>char:1字节</br>
>short int:2字节</br>
>int:4字节</br>
>unsigned int:4字节</br>
>long:32位4字节；64位8字节</br>
>unsigned long:32位4字节；64位8字节</br>
>long long:8字节</br>
>float:4字节</br>
>double:8字节</br>
>*(指针):32位4字节；64位8字节，使用sizeof()输出指针的长度</br>
>boo:1字节，C语言没有bool,C++中加入的；</br>
>32位和64位操作系统中数据字长的区别：指针、long、unsigned long不同，其他相同</br>
>32位机的寻址空间是4个字节</br>
>signed int 等于int，long int 等于long;


* 指针运算
>指针加上整数、指针自增时指针在内存中移动的字节数，与指针类型有关；</br>
>char占一个字节,char指针加1，内存中就移动1字节，内存地址加1；</br>
>指向数组的指针，对其进行加或减，如果超过了数组的内存范围会出错吗？

* double和float的精度
>布尔表达式中尽量将浮点型使用大于小于比较，避免使用等号比较
* c语言中没有布尔型，判断真假用0或非0
>if判断表达式不要使用==判断是否相等</br>
>c语言没有bool值，==表达式返回值是什么

* ASCII码值
>0到9:48到57</br>
>A到Z:65到90</br>
>a到z:97到122</br>


声明一个数组时，编译器都做了哪些事情，数组存放在堆中还是存放在栈中
复杂数据结构的定义和使用举例：
***
### 第三章   运算符及其优先级 ###
* 分类
>算数运算：+、-、*、/、%、++、-- </br>
>关系运算：= 、<、>、<=、>=、!=</br>
>逻辑运算：&&、||、逻辑非 ！</br>
>位操作符：&、|、按位非 ~、^、<<、>></br>
>赋值、复合赋值：=、复合算术赋值+=,-=,*=,/=,%=、复合位运算赋值&=,|=,^=,>>=,<<=</br>
>条件运算：三目运算符（？：）</br>
>逗号：把若干表达式组合成一个表达式</br>
>指针运算：*、&</br>
>求字节：sizeof</br>
>其他：()、[]、.、-></br>

* 运算符结合性
>C语言中，运算符的运算优先级共分为15级。1级最高，15级最低。</br>
>在表达式中，优先级较高的先于优先级较低的进行运算。 </br>
>而在一个运算量两侧的运算符优先级相同时， 则按运算符的结合性所规定的结合方向处理。</br> 
>C语言中各运算符的结合性分为两种，即左结合性(自左至右)和右结合性(自右至左)。</br>
>例如算术运算符的结合性是自左至右，即先左后右。</br>
>如有表达式x-y+z则y应先与“-”号结合， 执行x-y运算，然后再执行+z的运算。</br>
>这种自左至右的结合方向就称为“左结合性”。而自右至左的结合方向称为“右结合性”。</br> 
>最典型的右结合性运算符是赋值运算符。如x=y=z,由于“=”的右结合性，应先执行y=z再执行x=(y=z)运算。</br>
> C语言运算符中有不少为右结合性，应注意区别，以避免理解错误。</br>
>运算符结合优先级举例

* 优先级举例

***
<h3 id='4'>第四章   流程控制</h3>
* 分支结构
>if else
>switch case default

* 循环结构
>while
>do while
>for

* 跳转
>return
>continue用于循环结构
>break
>goto

* 综合使用
***

### 第五章   数组、结构体、函数与指针 ###
* 数组与指针
>数组名可以直接给指针变量赋值，数组名可以看作指针，但不等同于指针</br>
>指针指向的是数组中的某个元素，而数组名代表的是整个数组</br>
>数组是存储在堆中，还是存储在栈中</br>
>一个指向结构体的指针代表的是结构体整体，为什么指向数组的指针就不是代表数组整体</br>
>指针是有类型的，与整数加减运算是根据类型来移动字节数的，如果直接去修改指针的值会出错吗</br>
>一个int型变量占4个字节，指向它的指针的值是这4个字节的首地址，如果让这个指针的值指向其中的第二个字节会怎么样</br>
>内存中的地址一定是四个字节为基本单位的吗</br>
>int *a[10] ：数组指针.数组a里存放的是10个int型指针</br>
>int (*a)[10] ：a是指针,指向一个数组.此数组有10个int型元素</br>
>int *a[10]</br>
>先找到声明符a,然后向右看,有[]说明a是个数组,再向左看,是int *,说明数组中的每个元素是int *.所以这是一个存放int指针的数组.</br>
>int(*a)[10]</br>
>先找到声明符a,被括号括着,先看括号内的(优先级高),然后向右看,没有,向左看,是*,说明s是个指针,什么指针?在看括号外面的,先向右看,有[] 是个数组,</br>
>说明a是个志向数组的指针,再向左看,是int,说明数组的每个元素是int.所以,这是一个指向存放int的数组的指针.</br>
>例</br>
>int *p[10];</br>
>int (*q)[10];</br>
>printf( "*p[10]:%d\n ",sizeof(p));</br>
>printf( "(*q)[10]:%d\n ",sizeof(q));</br>
>结果是：</br>
>*p[10]:40 //说明p是一个数组名</br>
>(*q)[10]:4 //说明q是一个指针</br>
>数组指针指向的是数组中的一个具体元素，而不是整个数组；数组名可以给指针变量赋值，可以看作是指针，指针可以自增，数组名可不可以自增呢？</br>
>答案是不能，容易迷惑的是函数接收一个数组为参数，函数中数组形参可以使用自增符</br>
>数组名可不可以加或减呢？答案是可以 , 例如 int a[]={1,2,3}    int b=*(a+1);  问题：*（a-1）或者*（a+4）访问内存是否会出错？</br>

* 结构体与指针
>结构体定义的两种形式
```c
//一般形式
struct st{
  int a;
  char b;
} st1,st2;
struct st st3;/*创建对象需要加上struct*/
//使用typedef
//结构体名不写在struct后面
typedef struct{
  int a;
  char b;
}st;
st st1,*stp;/*创建对象和指针不需要struct，比较方便*/
//链表结构体,包含上面两种形式
typedef struct Node{
    ElemType data;

    struct Node *next; 
} Node;
```
>结构体声明定义：注意，定义结构体时分号不能少</br>
>结构体和数组不同，数组名表示数组首地址是一个指针，二结构体变量名代表结构体本身</br>
>指向结构体的指针与结构体成员访问</br>
>p是指向结构体的指针：（*p）.XXX或p->XXX</br>
>a是结构体变量名：a.XXX</br>
>结构体变量名是否可以直接给结构体指针赋值,(*p)与a是什么关系</br>

* 函数与指针
```c
int sum(int a, int b)
{
  return a + b;
}

int (*fp)(int, int); //声明一个函数指针；
fp = &sum; //将sum函数地址赋值给fp；
(*fp)(1, 2); //通过函数指针调用函数；
```
>对于普通的函数，&符可以省略；c++中函数指针可以指向类成员函数；
* 指向指针的指针
```c
//指针可以有多级
int a = 100;
int *p1 = &a;
int **p2 = &p1;
int ***p3 = &p2;
//多级指针使用
int b = **p2;
```

* 与指针有关的定义
>用变量a给出下面定义</br>
>一个有10个指针的数组，该指针是指向一个整型数的；</br>
>一个指向有10个整型数数组的指针；</br>
>一个指向函数的指针，该函数有一个整型参数并返回一个整型数；</br>
>一个有10个指针的数组，该指针指向一个函数，该函数有一个整型参数并返回一个整型数；</br>
>int * a[10]; int (*a)[10];int (*a)(int);int (*a[10])(int)</br>

* 编译器会为每个函数的参数都复制一份临时副本：http://blog.csdn.net/stormwy/article/details/8070966

* 关于数组、结构体等是存放在栈中还是存放在堆中
>全局的数组、static修饰的数组存放在静态数据区；</br>
>局部的数组、函数参数数组存放在栈中</br>
>使用malloc动态分配的数组存放在堆中</br>
>return不能返回指向栈内存的指针，函数结束后栈就消失了；http://blog.csdn.net/zxc123e/article/details/6856121</br>
>结构体中使用数组：http://blog.csdn.net/yuanbinquan/article/details/48129627</br>
>结构体变量存放在栈中的情形，结构体作为参数时传递的是值还是引用；http://blog.csdn.net/lin37985/article/details/38582027</br>
>数组参数传递与引用传递相同,形参数组可以当作指针使用:http://blog.csdn.net/foreversober/article/details/45441685</br>
>数组在内存中的存在形式：http://bbs.csdn.net/topics/391002768?page=1</br>
>C语言与汇编的对应关系</br>
>使用调试工具观察堆栈变化情况</br>

>"."和[]运算符的级别比*高，如果r是一个指向结构体person的指针，通过r取结构体中的变量使用如下两种形式
(*r).name  或   r->name


C语言中的引用：用&声明，声明引用有什么用；与指针有什么区别；scanf()函数中为什么要用&；&即是取地址符又是按位与符
***

### 第六章   宏定义与条件编译 ###
* \#define宏
>字符串和表达式替换，注意表达式外面使用括号；</br>
>带参宏与普通函数区别
>带参宏的好处，普通函数要开辟内存空间，宏参数不必指明数据类型；
* \#include 预处理指令  
* \#ifndef #define #endif 防止头文件被重复包含
```c
//头文件名为abc.h
#ifndef _ABC_H
#define _ABC_H
...
#endif

```
* \#if #ifdef #else #endif条件编译

* 变量作用域

* 编译的各个阶段完成什么工作

* 手动编写makefile，CMake的使用
```c
/* filename:add.h */
extern int add(int i, int j); 
/* filename:add.c */
int add(int i, int j)
{
  return i + j;
}; 
/* filename:main.c */
#include "add.h"
main()
{
  int a, b;
  a = 2;
  b = 3;
  printf("the sum of a+b is %d", add(a + b));
};

/*怎样为上述三个文件产生makefile呢？如下：
-------------------------
test : main.o add.o
gcc main.o add.o -o test
 
main.o : main.c add.h
gcc -c main.c -o main.o
 
add.o : add.c add.h
gcc -c add.c -o add.o 
-----------------------*/
//(注意分割符为TAB键）
```
多文件编译https://my.oschina.net/u/3160411/blog/edit/draft/630161
动态链接与静态链接
源文件和其他资源文件是如何打包成一个软件的，c
***

### 第七章   标准库函数使用举例 ###
* 标准输入输出stdio.h
>FILE文件结构体
>fopen()打开文件；fclose()关闭文件
>fgetc();fputc();getc();putc();
>scanf();fscanf();

* 字符函数ctype.h
>isalpha()判断是否是字符
>issupper();islower()判断大小写
>isdigit();判断是否是数字

* 字符串函数库 string.h
>strlen()返回字符串长度
>strcpy()；strncpy()复制字符串
>strcat();strncat()
>strcmp();strncmp()字符串比较
>strchr();strrchr()字符串搜索

* 数学函数math.h
>sqrt();平方
>fabs();绝对值
>pow() 幂,double类型
>fmod();double类型
>sin();exp();log();指数、对数、三角函数

* 其他
>rand();srand();随机数
>calloc();realloc();malloc();free();引入 stdlib.h
>exit();abort();正常和非正常退出；

* 坐标与颜色（conio.h）
>颜色：textbackground()背景色  textcolor()文本色 cprintf()
>坐标：gotoxy()定位 clrscr()清屏


* 时间函数：time.h   
>time() ctime() asctime() 
>localtime() gmtime() clock()

* 图形绘制 graphics.h
>circle（） putpixel()画点 
>ellipse（）椭圆

* 文件的操作
>操作文件有两种方式，通过C语言的库函数，与平台无关，编译时会根据不同系统做不同处理
>通过Linux提供的API函数，这些API依赖Linux系统调用
>系统调用：防止进程访问该进程以外的内存，用寄存器对每个进程访问的内存空间进行现在
>又为了防止进程修改这两个寄存器，将处理器分为两种状态，内核态和用户态，进程的切换是在内核态完成的
>有些操作不能让普通程序随便使用，将其封装成系统调用提供给用户态程序，比如IO操作由用户态程序向内核发起，由内核完成；
>系统调用必须先通过软中断机制进入内核态；
***

### 第八章   常见数据结构 ###
>线性表顺序存储与数组有什么区别
```c
/*线性表功能的实现*/
#include<stdio.h>

//定义常量 存储空间的初始化分配
#define MAXSIZE 20
#define TRUE 1
#define ERROR -1
#define FALSE 0
#define OK 1

//用typedef定义类型
typedef int Status;
typedef int ElemType;
//定义一个结构体类型
typedef struct{
    ElemType data[MAXSIZE];
    int length;
} SqList; 

//初始化函数
Status initList(SqList *L){
    L->length = 0;
    return OK; 
} 

//返回线性表的长度
Status getListLength(SqList L){
    return L.length;
}

//线性表为空返回true,否则返回false
Status listEmpty(SqList L){
    if(L.length == 0){
        return TRUE; 
    }
    return FALSE;
} 

//线性表清空,长度为0 
Status clearList(SqList *L){
    L->length = 0; 
    return OK;
} 
//获取指定的元素的值,返回下标为i - 1的元素,赋值给e
Status getElem(SqList L, int i, ElemType *e){
    //判断元素位置是否合法[i]
    if(i > L.length || i < 1){
        printf("查找的位置不正确 \n");
        return ERROR; 
    }
    //判断线性表是否为空
    if(listEmpty(L)){
        return ERROR;
    } 
    *e = L.data[i - 1];
    return OK;
}

//在线性表中查找指定的e相等的元素,如果查找成功,返回该元素的下标,否则返回ERROR
Status locateElem(SqList L, ElemType e){
    int i;
    for(i = 0; i < L.length - 1; i++){
        if(L.data[i] == e){
            return i;
        }
    }
    printf("没有查找到元素 %d 指定的下标\n",e);
    return ERROR;
} 

//自动创建 MAXSIZE 个元素,并赋值为0 
Status createList(SqList *L){
    int i;
    for(i = 0; i < 10; i++){
        L->data[i] = 0;
    } 
    L->length = 10;
    return OK;
} 

//在线性表中第i个位置前插入新元素e 
Status listInsert(SqList *L, int i, ElemType e){
    //判断长度是否可以允许插入新的数据 
    if(L->length >= MAXSIZE){
        printf("空间已满,不能再插入数据\n");
        return FALSE; 
    }
    //判断插入位置的合法性
    if(i < 1 || i > L->length) {
        printf("插入位置不正确\n");
        return FALSE;
    }
    int j;
    for(j = L->length - 1; j >= i; j--){
        L->data[j] = L->data[j - 1];
    }
    L->data[i - 1] = e;
    L->length++;
    return TRUE;
}

//删除线性表中第i个元素,成功后表长减1,用e返回其值 
Status deleteList(SqList *L, int i, ElemType *e){
    //判断线性表是否为空
    if(listEmpty(*L)){
        return ERROR;
    }
    //判断删除的位置是否合法
    if(i < 1 || i > L->length) {
        printf("删除位置不合法\n");
        return ERROR;
    }
    *e = L->data[i - 1];
    for(i; i < L->length; i++){
        L->data[i - 1] = L->data[i];
    }
    L->length--;
    return TRUE;
} 

//遍历线性表
Status listTraverse(SqList L){
    int i;
    for(i = 0; i < L.length; i++){
        printf("%d ",L.data[i]);
    }
    printf("\n");
    return OK;
} 
```
>单链表
```c
//单链表存储结构 
#include<stdio.h>
#include<stdlib.h>
#define OK 1
#define ERROR 0

typedef int ElemType;
typedef int Status;

typedef struct Node{
    ElemType data;

    struct Node *next; 
} Node;
typedef struct Node *LinkList;

//获取链表的长度 
Status getListLength(LinkList L){
    int i = 0; //计数器
    while(L->next){
        L = L->next;
        i++;
    } 
    return i;
}

//单链表的读取,用e返回L中的第i个元素的值 , 0 < i < L.length
Status getElem(LinkList L, int i, ElemType *e){ 
    int j = 1;
    LinkList p; 
    p = L->next;    //p为第一个节点
    while(p && j < i){ //p不为null 
        p = p->next;
        j++; 
    }
    if(!p || i > j){
        return ERROR;   //查找的元素不存在 
    }
    *e = p->data;   //去第i个元素的数据
    return OK; 
} 

//单链表的创建,随机产生n个随机数,建立带头结点的单链表(头插法) 
Status createListHead(LinkList *L, int n){
    LinkList p;
    int i;
    srand(time(0)); //初始化随机种子
    *L = (LinkList)malloc(sizeof(Node)); //建立链表 
    (*L)->next = NULL;  //定义一个头结点 
    for(i = 0; i < n; i++){     //生成结点 
        p = (LinkList)malloc(sizeof(Node));
        p->data = rand() % 100 + 1; //产生100以内的数字 
        p->next = (*L)->next;   
        (*L)->next = p; //插入到表头     
    }   
    return OK;  
}

//单链表的创建,随机产生n个随机数,建立带头结点的单链表(未插法) 
Status cretateListTail(LinkList *L, int n){
    LinkList p, q;
    int i;
    srand(time(0));
    *L = (LinkList)malloc(sizeof(Node));    //建立一个新的链表 
    q = *L;
    for(i = 0; i < n; i++){
        p = (LinkList)malloc(sizeof(Node));//产生一个新的节点
        p->data = rand() % 100 + 1; //产生一个100以内的数字 
        q->next = p;    //新节点添加到链表的末尾 
        q = p;      //新节点定义为未节点 
    }
    q->next = NULL; //链表的最后一个元素指向null
    return OK; 
} 

//遍历单链表,输出值
void listTraverse(LinkList L){
    if(L->next == NULL){
        printf("链表为空");
    }else{
        LinkList p;
        p = L->next;
        while(p != NULL){
            printf("%d ",p->data);
            p = p->next;
        }
        printf("\n");   
    }
}

//链表的插入 将e插入到第i个位置之前 0 < i < listLenght + 1 
//定位到第i个节点,生成一个新的节点,数据e保存在新的节点中,最后插入到链表中 
Status listInsert(LinkList *L, int i, ElemType e) {
    int j = 1;
    LinkList p, s;
    p = *L; 
    while(p && j < i){ //p不为null 
        p = p->next;
        j++;
    }
    if(!p || i < j){    //查找失败
        return ERROR;
    }
    s = (LinkList)malloc(sizeof(Node)); //生成一个新的节点
    s->data = e;
    s->next = p->next;  //插入新节点 
    p->next = s; 
    return OK;
}

//链表删除 从链表中删除第i个元素,将删除的元素保存到e中 
Status ListDelete(LinkList *L, int i, ElemType *e){
    int j = 1;
    LinkList p, q; 
    p = *L;
    while(p && i > j){
        p = p->next;
        j++;
    }
    if(!p || j > i){
        return ERROR;   //查找失败 
    }
    q = p->next;
    *e = q->data;   //保存要删除的数据
    p->next = q->next;  //将q的后继赋值给p的后继
    free(q);    //释放空间 
    return OK; 
} 

//删除所有的节点
Status clearList(LinkList *L) {
    LinkList p, q;
    p = (*L)->next;
    while(p){       //循环删除每一个节点 
        q = p->next;
        free(p);
        p = q;
    }
    (*L)->next = NULL;  //头结点 
    return OK;
}
```
>双向链表
```c
```
>循环链表
```c
```
>树的相关概念</br>

>节点的度：节点拥有的子树个数</br>
>树的度：所有节点度的最大值</br>
>根节点：没有双亲的节点，二叉树的双亲节点就是父节点的意思</br>
>内部节点：度（子树个数）不为0，且有双亲的节点</br>
>叶子节点：度为0的节点</br>
>层次：根节点是第一层或第零层；根据具体问题而言</br>
>树的高度：树中节点的最大层次,</br>
>二叉数：每个节点最多有两个子树</br>
>森林：n棵互不相交的树的集合</br>
>树的存储结构：双亲表示法、孩子表示法、孩子兄弟表示法</br>
>二叉树相关概念</br>
>二叉树每个节点最多有两个子树</br>
>子节点为叶子节点就认为没有子树</br>
>斜树、左斜树、右斜树</br>
>满二叉树和完全二叉树</br>
>二叉树存储结构：顺序存储结构、二叉链表</br>
>二叉树遍历：前序、中序、后序、层序遍历</br>
```c
/*
    二叉树(binary tree) - 链式存储结构
    实现 二叉树的创建和遍历
    遍历和创建分为三种 前序,中序,后序 
    输入 数据参考 <AB D  C  > 空格是要输入 的 
*/

#include<stdio.h>
#include<stdlib.h>
#define OK 1
#define ERROR 0;

typedef int Status;
typedef char TElemType;

//结点定义
typedef struct BiTNode {
    TElemType data;     //数据域 
    struct BiTNode *lchild, *rchild;    //左右孩子指针 
}BiTNode, *BiTree;

//前序遍历(previous order traverse)
void preOrderTraverse (BiTree T){
    if(T == NULL){
        return;
    } 
    printf("%c ", T->data);         //第一步 显示结点数据
    preOrderTraverse(T->lchild);    //第二步 前序遍历左子树 
    preOrderTraverse(T->rchild);        //第三步 前序遍历右子树 
}

//中序遍历(intermediate order traverse)
void inOrderTraverse (BiTree T){
    if(T == NULL){
        return;
    } 
    inOrderTraverse(T->lchild); //第一步 中序遍历左子树 
    printf("%c ", T->data);     //第二步 显示结点数据
    inOrderTraverse(T->rchild); //第三步 中序遍历右子树 
}

//后序遍历(post order traverse)
void postOrderTraverse(BiTree T){
    if(T == NULL){
        return;
    }
    postOrderTraverse(T->lchild);
    postOrderTraverse(T->rchild);
    printf("%c ", T->data);
} 

//二叉树的建立  按前序输入二叉树中结点的值 (一个字符)
//' '表示空树 让每个结点确定是否有左右孩子,构造二叉链表表示二叉树 
//如果输入顺序按中序或后序 , 代码的66 67 68行顺序要换一下 ,可以参照遍历的代码这里就不实现了. 
void createBiTree(BiTree *T){
    TElemType e;
    scanf("%c",&e);
    if(e == ' '){
        *T = NULL;
    } 
    else{
        *T = (BiTree)malloc(sizeof(BiTNode));   //生成结点 
        if(!(*T)){  //创建失败 
            printf("结点申请失败\n"); 
            return; 
        }
        (*T)->data = e; //给结点赋值
        createBiTree(&(*T)->lchild); //构造左子树
        createBiTree(&(*T)->rchild);    //构造右子树 
    } 
}
```
>栈，栈可以有顺序和链式存储结构

```c
/*栈 顺序存储结构实现*/
#include<stdio.h>

//定义常量 存储空间的初始化分配
#define MAXSIZE 20
#define ERROR 0
#define OK 1

//用typedef定义类型
typedef int Status;
typedef int SElemType;
//定义一个结构体类型
typedef struct{
    SElemType data[MAXSIZE];
    int top;
} SqStack; 

//入栈 push, 将元素e为新的栈顶元素 
Status push(SqStack *s, SElemType e){
    // 判断栈是否满
    if(s->top == MAXSIZE - 1){
        return ERROR;
    } 
    s->top++;   //栈顶上移 
    s->data[s->top] = e;    //将新元素复制到栈顶空间
    return OK; 
} 

//出栈 pop 将要出栈的元素保存在e中 
Status pop(SqStack *s, SElemType *e){
    //判断栈是否为空 
    if(s->top == -1){
        return ERROR;
    } 
    *e = s->data[s->top];   //保存要出栈的元素 
    s->top--;   //栈顶下移 
    return OK; 
} 

//初始化
Status initStack(SqStack *s){
    s->top = -1;
    return OK;
} 

//输出栈中的所有元素
void stackTraverse(SqStack s) {
    if(s.top == -1){
        printf("栈中无元素\n");
    }
    else{
        while(s.top != -1){
            printf("%d ",s.data[s.top]);
            s.top--;
        } 
        printf("\n");
    }
}
```
>队列</br>
>串</br>
>二维数组与矩阵</br>
>哈希表与时间复杂度O(1)
```c
/*最常用的构造散列函数的方法是: 除留余数法
F(key) = key mod P (P <= M)
若散列表的长度是M, 通常p为小于或等于表长(最好接近于m)的最小质数,或不包含小于20质因子的合数.*/
//hash表的生成和查找 
//hash函数是 除留余数法
//冲突采用 开放定址法 线性探测 
#include<stdio.h>
#include<stdlib.h> 

#define ERROR 0
#define OK 1
#define HASHSIZE 12
#define NULLKEY -32768  //初始化的默认值 
#define arr_length(array) (sizeof(array) / (sizeof(array[0])))  //定义一个宏 求数组长度 

typedef int Status; 
typedef struct{
    int *elem;  //数据元素的存储基址 
    int count;  //当前数据元素的个数 
} HashTable;

int m = 0;  //散列表长度

//初始化 散列表
Status initHashTable(HashTable *H){
    int i;
    m = HASHSIZE;
    H->count = m;
    H->elem = (int *)malloc(m * sizeof(int));   //在堆中开辟空间 
    for(i = 0; i < m; i++){
        H->elem[i] = NULLKEY;   //初始化数据 
    }
    return OK;
}

//散列函数 计算散列地址 
int hash(int key){
    return key % m; //除留余数法 
} 

//插入关键字进散列表
void insertHash(HashTable *H, int key){
    int addr = hash(key);   //求散列地址
    while(H->elem[addr] != NULLKEY){    //冲突产生了. 
        addr = (addr + 1) % m;  //开放定址法 线性探测 
    } 
    H->elem[addr] = key;    //如果有空位插入关键字 
} 

//散列表查找关键字 用*addr返回 
Status searchHash(HashTable H, int key, int *addr) {
    *addr = hash(key);
    while(H.elem[*addr] != key){    //有冲突,向下查找 
        *addr = (*addr + 1) % m; 
        if(H.elem[*addr] == NULLKEY || *addr == hash(key)){ //循环回到原点 说明关键字不存在 
            printf("查找的关键字不存在\n");
            return ERROR; 
        }
    }
    return OK;
}

//遍历
void traverse(HashTable H, int len) {
    if(len <= 0){
        printf("长度不合法\n");
        return ;
    } 
    int i = 0;
    for(i; i < len; i++){
        printf("%d ", H.elem[i]);       
    }
    printf("\n");
}
```
>图

创建链表有多种方式，可以分为带头节点和不带头节点：http://www.cnblogs.com/plxx/p/3388098.html</br>

链表带头节点的好处是：链表中第一个数据的操作和其他节点相同，空链表和非空链表的处理相同</br>

 对void指针强转时：</br>

struct NODE{} Node *next; 可以使用(Node\*)也可以使用(next);Node=\*next  ,   Node\*=next</br>


链表的反向，链接，插入，删除等操作
* 二叉树
* 图
***

### 第九章   网络套接字 ###
>主要的函数</br>
>socket();bind();listen();connect();accept();read();write();close();</br>
>各函数参数的意义</br>
>一个简单的客户端、服务器代码示例</br>
>Linux和windows下使用的函数的区别</br>
>windows下如何编写和导入动态链接库；命令行使用-l参数链接库，或在工程中加入依赖库</br>
>如何使服务端一直监听端口，接收请求</br>
>fork多个线程去同时处理多个请求</br>
>tcp的三次握手发生在哪个阶段</br>
>tcp建立连接后数据的接收和发送路由都不变吗</br>
http://www.cnblogs.com/Leo_wl/p/5665705.html</br>
http://c.biancheng.net/cpp/socket/</br>
http://blog.csdn.net/gneveek/article/details/8699198</br>
***

### 第十章   常见问题与算法总结 ###
排序、插入、查找、逆序、因式分解、公约数公倍数、字符统计、阶乘、倒数和（精度问题）、方程、递归、二维数组操作
***
### 第十一 C语言中使用汇编语言 ###
***
### 其他问题 ###
- 声明与定义

> 举个例子：A)int i; B)extern int i;哪个是定义？哪个是声明？
> ***
> 什么是定义：所谓的定义就是(编译器)创建一个对象，为这个对象分配一块内存并给它取上一个名字，这个名字就是我们经常所说的变量名或对象名。
> 但注意，这个名字一旦和这块内存匹配起来，它们就同生共死，终生不离不弃。并且这块内存的位置也不能被改变。
> 一个变量或对象在一定的区域内（比如函数内，全局等）只能被定义一次，如果定义多次，编译器会提示你重复定义同一个变量或对象。
>***
> 什么是声明：有两重含义。如下：
>
>第一重含义：告诉编译器，这个名字已经匹配到一块内存上了，下面的代码用到变量或对象是在别的地方定义的。声明可以出现多次。
> 
>第二重含义：告诉编译器，我这个名字我先预定了，别的地方再也不能用它来作为变量名或对象名。 	比如你在图书馆自习室的某个座位上放了一本书，表明这个座位已经有人预订，别人再也不允许使用这个座位。
> 	其实这个时候你本人并没有坐在这个座位上。这种声明最典型的例子就是函数参数的声明，例如：void fun(int i, char c);
>***
>答案:A)是定义；B)是声明。定义声明最重要的区别：定义创建了对象并为这个对象分配了内存，声明没有分配内存。

- 关于内存分配：编译好的程序被载入内存的时候分为指令区和数据区，指令中包含操作数的地址，编译器在编译的时候是如何确定操作数的地址的？变量名是给编译器看的，不占内存?

- *号与[]的结合 *与.结合，++的结合

- 引用传递和值传递

>函数参数的传递。将指针，结构体，整型变量传递给函数时，什么时候是值传递，什么时候是引用传递？编译器为函数参数复制副本
>***
>值传递：(形式参数类型是基本数据类型)：方法调用时，实际参数把它的值传递给对应的形式参数，形式参数只是用实际参数的值初始化自己的存储单元内容，是两个不同的存储单元，所以方法执行中形式参数值的改变不影响实际参数的值。
>***
>引用传递：(形式参数类型是引用数据类型参数)：也称为传地址。方法调用时，实际参数是对象(或数组)，这时实际参数与形式参数指向同一个地址，在方法执行中，对形式参数的操作实际上就是对实际参数的操作，这个结果在方法结束后被保留了下来，所以方法执行中形式参数的改变将会影响实际参数。
>***
>总结：引用参数传入函数是，编译器也会为其复制副本，但是副本和原引用指向同一个内存地址，所有操作引用副本相当于操作原引用，
但是要注意不要使用malloc()函数将引用副本重新指向其他内存http://blog.csdn.net/stormwy/article/details/8070966。

- 动态内存分配与释放

>malloc()函数族
>free()释放内存后指针要置为NULL

- C99标准main()函数

>C99标准main函数写法
int main(void){return 0;}
int main(int argc,char* argv[]){return 0;}
main函数接收的参数是不是可以用作启动程序时传入的参数？比如shell命令后面的参数。
对char* argv[]的理解：
char* argv[]是存放指针的数组
例如：
char a[]="123";
char b[]="456";
char* argv[]={a,b};
argv[] 是数组，其中每个元素的大小是**一个字节**
指针的大小与指针的类型有关吗？与CPU位数有关吗？使用sizeof输出不同类型指针的大小：
例如：char a[]是字符数组，int a[]是整数数组
注意：C语言中"acb"表示字符数组
char *name;
name="tom";
在C语言中保存字符串一般使用上面这种方式
也可以使用char name[]="abc"保存字符串，但是需要单个单个字符去取
http://www.cnblogs.com/afarmer/archive/2011/05/05/2038201.html

- 为什么scanf中使用&符，printf中不使用

> 因为C函数的参数是传值的，只能往里传数据。而scanf需要从函数内读出数据，因此参数就设计指针形式。
>输出的时候使用变量名，输入时需要传入变量的地址，应该从编译角度来看
变量名，取地址都是在编译时才有用的
因为语法格式要求此处是变量地址

- 内存地址

> 内存地址怎么表示，指令分为操作码和操作数，操作数是由地址给出的，指令中的内存地址是什么
>
>内存地址实际上是一种偏移量，存储于段寄存器中。内存地址只是一种抽象，不是真正的物理内存地址，而是逻辑地址。由逻辑地址寻找到物理地址需要经过 逻辑地址->线性地址->物理地址 转换过程，而这些过程都是基于寄存器完成的。地址是16进制，关于计算机如何识别16进制，甚至关于内存地址更详细的知识，题主可以通过看相关书籍（比如CSAPP，操作系统相关的书籍，了解操作系统如何进行内存映射）进一步深入了解。

- 进程库、进程间通信
- 本地进程的通信方式

- segmentation fault (core dumped)
>程序执行时报错，段错误，一般时操作指针不当引起的，但编译时不会报错
>使用数组给指针赋值，然后使用指针名加数组下标的方式访问数组中元素，下标越界不会造成编译错误，运行时不一定会出错
