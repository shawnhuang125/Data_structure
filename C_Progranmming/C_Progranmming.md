# 基礎演算法實作
## 排序法
#### 插入排序法
#### 氣泡排序法
#### 快速排序法
## 方陣練習
#### 使用C語言宣告三個陣列並分別儲存這三個矩陣的值並印出
- 描述：已知三個矩陣 A4X3 ,B3X4 ,C4X4 其中C4X4  = A4X3 + B3X4 , 且 aij = i+j, bij = i×j, 
- 要求：
- 輸出：印出三個矩陣的值
```
#include<stdlib.h>
#include<stdio.h>
int main(){
    int table_one[3][3]={0},table_two[3][3]={0},table_three[3][3]={0};
    /*printf("table_one\n");
    for(int i=0;i<3;i++){
        for(int j=0;j<3;j++){
            printf("%d",table_one[i][j]);
            printf("\t");
        }
        printf("\n");
    }*/
    /*printf("table_two\n");
    for(int i=0;i<3;i++){
        for(int j=0;j<3;j++){
            printf("%d\t",table_two[i][j]);
        }
        printf("\n");
    }*/
    //printf("table_one_calculation\n");
    for(int i=0;i<3;i++){
        for(int j=0;j<3;j++){
            table_one[i][j] = i+j;
            //printf("%d\t",table_one[i][j]);
        }
        //printf("\n");
    }
    //printf("table_two_calculation\n");
    for(int i=0;i<3;i++){
        for(int j=0;j<3;j++){
            table_two[i][j] = i*j;
            //printf("%d\t",table_two[i][j]);

        }
        //printf("\n");
    }
    /*printf("table_three\n");
    for(int i=0;i<3;i++){
        for(int j=0;j<3;j++){
            printf("%d\t",table_three[i][j]);
        }
        printf("\n");
    }*/
    printf("Table_C_Result\n");
    for(int i=0;i<3;i++){
        for(int j=0;j<3;j++){
            table_three[i][j] = table_one[i][j] + table_two[i][j];
            printf("%d\t",table_three[i][j]);
        }
        printf("\n");
    }
    return 0;
}
```
- 結果
- ![image](https://github.com/user-attachments/assets/6a021c60-5a90-4db5-8859-be2d01f5b96c)

#### 使用C語言宣告三個陣列並分別儲存這三個矩陣的值並印出
- 描述：已知三個矩陣 A4X3 ,B3X4 ,C4X4 其中C4X4  = A4X3 × B3X4 , 且 aij = i+j, bij = i×j, 
- 要求：
- 輸出：印出三個矩陣的值
```
#include<stdlib.h>
#include<stdio.h>
int main(){
    int table_one[3][3]={0},table_two[3][3]={0},table_three[3][3]={0};
    /*printf("table_one\n");
    for(int i=0;i<3;i++){
        for(int j=0;j<3;j++){
            printf("%d",table_one[i][j]);
            printf("\t");
        }
        printf("\n");
    }*/
    /*printf("table_two\n");
    for(int i=0;i<3;i++){
        for(int j=0;j<3;j++){
            printf("%d\t",table_two[i][j]);
        }
        printf("\n");
    }*/
    //printf("table_one_calculation\n");
    for(int i=0;i<3;i++){
        for(int j=0;j<3;j++){
            table_one[i][j] = i+j;
            //printf("%d\t",table_one[i][j]);
        }
        //printf("\n");
    }
    //printf("table_two_calculation\n");
    for(int i=0;i<3;i++){
        for(int j=0;j<3;j++){
            table_two[i][j] = i*j;
            //printf("%d\t",table_two[i][j]);

        }
        //printf("\n");
    }
    /*printf("table_three\n");
    for(int i=0;i<3;i++){
        for(int j=0;j<3;j++){
            printf("%d\t",table_three[i][j]);
        }
        printf("\n");
    }*/
    printf("Table_C_Result\n");
    for(int i=0;i<3;i++){
        for(int j=0;j<3;j++){
            table_three[i][j] = table_one[i][j] * table_two[i][j];
            printf("%d\t",table_three[i][j]);
        }
        printf("\n");
    }
    return 0;
}
```
- 結果
- ![image](https://github.com/user-attachments/assets/abc83578-7dbf-480e-af5e-09d966335ec2)

#### 3*3魔術矩陣
- 描述：
- 請使用C語言宣告一陣列 int A[3][3], 並自動填入3×3魔術方陣的值後印出
```
#include<stdlib.h>
#include<stdio.h>
int main(){
    int x=0,y=1,array[3][3]={0};
    /*for(int i=0;i<3;i++){
        for(int j=0;j<3;j++){
            printf("%d\t",array[i][j]);
        }
        printf("\n");
    }*/
   array[0][1]=0;
   for(int value=1;value<10;value++){
    int x_new=0,y_new=0;
    x_new = (x+1)%3;
    y_new = (y-1+3)%3;
    if(array[y_new][x_new] != 0){
        y = y+1;
        printf("array[y][x]=%d\n",array[y][x]);
    }else{
        x = x_new;
        y = y_new;

    }
    array[y][x] = value;
    }
    for(int i=0;i<3;i++){
        for(int j=0;j<3;j++){
            printf("%d\t",array[i][j]);
        }
        printf("\n");
    }

    return 0;
}
```
- 結果
![image](https://github.com/user-attachments/assets/b803ea51-a97b-40f0-87d2-c7b78ddbd46a)


#### 9*9魔術矩陣
- 描述：
- 請使用C語言宣告一陣列 int A[9][9], 並自動填入3×3魔術方陣的值後印出
```
#include<stdlib.h>
#include<stdio.h>
int main(){
    int x=0,y=1,array[9][9]={0};
    /*for(int i=0;i<3;i++){
        for(int j=0;j<3;j++){
            printf("%d\t",array[i][j]);
        }
        printf("\n");
    }*/
   array[0][1]=0;
   for(int value=1;value<82;value++){
    int x_new=0,y_new=0;
    x_new = (x+1)%9;
    y_new = (y-1+9)%9;
    if(array[y_new][x_new] != 0){
        y = y+1;
        //printf("array[y][x]=%d\n",array[y][x]);
    }else{
        x = x_new;
        y = y_new;

    }
    array[y][x] = value;
    }
    for(int i=0;i<9;i++){
        for(int j=0;j<9;j++){
            printf("%d\t",array[i][j]);
        }
        printf("\n");
    }

    return 0;
}
```
- 結果
- - ![image](https://github.com/user-attachments/assets/38dfacdd-cddb-49dd-aa4d-1dfdf0052504)

#### 陣列的基本操作
- 題目描述：
- 實作一個簡單的程式來進行陣列的插入、刪除和搜尋操作。

- 要求：

- 輸入一組整數陣列。
- 插入新的元素到指定位置。
- 刪除指定位置的元素。
- 搜尋特定元素並輸出其在陣列中的位置。
- 輸入範例：

```
輸入陣列: 2 4 6 8
插入: 5 位置: 2
刪除位置: 3
搜尋: 4
```
- 程式碼:
```
```
- 輸出範例：

```
插入後陣列: 2 5 4 6 8
刪除後陣列: 2 5 4 8
搜尋結果: 位置 2
```
#### 字串倒序
- 題目描述：
- 寫一個程式，讀取一個字串並將其倒序輸出。

- 要求：

- 讀取使用者輸入的字串。
- 輸入範例：

```
輸入: hello
```
- 程式碼:
```
```
- 輸出範例：

```
倒序字串: olleh
```
#### 最大值和最小值
- 題目描述：
- 實作一個程式，讀取一組整數，並找出其中的最大值和最小值。

- 要求：

- 讀取一組整數並儲存在陣列中。
- 找出最大值和最小值。
- 輸入範例：

```
輸入: 10 22 3 15 7
```
- 程式碼:
```
```
- 輸出範例：

```
最大值: 22
最小值: 3
```
#### 簡單排序
- 題目描述：
- 寫一個程式對整數陣列進行排序，並顯示排序後的結果。

- 要求：

- 輸入一組整數。
- 使用選擇排序法（Selection Sort）對陣列進行升序排列。
- 顯示排序後的陣列。
- 輸入範例：

```
輸入: 5 3 8 1 2
```
- 程式碼:
```
```
- 輸出範例：

```
排序後的陣列: 1 2 3 5 8
```
#### 計算陣列元素的總和
- 題目描述：
- 寫一個程式來計算整數陣列中所有元素的總和。

- 要求：

- 讀取一組整數。
- 計算並輸出所有元素的總和。
- 輸入範例：

```
輸入: 4 7 1 3 9
```
- 程式碼:
```
```
- 輸出範例：

```
總和: 24
```
## Stack堆疊
> First In Last Out
### Stack堆疊-push and pull功能(為了實現First In Last Out)
- 程式碼:
```
#include<stdlib.h>
#include<stdio.h>
#define max 100
int push(int stack[],int *top,int value){
    if(*top==max-1){
        printf("the stack is full");
        return -1;
    }
    (*top)++;
    stack[*top] = value;
    printf("pushed %d to the stack\n",value);
    return 0;
}
int pop(int stack[],int *top){
    if(*top==-1){
        printf("the stack is empty\n");   //如果stack已經見底,輸出stack已經空了
        return -1;
    }
    int value;
    value = stack[*top];
    (*top)--;
    printf("poped %d out of stack\n",value);
    return 0;
}
int main(){
    int array[max],insert_value; //定義空陣列
    int x,top = -1;   //初始位址為-1
    while(1){
        printf("1: pull,2: pop,3:exit,please choose a num:");
        scanf("%d",&x);
        if(x==1){
            //push
            printf("please insert a num to stack:");
            scanf("%d",&insert_value);
            push(array,&top,insert_value);
        }else if(x==2){
            //pop
            pop(array,&top);
        }else if(x==3){
            printf("exiting...\n");
            break;
        }
    }
    // 顯示堆疊狀態
    if (top == -1) {
        printf("The stack is empty.\n");
    } else {
        printf("Current stack status: ");
        for (int i = 0; i <= top; i++) {  // 只顯示堆疊中有效的元素
            printf("%d", array[i]);
            if (i < top) {  // 避免最後一個元素後加逗號
                printf(", ");
            }
        }
        printf("\n");
    }
    return 0;
}
```
- 輸出範例：
```
1: pull,2: pop,3:exit,please choose a num:1
please insert a num to stack:2
pushed 2 to the stack
1: pull,2: pop,3:exit,please choose a num:1
please insert a num to stack:3
pushed 3 to the stack
1: pull,2: pop,3:exit,please choose a num:1
please insert a num to stack:4
pushed 4 to the stack
1: pull,2: pop,3:exit,please choose a num:1
please insert a num to stack:5
pushed 5 to the stack
1: pull,2: pop,3:exit,please choose a num:2
poped 5 out of stack
1: pull,2: pop,3:exit,please choose a num:3
exiting...
Current stack status: 2, 3, 4
```
### infix to prefix-輸入並切割,判斷是否為運算子
- 程式碼:
```
#include<stdlib.h>
#include<stdio.h>
#include<ctype.h>
int main(){
    char formula[100];  //初始化算式容器

    printf("please insert a formula:");
    scanf("%s",formula);        //先輸入算式
     printf("The formula contains the following characters:\n");    //確認切割無誤
    for(int i=0;formula[i] !='\0';i++){
        //切割
        int charac = formula[i];
        //printf("%c,\t",formula[i]);    
        if(isdigit(charac)){
            //判斷是否為數字
            printf("'%c' is number\n",charac);
        }else if(formula[i]){
            //判斷是否為運算子
            printf("'%c' is a operator\n",charac);
        }else{
            //其他未知的字元
            printf("'%c' is unknown chracter\n",charac);
        }


    }


    
    //判斷是不是數字
    //判斷operator的優先層級
    //輸出每個字元的優先層及
    
    return 0;
}
```
- 輸出範例：
```
please insert a formula:(3+2)*(5-3)
The formula contains the following characters:
'(' is a operator
'3' is number
'+' is a operator
'2' is number
')' is a operator
'*' is a operator
'(' is a operator
'5' is number
'-' is a operator
'3' is number
')' is a operator
```
### infix to prefix-判斷優先層級
- 程式碼:
```
#include<stdlib.h>
#include<stdio.h>
#include<ctype.h>
int operator_precedence(char oper){
    switch(oper){
        case '(':case ')':
            return 3;
        case '*':case '/':
            return 2;
        case '+':case '-':
            return 1;
        default:
            printf("operator precedence error: unknown operator '%c'\n", oper);
            return 0;

    }

}
int main(){
    char formula[100];  //初始化算式容器

    printf("please insert a formula:");
    scanf("%s",formula);        //先輸入算式
     printf("The formula contains the following characters:\n");    //確認切割無誤
    for(int i=0;formula[i] !='\0';i++){
        //切割
        int charac = formula[i];
        //printf("%c,\t",formula[i]);    
        if(isdigit(charac)){
            //判斷是不是數字
            printf("'%c' is number\n",charac);
        }else if(charac =='+' || charac =='-' || charac =='*' || charac =='/' || charac =='(' || charac ==')' ){

            int precedence = operator_precedence(charac);   //判斷operator的優先層級,並回傳層級的值
            printf("'%c' operator with precedence:%d\n",charac,precedence);
        }else{
            //其他未知的字元
            printf("'%c' is unknown chracter\n",charac);
        }


    }

    
    return 0;
}
```
- 輸出範例：
```
please insert a formula:(3+2)*(5-3)
The formula contains the following characters:
'(' operator with precedence:3
'3' is number
'+' operator with precedence:1
'2' is number
')' operator with precedence:3
'*' operator with precedence:2
'(' operator with precedence:3
'5' is number
'-' operator with precedence:1
'3' is number
')' operator with precedence:3
```
