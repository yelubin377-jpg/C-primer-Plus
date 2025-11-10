# C Primer Plus部分题解

#include <stdio.h>
#include <stdlib.h>
#include <ctype.h> 
#include <string.h>
#include <time.h>

## 4.1

```C
int main()
{
    printf("清输入您的名:");
    char a[20] = {0};
    scanf("%s",a);
    char b[20] = {0};
    printf("清输入您的姓:");scanf("%s",b);
    printf("%s.%s",a,b);
    return 0;
}
```



## 4.2

```C
int main()
{
    printf("请输入您的名字:");
    char a[20]={0};
    scanf("%s",a);
    printf("\"%s\"\n",a);
    printf("\"%20s\"\n",a);
    printf("\"%-20s\"\n",a);
    int x = strlen(a)+3; 
    printf("%*s\n",x,a);
    return 0; 
}
```



## 4.3

```C
int main()
{
    printf("清输入一个浮点数");
    float num;
    scanf("%f",&num);
    printf("The input is %.1f or %.1e.\n",num,num);
    printf("The input is %.3f or %.3E.\n ",num,num);
    return 0;
}
```



## 5.1

```C
int main()
{
    int a=1;
    const int h = 60;
    while(a>0)
  {
    printf("请输入分钟数:");
    scanf("%d",&a);
    int b = a / h;
    int c = a - h*b;
    printf("\n%d小时%d分钟\n",b,c);
  }
}


```



## 5.2

```C
int main()
{
    int a = 0;
    printf("清输入一个数：");
    scanf("%d",&a);
    for(int i = a;i<=a+10;i++)
    {
        printf("%d ",i);
    }
}
```



## 5.3

```C
int main()
{

    int a = 1;

   while(a>0)
   { 
    printf("输入天数：");
    scanf("%d",&a);
    const int x = 7;
    int b = a / x;//周
    int c = a - 7*b;//天
    printf("%d days are %d weeks,%d days.\n",a,b,c);
   }
}


```



# 6.1

```C
int main()
{
    char a[27] = {0};
    char b;
    printf("请输入26个小写字母:\n");
    for(int i = 0;i<26;i++)
    {
        scanf(" %c",&b);
        a[i] = b;
    }
    for(int i = 0;i<26;i++)
    {
        printf("%c ",a[i]);
    }
    return 0;



}
```




## 6.2

```C
int main()
{

        for(int j = 1;j<=5;j++)
        {
            int g = 0;
            while(g!=j)
            {
                printf("$");
                g++;
            }
            printf("\n");
        }

}
```



## 6.3

```C
int main()
{
    for(int i = 0;i<6;i++)
    {
        char a = {'F'};
        int num = 0;
        for(int j = 0;j<=i;j++)
        {
            printf("%c",a-num);
            num++;
        }
        printf("\n");
    }
}
```



## 7.1

```C
int main()
{
    printf("请输入一串字符:");
    char a[1000000] = {0};
    fgets(a,sizeof(a),stdin);
    int b = 0;//空格数
    int c = 0;//换行符数
    int d = 0;//其他字符数量
    for(int i = 0;i<1000000;i++)
    {
        if(a[i]==' ')
        {
            b++;
        }
        else if(a[i]=='\\'&&a[i+1]=='n')
        {
            c++;
            d--;
        }
        else if(a[i]=='#')
        {
            break;
        }
        else
        {
            d++;
        }
    }
    printf("空格的数量：%d\n",b);
    printf("换行符的数量：%d\n",c);
    printf("其他字符的数量：%d\n",d);
}


```



## 7.2

```C
int main()
{
    printf("请输入一串字符:");
    char a[1000000] = {0};
    fgets(a,sizeof(a),stdin);
    int b = 0;
    for(int i = 0;i<1000000;i++)
    {
        if(a[i]=='#')
        {
            break;
        }
        else
        {
            b++;
        }
    }
    int c = 0;
    for(int i = 0;i<b;i++)
    {
        printf("%c-%d ",a[i],a[i]);
        c++;
        if(c%8==0&&c!=0)
        {
            printf("\n");
        }
    }
    return 0;
}


```



## 7.3

```C
int main()
{
    printf("请输入一段数字（不带空格）");
    char a[1000000] = {0};
    int odd = 0;//奇数
    int even = 0;//偶数
    int evencount = 0;//偶数个数
    int oddcount = 0;//奇数个数 
    fgets(a,sizeof(a),stdin);
    for(int i = 0;i<1000000;i++)
    {
        if(a[i]%2==0&&a[i]!=0)
        {
            even = even + a[i];
            evencount++;
        }
        else if(a[i]%2!=0)
        {
            odd = odd +a[i];
            oddcount++;
        }
        else if(a[i]=='0')
        {
            break;
        }
    }
    int evenaverage = even/evencount;
    int oddaverage = odd/oddcount;
    printf("evencount:%d evenaverage:%d oddcount:%d oddaverage:%d",evencount,evenaverage,oddcount,oddaverage);
    return 0;
}
```



## 8.1

```C
int main()
{
    char a[1000000] = {0};
    fgets(a,sizeof(a),stdin);
    int b = strlen(a);
    for(int i = 0;i<1000000;i++)
    {
        if(a[i]=='\0')
        {
            a[i]=' ';
        }
    }
    printf("%d",b);
}
```



## 8.2

```C
int main()
{
    int ch;
    int count = 0;
    while((ch=getchar()) != EOF && ch!= '&')
    {
        count++;
    

    if(ch<32)
    {
        if(ch=='\n')
        {
            printf("\\n(10)");
            count = 0;
        }
        else if(ch == '\t')
        {
            printf("\\t(9)");
        }
        else
        {
            printf("^%c(%d)",ch+64,ch);
        }
    }
        else
        {
            printf("%c (%d)",ch,ch);
        }
        if(count % 10 == 0&& ch !='\n')
        {
            putchar('\n');
            count = 0;
        }
    }
    return 0;

}

## 
```

##  8.3

```C
int main()
{
    char a;
    int largercount = 0;
    int lowercount = 0;
    while((a=getchar())!=EOF)
    {
        if(isupper(a))
        {
            largercount++;
        }
        else if(islower(a))
        {
            lowercount++;
        }
    }
    printf("largercount:%d lowercount:%d",largercount,lowercount);
}
```



## 9.1

```C
double min(double x,double y)
{
    if(x>=y);return y;
    if(x<y);return x;
}
//测试
int main()
{
    double x = 7.33;
    double y = 9.66;
    printf("%.2lf",min(x,y));
}
```



## 9.2

```C
void chline(char ch[][3],int i,int j)
{
     printf("字符数组第%d行%d列的元素是:%c\n",i,j,ch[i][j]);
}
//测试
int main()
{
    char ch[1][3] = 
    {
        {'a' , 'b' , 'c'}
    };
    chline(ch,0,0);
}
```





## 9.3

```C
void function(char *ch,int x,int y)
{
     scanf("%s",ch);
     for(int i = 0;i<y;i++)
     {
        for(int j = 0;j<x;j++)
        {
            printf("%s ",ch);
        }
        printf("\n");
     }
}
//测试
int main()
{
    int x = 3;
    int y = 7;
    char ch[30000]={0};
    function(ch,x,y);
}
```



## 10.3

```C
// 返回int数组的最大值
int find_max_int(const int arr[], int n) {
    int max = arr[0];
    for (int i = 1; i < n; i++) {
        if (arr[i] > max) {
            max = arr[i];
        }
    }
    return max;
}
// 测试程序
int main() {
    int arr[] = {12, 45, 7, 98, 33};
    int len = sizeof(arr) / sizeof(arr[0]);
    int max_val = find_max_int(arr, len);
    printf("数组的最大值是：%d\n", max_val); // 输出98
    return 0;
}


```



## 10.4

// 返回double数组最大值的下标

```C
int find_max_double_index(const double arr[], int n) {
    int max_idx = 0;
    for (int i = 1; i < n; i++) {
        if (arr[i] > arr[max_idx]) {
            max_idx = i;
        }
    }
    return max_idx;
}
// 测试
int main() {
    double arr[] = {3.14, 6.28, 1.59, 9.81, 2.71};
    int len = sizeof(arr) / sizeof(arr[0]);
    int idx = find_max_double_index(arr, len);
    printf("最大值的下标是：%d，对应值：%.2f\n", idx, arr[idx]); // 输出3，对应9.81
    return 0;
}


```



## 10.5

```C
// 返回double数组最大值与最小值的差值
double max_min_diff(const double arr[], int n) {
    double max = arr[0], min = arr[0];
    for (int i = 1; i < n; i++) {
        if (arr[i] > max) max = arr[i];
        if (arr[i] < min) min = arr[i];
    }
    return max - min;
}

// 测试程序
int main() {
    double arr[] = {5.2, 1.8, 9.7, 3.4, 7.1};
    int len = sizeof(arr) / sizeof(arr[0]);
    double diff = max_min_diff(arr, len);
    printf("最大值与最小值的差值是：%.2f\n", diff); // 输出9.7-1.8=7.9
    return 0;
}


```





## 11.1

```C
void chars(char *arr,int n)
{
    for(int i = 0;i<n;i++)
    {
        arr[i] = getchar();
    }
    arr[n] = '\0';
}
int main()
{
    char arr[100];
    int n = 0;
    printf("请输入要读取的字符数：");
    scanf("%d",&n);
    getchar();//吸收换行符
    chars(arr,n);
    printf("读取的字符是:%s\n",arr);
    return 0;
}
```



## 11.2

```C
void chars(char *arr,int n)
{
    int i = 0;
    char ch;
    while(i < n)
    {
        ch = getchar();
        if(ch == ' ' ||ch == '\t' || ch == '\n')
        {
            break;
        }
        arr[i] = ch;
        i++;
    }
    arr[n] = '\0';
}
int main()
{
    char arr[100];
    int n = 0;
    printf("请输入要读取的字符数：");
    scanf("%d",&n);
    getchar();//吸收换行符
    chars(arr,n);
    printf("读取的字符是:%s\n",arr);
    return 0;
}
```



## 11.3

```C
void chars(char *arr)
{
    char ch;
    int i = 0;
    while ((ch = getchar())!=EOF)
    {
        if(ch!=' '&& ch != '\t' &&ch != '\n')
        {
            break;
        }
    }
    arr[i++] = ch;
    while((ch=getchar())!=EOF)
    {
        if(ch==' ' || ch=='\t' || ch == '\n')
        {
            break;
        }
        arr[i++] = ch;
    }
    arr[i] = '\0';
    while((ch = getchar())!=EOF && ch != '\n');
}

int main()
{
    char word[100];
    printf("请输入一行内容（包含单词）：\n");
    chars(word);
    printf("读取的单词是：%s\n",word);
    return 0;
}


```



## 12.4

```C
// 统计调用次数的函数
int call_count() 
{
    static int count = 0; // 静态变量，函数调用间保持值
    count++;
    return count;
}
// 测试
int main() 
{
    printf("测试函数调用次数：\n");
    for (int i = 0; i < 5; i++) 
    {
        printf("第 %d 次调用，返回值：%d\n", i+1, call_count());
    }
    return 0;
}
```



## 12.5

```C
#define SIZE 100
// 选择排序（降序）
void sort_descending(int arr[], int size) {
    for (int i = 0; i < size-1; i++) {
        int max_idx = i;
        for (int j = i+1; j < size; j++) {
            if (arr[j] > arr[max_idx]) {
                max_idx = j;
            }
        }
        // 交换当前元素与最大元素
        int temp = arr[i];
        arr[i] = arr[max_idx];
        arr[max_idx] = temp;
    }
}

// 打印数组（每行10个）
void print_array(int arr[], int size) {
    for (int i = 0; i < size; i++) {
        printf("%d ", arr[i]);
        if ((i+1) % 10 == 0) {
            printf("\n");
        }
    }
}
// 测试
int main() {
    int nums[SIZE];
    srand((unsigned int)time(NULL)); // 设置随机数种子（避免每次运行结果相同）

    // 生成100个1~10的随机数
    for (int i = 0; i < SIZE; i++) {
        nums[i] = rand() % 10 + 1; // rand()%10得到0~9，+1后范围1~10
    }
    
    printf("排序前的随机数：\n");
    print_array(nums, SIZE);
    
    // 降序排序
    sort_descending(nums, SIZE);
    
    printf("\n降序排列后：\n");
    print_array(nums, SIZE);
    
    return 0;

}




```



## 12.6

```C
#define SIZE 1000
// 统计1~10随机数的出现次数
void count_random_frequency(int seeds[], int seed_num) {
    for (int s = 0; s < seed_num; s++) {
        int count[11] = {0}; // count[1]~count[10]对应数字1~10的次数
        srand(seeds[s]);     // 设置不同种子

        // 生成1000个1~10的随机数并统计
        for (int i = 0; i < SIZE; i++) {
            int num = rand() % 10 + 1;
            count[num]++;
        }
    
        // 输出当前种子的统计结果
        printf("种子 = %d 时，各数出现次数：\n", seeds[s]);
        for (int num = 1; num <= 10; num++) {
            printf("数字 %d：%d 次\n", num, count[num]);
        }
        printf("------------------------\n");
    }

}
// 测试
int main() {
    // 10个不同的种子值
    int seeds[10] = {1, 10, 100, 1000, 1234, 5678, 9999, 123, 456, 789};
    

    count_random_frequency(seeds, 10);
    
    // 结论：不同种子生成的随机数分布不同，出现次数不相同
    printf("结论：不同种子生成的随机数，各数字出现次数不相同。\n");
    return 0;

}
```



## 13.1

```C
int main(void) 
{
    int ch;
    FILE *fp;
    unsigned long count = 0;
    char filename[100]; // 存储用户输入的文件名

    // 提示用户输入文件名
    printf("请输入要打开的文件名：");
    fgets(filename, sizeof(filename), stdin);
    // 移除fgets读取的换行符
    filename[strcspn(filename, "\n")] = '\0';
    
    // 打开文件
    if ((fp = fopen(filename, "r")) == NULL) 
    {
        printf("无法打开文件：%s\n", filename);
        exit(EXIT_FAILURE);
    }
    
    // 读取文件内容并统计字符数
    while ((ch = getc(fp)) != EOF) 
    {
        putc(ch, stdout); // 输出文件内容
        count++;
    }
    
    // 关闭文件并输出结果
    fclose(fp);
    printf("\n文件 %s 包含 %lu 个字符\n", filename, count);
    return 0;

}
```



## 13.2

***
```C
int main(int argc, char *argv[]) {
    FILE *src_fp, *dest_fp;
    int ch;

    // 检查命令行参数数量
    if (argc != 3) {
        printf("用法：%s 源文件名 目标文件名\n", argv[0]);
        exit(EXIT_FAILURE);
    }
    
    // 打开源文件（二进制读）
    if ((src_fp = fopen(argv[1], "rb")) == NULL) {
        printf("无法打开源文件：%s\n", argv[1]);
        exit(EXIT_FAILURE);
    }
    
    // 打开目标文件（二进制写）
    if ((dest_fp = fopen(argv[2], "wb")) == NULL) {
        printf("无法创建目标文件：%s\n", argv[2]);
        fclose(src_fp); // 关闭已打开的源文件
        exit(EXIT_FAILURE);
    }
    
    // 拷贝文件内容
    while ((ch = getc(src_fp)) != EOF) {
        putc(ch, dest_fp);
    }
    
    // 关闭文件
    fclose(src_fp);
    fclose(dest_fp);
    printf("文件拷贝完成：%s -> %s\n", argv[1], argv[2]);
    return 0;

}


```



## 13.3

***
```C
int main(void) {
    FILE *src_fp, *dest_fp;
    int ch;
    char filename[100];

    // 提示用户输入文件名
    printf("请输入要处理的文本文件名：");
    fgets(filename, sizeof(filename), stdin);
    filename[strcspn(filename, "\n")] = '\0'; // 移除换行符
    
    // 打开源文件（文本读）
    if ((src_fp = fopen(filename, "r")) == NULL) {
        printf("无法打开文件：%s\n", filename);
        exit(EXIT_FAILURE);
    }
    
    // 打开目标文件（文本写，覆盖原文件）
    if ((dest_fp = fopen(filename, "w")) == NULL) {
        printf("无法写入文件：%s\n", filename);
        fclose(src_fp);
        exit(EXIT_FAILURE);
    }
    
    // 读取内容、转大写并写入
    while ((ch = getc(src_fp)) != EOF) {
        putc(toupper(ch), dest_fp);
    }
    
    // 关闭文件
    fclose(src_fp);
    fclose(dest_fp);
    printf("文件已转为大写并保存：%s\n", filename);
    return 0;

}
```





## 14.1

***
```C
// 定义月份结构体
struct month {
    char name[20];    // 月份名
    char abbr[4];     // 月份缩写
    int days;         // 天数
    int num;          // 月份号
};

// 初始化非闰年的月份数组
struct month months[12] = {
    {"January", "Jan", 31, 1},
    {"February", "Feb", 28, 2},
    {"March", "Mar", 31, 3},
    {"April", "Apr", 30, 4},
    {"May", "May", 31, 5},
    {"June", "Jun", 30, 6},
    {"July", "Jul", 31, 7},
    {"August", "Aug", 31, 8},
    {"September", "Sep", 30, 9},
    {"October", "Oct", 31, 10},
    {"November", "Nov", 30, 11},
    {"December", "Dec", 31, 12}
};

// 函数：根据月份名/缩写，计算到该月的总天数
int total_days_by_name(const char *month_name) {
    int total = 0;
    int i;
    // 匹配月份名或缩写
    for (i = 0; i < 12; i++) {
        if (strcmp(month_name, months[i].name) == 0 || 
            strcmp(month_name, months[i].abbr) == 0) {
            // 累加前i个月的天数
            for (int j = 0; j <= i; j++) {
                total += months[j].days;
            }
            return total;
        }
    }
    return -1; // 匹配失败
}

// 测试程序
int main() {
    char input[20];
    printf("请输入月份名或缩写（如January/Feb）：");
    scanf("%s", input);
    

    int days = total_days_by_name(input);
    if (days == -1) {
        printf("输入的月份无效！\n");
    } else {
        printf("到该月为止的总天数：%d\n", days);
    }
    return 0;

}
```



## 14.2

***
```C
struct month {
    char name[20];
    char abbr[4];
    int days;
    int num;
};

struct month months[12] = {
    {"January", "Jan", 31, 1},
    {"February", "Feb", 28, 2},
    {"March", "Mar", 31, 3},
    {"April", "Apr", 30, 4},
    {"May", "May", 31, 5},
    {"June", "Jun", 30, 6},
    {"July", "Jul", 31, 7},
    {"August", "Aug", 31, 8},
    {"September", "Sep", 30, 9},
    {"October", "Oct", 31, 10},
    {"November", "Nov", 30, 11},
    {"December", "Dec", 31, 12}
};

// 判断是否为闰年
int is_leap(int year) {
    if ((year % 4 == 0 && year % 100 != 0) || (year % 400 == 0)) {
        return 1;
    }
    return 0;
}

// 根据月份（号/名/缩写）获取月份索引
int get_month_index(const char *month_input) {
    // 尝试匹配月份号
    int num = atoi(month_input);
    if (num >= 1 && num <= 12) {
        return num - 1;
    }
    // 尝试匹配月份名/缩写
    for (int i = 0; i < 12; i++) {
        if (strcmp(month_input, months[i].name) == 0 || 
            strcmp(month_input, months[i].abbr) == 0) {
            return i;
        }
    }
    return -1; // 无效
}

// 计算该日期是当年的第几天
int day_of_year(int day, const char *month_input, int year) {
    int m_idx = get_month_index(month_input);
    if (m_idx == -1 || day < 1) {
        return -1;
    }
    // 计算到该月的总天数
    int total = 0;
    for (int i = 0; i < m_idx; i++) {
        total += months[i].days;
    }
    // 处理闰年的2月
    if (m_idx >= 1 && is_leap(year)) {
        total += 1;
    }
    // 加上日期（需判断日期是否合法）
    int max_day = months[m_idx].days;
    if (m_idx == 1 && is_leap(year)) {
        max_day = 29;
    }
    if (day > max_day) {
        return -1;
    }
    total += day;
    return total;
}

int main() {
    int day, year;
    char month[20];
    printf("请输入日：");
    scanf("%d", &day);
    printf("请输入月（号/名/缩写）：");
    scanf("%s", month);
    printf("请输入年：");
    scanf("%d", &year);
    

    int result = day_of_year(day, month, year);
    if (result == -1) {
        printf("输入的日期无效！\n");
    } else {
        printf("该日期是当年的第 %d 天\n", result);
    }
    return 0;

}
```



## 14.3

***
```C
#define MAX_BOOKS 100
#define MAX_TITLE 50
#define MAX_AUTHOR 50

// 图书结构体
struct book {
    char title[MAX_TITLE];
    char author[MAX_AUTHOR];
    float value;
};

// 按书名字母序排序的比较函数
int compare_title(const void *a, const void *b) {
    const struct book *bookA = (const struct book *)a;
    const struct book *bookB = (const struct book *)b;
    return strcmp(bookA->title, bookB->title);
}

// 按价格升序排序的比较函数
int compare_price(const void *a, const void *b) {
    const struct book *bookA = (const struct book *)a;
    const struct book *bookB = (const struct book *)b;
    if (bookA->value < bookB->value) return -1;
    if (bookA->value > bookB->value) return 1;
    return 0;
}

// 输出图书列表
void print_books(struct book books[], int count, const char *title) {
    printf("\n===== %s =====\n", title);
    for (int i = 0; i < count; i++) {
        printf("《%s》 - %s - ￥%.2f\n", 
               books[i].title, books[i].author, books[i].value);
    }
}

int main() {
    struct book books[MAX_BOOKS];
    int count = 0;
    char choice;

    // 输入图书信息
    do {
        if (count >= MAX_BOOKS) {
            printf("已达到最大图书数量！\n");
            break;
        }
        printf("请输入第 %d 本图书的信息：\n", count + 1);
        printf("书名：");
        getchar(); // 吸收换行符
        fgets(books[count].title, MAX_TITLE, stdin);
        books[count].title[strcspn(books[count].title, "\n")] = '\0'; // 去掉换行符
        printf("作者：");
        fgets(books[count].author, MAX_AUTHOR, stdin);
        books[count].author[strcspn(books[count].author, "\n")] = '\0';
        printf("价格：");
        scanf("%f", &books[count].value);
        count++;
        printf("是否继续输入？(y/n)：");
        scanf(" %c", &choice);
    } while (choice == 'y' || choice == 'Y');
    
    // 按输入顺序输出
    print_books(books, count, "按输入顺序输出");
    
    // 按书名字母序输出（先拷贝数组避免原数据被修改）
    struct book books_title[MAX_BOOKS];
    memcpy(books_title, books, count * sizeof(struct book));
    qsort(books_title, count, sizeof(struct book), compare_title);
    print_books(books_title, count, "按书名字母序输出");
    
    // 按价格升序输出
    struct book books_price[MAX_BOOKS];
    memcpy(books_price, books, count * sizeof(struct book));
    qsort(books_price, count, sizeof(struct book), compare_price);
    print_books(books_price, count, "按价格升序输出");
    
    return 0;

}


```



## 15.1

```C
// 二进制字符串转int数值
int bin_str_to_int(const char *pbits) {
    int result = 0;
    int len = strlen(pbits);
    for (int i = 0; i < len; i++) {
        // 每一位字符转数字，左移累加
        result = (result << 1) + (pbits[i] - '0');
    }
    return result;
}

// 测试程序
int main() {
    char *pbits = "01001001";
    int num = bin_str_to_int(pbits);
    printf("二进制字符串 %s 转换为整数：%d\n", pbits, num); // 输出73
    return 0;
}


```



## 15.2

***
```C
//二进制字符串转int
int bin_to_int(const char *str) {
    int res = 0;
    for (int i = 0; str[i] != '\0'; i++) {
        res = (res << 1) + (str[i] - '0');
    }
    return res;
}

// int转二进制字符串（最多32位）
void int_to_bin(int num, char *str) {
    if (num == 0) {
        str[0] = '0';
        str[1] = '\0';
        return;
    }
    char temp[33];
    int idx = 0;
    // 处理负数（按补码输出）
    unsigned int u_num = (unsigned int)num;
    while (u_num > 0) {
        temp[idx++] = (u_num % 2) + '0';
        u_num /= 2;
    }
    temp[idx] = '\0';
    // 反转字符串得到正确顺序
    int len = strlen(temp);
    for (int i = 0; i < len; i++) {
        str[i] = temp[len - 1 - i];
    }
    str[len] = '\0';
}

// 测试程序
int main() {
    char bin1[33], bin2[33];
    printf("输入第一个二进制字符串：");
    scanf("%s", bin1);
    printf("输入第二个二进制字符串：");
    scanf("%s", bin2);

    int num1 = bin_to_int(bin1);
    int num2 = bin_to_int(bin2);
    char res[33];
    
    // 按位非 ~
    int_to_bin(~num1, res);
    printf("~%s = %s\n", bin1, res);
    int_to_bin(~num2, res);
    printf("~%s = %s\n", bin2, res);
    
    // 按位与 &
    int_to_bin(num1 & num2, res);
    printf("%s & %s = %s\n", bin1, bin2, res);
    
    // 按位或 |
    int_to_bin(num1 | num2, res);
    printf("%s | %s = %s\n", bin1, bin2, res);
    
    // 按位异或 ^
    int_to_bin(num1 ^ num2, res);
    printf("%s ^ %s = %s\n", bin1, bin2, res);
    
    return 0;

}


```



## 15.3

***
```C
// 统计整数中1的位的数量
int count_set_bits(int num) {
    int count = 0;
    // 处理负数（转为无符号数，按补码统计）
    unsigned int u_num = (unsigned int)num;
    while (u_num > 0) {
        count += (u_num & 1); // 取最低位，是1则加1
        u_num >>= 1;          // 右移一位
    }
    return count;
}

// 测试程序
int main() {
    int num;
    printf("输入一个整数：");
    scanf("%d", &num);
    int bits = count_set_bits(num);
    printf("整数 %d 中打开位的数量：%d\n", num, bits);
    return 0;
}




```















