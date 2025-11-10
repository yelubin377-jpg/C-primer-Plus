# 西邮 Linux 兴趣小组 2024 纳新面试题
学长寄语：长期以来，西邮 Linux 兴趣小组的面试题以难度之高名扬西邮校内。我们作为出题人也清楚的知道这份试题略有难度。请你动手敲一敲代码。别担心，若有同学能完成一半的题目，就已经十分优秀。其次，相比于题目的答案，我们对你的思路和过程更感兴趣，或许你的答案略有瑕疵，但你正确的思路和对知识的理解足以为你赢得绝大多数的分数。最后，做题的过程也是学习和成长的过程，相信本试题对你更加熟悉地掌握 C 语言一定有所帮助。祝你好运。我们东区逸夫楼 FZ103 见！

本题目只作为西邮 Linux 兴趣小组 2024 纳新面试的有限参考。
为节省版面，本试题的程序源码省去了 #include 指令。
本试题中的程序源码仅用于考察 C 语言基础，不应当作为 C 语言「代码风格」的范例。
所有题目编译并运行于 x86_64 GNU/Linux 环境。

## 0. 聪明的吗喽

一个小猴子边上有 100 根香蕉，它要走过 50 米才能到家，每次它最多搬 50 根香蕉，（多了就拿不动了），它每走 1 米就要吃掉一根，请问它最多能把多少根香蕉搬到家里。

（提示：他可以把香蕉放下往返走，但是必须保证它每走一米都能有香蕉吃。也可以走到 n 米时，放下一些香蕉，拿着 n 根香蕉走回去重新搬 50 根。）

---

题解
  阶段1：
起点共100根，需分2次搬运（每次50根），第1次往返消耗 2x 根，第2次单程消耗 x 根（无需返回）。
中转点A剩余香蕉： 100 - (2x + x) = 100 - 3x 。
关键：需让中转点A的香蕉≤50根（避免后续仍需分2次搬运），即 100 - 3x ≤ 50 ，解得 x ≥ 16.67 米。
取整数 x = 17 米（若取16米，剩余 100 - 48 = 52 根，仍需分2次，多消耗往返）：
实际消耗： 3×17 = 51 根，中转点A剩余 100 - 51 = 49 根（≤50根，符合要求）。

  阶段2：
从中转点A（17米）到终点（50米）
距离： 50 - 17 = 33 米，仅需单程运输，消耗33根。
终点剩余： 49 - 33 = 16 根。

---



## 1. 西邮Linux欢迎你啊

  请解释以下代码的运行结果。

  

  ```c
  int main() {
      unsigned int a = 2024;
      for (; a >= 0; a--)
          printf("%d\n", printf("Hi guys! Join Linux - 2%d", printf("")));
      return 0;
  }
  ```


---

题解：a是一个非负整形变量，for循环规定a>=0时，
 输出三个嵌套printf（最里面输出0，外一层输出Hi guys! Join Linux - 20
 在向外一层，因为24个字符，故输出Hi guys! Join Linux - 2024）

---

## 2. 眼见不一定为实

  输出为什么和想象中不太一样？

  你了解 `sizeof()` 和 `strlen()` 吗？他们的区别是什么？

  

  ```c
  int main() {
      char p0[] = "I love Linux";
      const char *p1 = "I love Linux\0Group";
      char p2[] = "I love Linux\0";
      printf("%d\n%d\n", strcmp(p0, p1), strcmp(p0, p2));
      printf("%d\n%d\n", sizeof(p0) == sizeof(p1), strlen(p0) == strlen(p1));
      return 0;
  }
  ```

---

题解：sizeof()与strlen()的区别有：
 1.sizeof()会读取字符串中的\0，而strlen不会读取\0；
 2.本质不同：sizeof是关键字或运算符（编译时计算），strlen是函数（运行时计算）
 3.sizeof计算的是字节数，strlen计算的是字符数。
 4.适用范围不同：sizeof适用于所有类型（数组、指针、结构体等）strlen仅适用于以\0结尾的字符串（char*/char数组）
strcmp函数比较首字母的ASCII值，倘若前大于后，则输出一个正数，若相等，则输出0继续比较下一位，若小于，则输出一个负数。
在\0前，p0，p1，p2的字符串相等，输出0，而p1是指针，故sizeof（p1）是4或8，与sizeof（p0）和sizeof（p2）不等
其次，strlen(p0)与strlen(p1)在\0前字符数量相等，
故最终输出：
0
0
0
1

---

## 3. 1.1 - 1.0 != 0.1

为什么会这样，除了下面给出的一种方法，还有什么方法可以避免这个问题？



```c
int main() {
    float a = 1.0, b = 1.1, ex = 0.1;
    printf("b - a == ex is %s\n", (b - a == ex) ? "true" : "false");
    int A = a * 10, B = b * 10, EX = ex * 10;
    printf("B - A == EX is %s\n", (B - A == EX) ? "true" : "false");
}
```

题解：
因为二进制无法完美存储1.0，1.1，0.1这三个数（无法精确表示为2的多少次方），存储时会有误差，估计算下来不相等。
而乘以10以后，都可以被二进制精确存储，所以计算正确。
避免方法：高精度计算
最终输出：b - a == ex is false
          B - A == EX is true

---



## 4. 听说爱用位运算的人技术都不太差

解释函数的原理，并分析使用位运算求平均值的优缺点。



```c
int average(int nums[], int start, int end) {
    if (start == end)
        return nums[start];
    int mid = (start + end) / 2;
    int leftAvg = average(nums, start, mid);
    int rightAvg = average(nums, mid + 1, end);
    return (leftAvg & rightAvg) + ((leftAvg ^ rightAvg) >> 1);
}
```


题解：设置一个函数，并命名一个整型数组以及数组的首位下标和数组的最后一位下标。
如果该数组只有一个元素，那么进入if语句，直接返回。
设置一个mid变量，拆分中点（不断对半分，知道剩下一个元素）
对于return (leftAvg & rightAvg) + ((leftAvg ^ rightAvg) >> 1)原理：
   相同位部分（a & b）：二进制中a和b都为1的位，对总和的贡献是2×bit（因为a和b各有一个1），平均后为bit（即直接保留a&b）。
   不同位部分（a ^ b）：二进制中a和b不同的位（一个为1，一个为0），对总和的贡献是1×bit，平均后为bit >> 1（右移1位等价于除以2）。
举例：
若a=3（二进制011）、b=5（101）：
a & b = 001（1），a ^ b = 110（6），6 >> 1 = 3，总和1 + 3 = 4，等价于(3 + 5) / 2 = 4。
若a=2（010）、b = 3（011）：
a & b = 010（2），a ^ b = 001（1），1 >> 1 = 0，总和2 + 0 = 2，等价于(2 + 3) / 2 = 2（向下取整）。

---


## 5. 全局还是局部!!!

先思考输出是什么，再动动小手运行下代码，看跟自己想得结果一样不一样 >-<



```C
int i = 1;
static int j = 15;
int func() {
    int i = 10;
    if (i > 5) i++;
    printf("i = %d, j = %d\n", i, j);
    return i % j;
}
int main() {
    int a = func();
    printf("a = %d\n", a);
    printf("i = %d, j = %d\n", i, j);
    return 0;
}
```

---


题解：首先明确，全局变量的生命周期在整串代码中可用，而局部变量在除了作用域后生命周期结束。
此外，当在局部中全局变量与局部变量冲突时，以局部变量为准
还有，static定义的变量其他文件无法调用，而且仅仅只会初始化一次，后续不在初始化。
从main函数开始，进入func函数，此时局部变量优先所以i=10，进入if语句，i=11，输出i=11,j=15。
退出函数后，局部变量失效，i变为1，j为15
故最终输出：i = 11, j = 15
            a = 11
            i = 1, j = 15

---


## 6. 指针的修罗场：改还是不改，这是个问题

指出以下代码中存在的问题，并帮粗心的学长改正问题。



```C
int main(int argc, char **argv) {
    int a = 1, b = 2;
    const int *p = &a;
    int * const q = &b;
    *p = 3, q = &a;
    const int * const r = &a;
    *r = 4, r = &b;
    return 0;
}
```

---


题解：
首先明确：语法形式    名称        含义                                                                    口诀
        const int* p    常量指针    指针p指向的内容（* p）是const，不能通过p修改内容；但p可以指向其他地址。    const修饰* p（内容）
        int* const q    指针常量    指针q本身是const，不能修改q的指向；但可以通过q修改指向的内容。            const修饰q（指针）
   const int* const r    不可变指针    既不能修改r的指向，也不能通过r修改内容。                                const修饰两者
所以修改后的代码：
int main(int argc, char** argv) {
int a = 1, b = 2;
const int* p = &a;
int* const q = &b;
*q = 3;
p = &b;
const int* const r = &a;
return 0;
}


---



## 7. 物极必反？

你了解 `argc` 和 `argv` 吗，这个程序里的 `argc` 和 `argv` 是什么？

程序输出是什么？解释一下为什么。



```C
int main(int argc, char *argv[]) {
    while (argc++ > 0);
    int a = 1, b = argc, c = 0;
    if (--a || b++ && c--)
        for (int i = 0; argv[i] != NULL; i++)
            printf("argv[%d] = %s\n", i, argv[i]);
    printf("a = %d, b = %d, c = %d\n", a, b, c);
    return 0;
}
```

---


题解：argc指的是命令行的参数数量  argv是一个指向字符串的数组，存储具体的命令行参数。
明确逻辑运算符的优先级：&& > ||
在while循环中argc无限自增，直到溢出，变为-2147483647（因为argc先使用后自增）
又因为--a后a=0，b+1后变为-2147483646，c--后变为c=-1，所以if语句为假，不执行
最终输出：a = 0, b = -2147483646, c = -1


---


##  8.指针？数组？数组指针？指针数组？

在主函数中定义如下变量：



```C
int main() {
    int a[2] = {4, 8};
    int(*b)[2] = &a;
    int *c[2] = {a, a + 1};
    return 0;
}
```

说说这些输出分别是什么？



```C
a, a + 1, &a, &a + 1, *(a + 1), sizeof(a), sizeof(&a)
*b, *b + 1, b, b + 1, *(*b + 1), sizeof(*b), sizeof(b)
c, c + 1, &c, &c + 1, **(c + 1), sizeof(c), sizeof(&c)
```

---

题解:
int main() 
 {
int a[2] = { 4, 8 };       数组a：2个int元素，值为4、8
int(*b)[2] = &a;           数组指针b：指向数组a的地址
int* c[2] = { a, a + 1 };  指针数组c：存储2个int指针，分别指向a[0]、a[1]
return 0;
}
a, a + 1, & a, & a + 1, * (a + 1), sizeof(a), sizeof(&a)；
--a（a[0]的地址，类型衰减为int*），a+1（a[1]的地址，类型为int*），&a（与a的地址相同，但类型为int(*)[2]），&a+1（下一个数组的起始地址），*(a+1)值8（a[1]的内容），8，4或8。

* b, * b + 1, b, b + 1, * (*b + 1), sizeof(*b), sizeof(b)
--*b（a[0]的地址，与a的衰减结果一致，类型为int[2]衰减为int*），*b+1（a[1]的地址,类型为int*）,
--b（指向整个数组a的地址，与&a相同，类型为int(*)[2]），b+1（下一个数组的起始地址，类型为int(*)[2]），* (*b + 1)值为8（a[1]的内容），8（整个数组大小），4或8。
c, c + 1, & c, & c + 1, ** (c + 1), sizeof(c), sizeof(&c)
--c（c[0]的地址，c[0]存储的是a的地址，类型衰退为int**），c+1（c[1]的地址，c[1]存储的是a+1的地址，类型为int**），&c（类型：int*(*)[2]（指向整个指针数组c的指针）与c的地址相同，但类型是数组指针）
--&c+1（类型为：int*(*)[2]（下一个指针数组的起始地址））， ** (c + 1)值为a[1]=8，sizeof(c)值为整个数组的大小（2个int*元素，值为8），sizeof(&c)（&c是指向指针数组的数组指针（int*(*)[2]），值为4）


---



## 9. 嘻嘻哈哈，好玩好玩

在宏的魔法下，数字与文字交织，猜猜结果是什么？



```C
#define SQUARE(x) x *x
#define MAX(a, b) (a > b) ? a : b;
#define PRINT(x) printf("嘻嘻，结果你猜对了吗，包%d滴\n", x);
#define CONCAT(a, b) a##b

int main() {
    int CONCAT(x, 1) = 5;
    int CONCAT(y, 2) = 3;
    int max = MAX(SQUARE(x1 + 1), SQUARE(y2))
    PRINT(max)
    return 0;
}
```

---



题解：首先明确
CONCAT(a,b) = a##b            连接两个参数为一个标识符（无空格）    ##是“连接符”，直接拼接文本
SQUARE(x) = x * x                计算“x的平方”（但无括号，有陷阱）    仅替换文本，不处理运算符优先级
MAX(a, b) = (a > b) ? a : b;    取a、b的较大值（注意末尾有分号）    三目运算符，替换后会带分号
PRINT(x)                        打印带格式的字符串                    直接替换x为参数值

CONCAT(x, 1) → 连接x和1 → x1；
CONCAT(y, 2) → 连接y和2 → y2。
x1 = 5; y2 = 3;  
先处理SQUARE的替换（无括号的陷阱！）
SQUARE(x1 + 1) → 替换为x1 + 1 * x1 + 1（不是(x1 + 1) * (x1 + 1)！）；
代入x1 = 5 → 5 + 1 * 5 + 1 = 5 + 5 + 1 = 11。
SQUARE(y2) → 替换为y2 * y2；
代入y2 = 3 → 3 * 3 = 9。
再处理MAX的替换（注意末尾分号）：
MAX(11, 9) → 替换为(11 > 9) ? 11 : 9; （结果为11）。
int max = (11 > 9) ? 11 : 9;
PRINT(max) → 替换为printf("嘻嘻，结果你猜对了吗，包%d滴\n", max); ；
代入max = 11
最终输出结果为：嘻嘻，结果你猜对了吗，包11滴

---


## 10. 我写的排序最快

写一个 `your_sort` 函数，要求不能改动 `main` 函数里的代码，对 `arr1` 和 `arr2` 两个数组进行升序排序并剔除相同元素，最后将排序结果放入 `result` 结构体中。



```C
int main() {
    int arr1[] = {2, 3, 1, 3, 2, 4, 6, 7, 9, 2, 10};
    int arr2[] = {2, 1, 4, 3, 9, 6, 8};
    int len1 = sizeof(arr1) / sizeof(arr1[0]);
    int len2 = sizeof(arr2) / sizeof(arr2[0]);

    result result;
    your_sort(arr1, len1, arr2, len2, &result);
    for (int i = 0; i < result.len; i++) {
        printf("%d ", result.arr[i]);
    }
    free(result.arr);
    return 0;
}
```

---



题解：
                         定义result结构体（必须保留，与main函数兼容）
                         typedef struct 
                         {
                               int* arr;    结果数组（动态分配）
                               int len;     结果长度
                         } result;

```C
       升序排序的比较函数（qsort用）
      int cmp(const void* a, const void* b) 
      {
          return *(int*)a - *(int*)b;
      }

       your_sort核心函数
      void your_sort(int arr1[], int len1, int arr2[], int len2, result* res) 
      {
      1. 合并两个数组到临时空间（避免修改原数组）
         int total_len = len1 + len2;
         int* temp = (int*)malloc(total_len * sizeof(int));   直接分配
         memcpy(temp, arr1, len1 * sizeof(int));        复制arr1
         memcpy(temp + len1, arr2, len2 * sizeof(int)); 复制arr2到尾部

      2. 快速排序（qsort是标准库高效排序）
         qsort(temp, total_len, sizeof(int), cmp);

      3. 统计不重复元素的数量（排序后重复元素连续）
         int unique_len = (total_len == 0) ? 0 : 1;  至少1个元素
         for (int i = 1; i < total_len; i++) 
         {
             if (temp[i] != temp[i - 1]) unique_len++;
         }

      4. 复制不重复元素到结果结构体
         res->arr = (int*)malloc(unique_len * sizeof(int));   直接分配
         res->len = unique_len;
         if (unique_len > 0) 
         {
            res->arr[0] = temp[0];   第一个元素
            int j = 1;
            for (int i = 1; i < total_len; i++) 
            {
               if (temp[i] != temp[i - 1]) 
               {
                  res->arr[j++] = temp[i];  复制不重复元素
               }
            }
         }

      5. 释放临时空间（避免内存泄漏）
                    free(temp);
      }
```

 原题main函数（完全不变）
int main() 
{
    int arr1[] = { 2, 3, 1, 3, 2, 4, 6, 7, 9, 2, 10 };
    int arr2[] = { 2, 1, 4, 3, 9, 6, 8 };
    int len1 = sizeof(arr1) / sizeof(arr1[0]);
    int len2 = sizeof(arr2) / sizeof(arr2[0]);

​    result result;
​    your_sort(arr1, len1, arr2, len2, &result);
​    for (int i = 0; i < result.len; i++) 
​    {
​        printf("%d ", result.arr[i]);
​    }
​    free(result.arr);  释放结果数组（必须保留）
​    return 0;
}


---





## 11.猜猜我是谁

在指针的迷宫中，五个数字化身为神秘的符号，等待被逐一揭示。



```C
int main() {
    void *a[] = {(void *)1, (void *)2, (void *)3, (void *)4, (void *)5};
    printf("%d\n", *((char *)a + 1));
    printf("%d\n", *(int *)(char *)a + 1);
    printf("%d\n", *((int *)a + 2));
    printf("%lld\n", *((long long *)a + 3));
    printf("%d\n", *((short *)a + 4));
    return 0;
}
```

---

题解：
假设数组首地址为 0x1000，a[0] 存储(void*)1，其内存内容为：

地址	                    0x1000    0x1001       0x1002        0x1003
内容（十六进制）     01	     00	       00	         00
void* 指针占 4字节，1 的十六进制值为 0x00000001，按小端存储为 01 00 00 00。
a[0] 的完整内存范围是 0x1000~0x1003。

一、表达式： * ((char*)a + 1)
执行步骤如下：

1. (char*)a：将数组首地址转为 char*
	a 是 void* 指针数组的首地址（0x1000）。
	强制转换为 char* 后，指针类型变为 “指向1字节的char”，但 地址仍为 0x1000。
	步长：char * 指针每次加减的步长为 1字节。
2. + 1：指针偏移
		(char*)a 是 0x1000， + 1 后地址变为 0x1000 + 1×1 = 0x1001。
		此时指针指向 a[0] 的 第2个字节（地址 0x1001）。
3. * ：解引用取值
		解引用 char* 指针（地址 0x1001），取 1字节 的值。
		0x1001 的内容是 0x00（见内存布局表）。
4. 输出结果
	最终值为 0（十进制）。

二、表达式：*(int*)(char*)a + 1
(char*)a转为char* （地址0x1000）。
再转为int* （地址0x1000），解引用取a[0]的前4字节，值为1。

+ 1后结果为1 + 1 = 2。
	结果：2。

三、表达式：*((int*)a + 2)
(int*)a转为int*(地址0x1000,步长变为4)
+2:向右偏移8个字节,变为0x1008，指向a[1]的首地址（a[1]的内容是(void*)2
*：解引用int*指针，02 00 00 00 00 00 00 00（十进制）
结果：2

四、表达式： *((long long*)a + 3))
64位系统（void*占8字节），此时：
(long long*)a：转为long long* （步长8字节，与void* 步长一致）；

+ 3：指针偏移3×8 = 24字节，指向a[3]的首地址（0x1000 + 24 = 0x1018，a[3]的内容是(void*)4）；

* ：解引用long long* 指针，取8字节→04 00 00 00 00 00 00 00（十进制4）。
	结果：4

五、表达式：*((short*)a + 4)
(short*)a转为short*(地址为0x1000，步长变为2)
+4：指针偏移2*4=8个字节，指向a[1]的首地址
同第三个表达式
最终结果为2

故最终输出：
0
2
2
4
2



---

## 12. 结构体变小写奇遇

计算出 `Node` 结构体的大小，并解释以下代码的运行结果。



```c
union data {
    int a;
    double b;
    short c;
};
typedef struct node {
    long long a;
    union data b;
    void (*change)( struct node *n);
    char string[0];
} Node;
void func(Node *node) {
    for (size_t i = 0; node->string[i] != '\0'; i++)
        node->string[i] = tolower(node->string[i]);
}

int main() {
    const char *s = "WELCOME TO XIYOULINUX_GROUP!";
    Node *P = (Node *)malloc(sizeof(Node) + (strlen(s) + 1) * sizeof(char));
    strcpy(P->string, s);
    P->change = func;
    P->change(P);
    printf("%s\n", P->string);
    return 0;
}
```

---

题解：

1. 联合体大小计算
	union data {
	 int a;               //4字节
	 double b;            //8字节
	 short c;             //2字节
	};//取最大为内存，故该联合体大小为8字节
	2.结构体大小计算
	typedef struct node {
	 long long a;       // 8字节（64位系统）
	 union data b;      // 8字节（联合体大小由最大成员double决定）
	 void (*change)();  // 8字节（函数指针）
	 char string[0];    // 柔性数组（不占空间）
	} Node;
	成员对齐规则（64位系统）：
	long long a  对齐到  8字节。
	union data b 对齐到  8字节（因为最大成员是double）。
	void (*change)() 对齐到 8字节。
	 总大小计算：
	 long long a 占 8字节。
	 union data b 占 8字节（无需填充）。
	 void (*change)() 占 8字节。
	 总计：8 + 8 + 8 = 24字节。
	3.代码运行结果解析
	 内存分配：
	 Node * P = (Node*)malloc(sizeof(Node) + (strlen(s) + 1) * sizeof(char));
	分配空间包括 Node 结构体（24字节）和柔性数组 string（存储字符串 "WELCOME TO XIYOULINUX_GROUP!" 及其终止符）。
	数据初始化：

strcpy(P->string, s);    // 将字符串复制到柔性数组
P->change = func;        // 函数指针指向 func
函数调用：

P->change(P);            // 调用 func(P)
func 遍历 string，将每个字符转为小写：
for (size_t i = 0; node->string[i] != '\0'; i++)
node->string[i] = tolower(node->string[i]);
输出结果：
printf("%s\n", P->string); // 输出全小写字符串
输出结果：
welcome to xiyoulinux_group!


---



## 13. GNU/Linux (选做)

注：嘿！你或许对Linux命令不是很熟悉，甚至没听说过Linux。
但别担心，这是选做题，了解Linux是加分项，不了解也不扣分哦！

- 你知道 `ls` 命令的用法与 `/` `.` `~` 这些符号的含义吗？
- 你知道 Linux 中权限 `rwx` 的含义吗？
- 请问你还懂得哪些与 GNU/Linux 相关的知识呢~

---

题解：

一、`ls` 命令及路径符号 `/`、`.`、`~`

#### **1. `ls` 命令**

`ls` 用于**列出目录内容**（list）。

常用用法：

| 命令       | 含义                                                 |
| ---------- | ---------------------------------------------------- |
| `ls`       | 列出当前目录下的文件和文件夹                         |
| `ls -l`    | 以详细列表形式显示（包括权限、所有者、大小、时间等） |
| `ls -a`    | 显示所有文件，包括以`.`开头的隐藏文件                |
| `ls -lh`   | 以人类可读的方式显示大小（如 1K、2M）                |
| `ls /home` | 查看指定目录 `/home` 的内容                          |

------

#### **2. 路径符号**

| 符号 | 含义                         | 示例                                   |
| ---- | ---------------------------- | -------------------------------------- |
| `/`  | 根目录（整个系统的起点）     | `/etc/passwd`、`/home/user`            |
| `.`  | 当前目录                     | `./a.out` 表示当前目录下的 `a.out`     |
| `..` | 上一级目录                   | `cd ..` 返回上一级                     |
| `~`  | 当前用户的主目录（home目录） | `cd ~` 或 `cd` 都会回到 `/home/用户名` |

------

### 二、文件权限 `rwx`

在 Linux 中，每个文件或目录都有三类访问者：

1. **u（user）**：文件所有者
2. **g（group）**：同组用户
3. **o（others）**：其他用户

每类访问者有三种权限：

| 符号 | 含义    | 说明                                |
| ---- | ------- | ----------------------------------- |
| `r`  | read    | 读取文件内容或查看目录              |
| `w`  | write   | 修改文件内容或在目录中创建/删除文件 |
| `x`  | execute | 执行文件或进入目录                  |

例如：

```
-rwxr-xr--
```

意思是：

- 文件所有者有 `rwx`（读写执行）
- 所属组有 `r-x`（读和执行）
- 其他用户有 `r--`（只能读）

修改权限可用命令：

```
chmod 755 file
```

→ 表示权限为 `rwxr-xr-x`。

------

### 三、其他 GNU/Linux 基础知识

一些常见命令与概念：

| 命令                    | 功能                         |
| ----------------------- | ---------------------------- |
| `cd`                    | 切换目录                     |
| `pwd`                   | 显示当前工作目录             |
| `cp` / `mv` / `rm`      | 复制 / 移动 / 删除文件       |
| `cat` / `less` / `head` | 查看文件内容                 |
| `touch`                 | 创建空文件                   |
| `mkdir` / `rmdir`       | 创建 / 删除目录              |
| `man <命令>`            | 查看命令帮助（manual）       |
| `grep`                  | 搜索文本内容                 |
| `sudo`                  | 以管理员（root）权限执行命令 |
| `apt` 或 `dnf`          | 软件包管理工具（安装软件）   |

---


结语

🎉 恭喜你成功完成了所有挑战！\(^▽^)/！这是一项了不起的成就。👏
无论结果如何，相信这个过程已经让你对 C 语言和 Linux 有了更深入的了解。
记住，编程是一个持续学习的过程。
唯有脚踏实地，笃行不怠，方能拨云雾而见青天！

---
