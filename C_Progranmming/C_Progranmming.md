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
