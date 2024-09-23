# 資料結構與演算法
## 背景
- 一般來說資訊工程是將從傳感器蒐集的客觀事實上傳電腦通過人為操作電腦將資料組織,存取,管理成為一個有邏輯的資料結構。
- 資訊:客觀事實,蒐集的資料
- 工程:主要是一種手段,用來組織,存取或管理資料。
## 資料結構
> 定義:主要是經過演算法組織,存取或管理之後而產生的一個邏輯框架。
  用途:資料結構主要是用來組織資料。
## 演算法
> 定義: 是一個方法論,主要是用來存取,管理與組織資料的方法論,可以用來製作資料處理的框架。
  用途:用來管理和存儲資料
### 演算法的五大原則
  - 輸入/輸出:有定義好的輸入和輸出,讓輸入輸出更有效率。
  - 有限性:在有限的處理步驟中處理完數據並產出結果。
  - 明確性:一定要定義好每個步驟的正確性,電腦才看得懂你定義的處理流程。
  - 正確性:讓輸出的結果有較高的正確性。

### 如何判斷演算法的好壞?(在有正確性的情況下)
  - 時間複雜度:取決於電腦的處理時間
  - Big O of g(n):意思是再n趨近於無限大時,演算法裡面的最高次方就會主導結果,所以冪次愈小的可以忽略不計因為當n趨近於無限大,冪次愈小其值愈小,所以可以小道忽略不計。
  - ![image](https://github.com/user-attachments/assets/6cb5c46f-4593-473a-b266-dc25e504d3fc)
  - Homework:
  - 1.計算1到n的總和,求其時間複雜度?
  - 2.計算1!到n!的值,求其時間複雜度?
  - 空間複雜度:取決於占用多少電腦資源
### 基礎演算法實作(使用C)
#### 氣泡排序法
- 描述:
```
```
#### 插入排序法
- 描述:
```
```
#### 快速排序法
- 描述:
```
```
#### 選擇排序法
- 描述:
```
```
#### 線性搜尋法
- 描述:
```
```
#### 二分搜尋法
- 描述:
```
```
### 進階演算法實作(使用C)
#### 快速排序法
- 描述:
```
```
#### 合併排序法 (Merge Sort)
- 描述:
```
```
#### 深度優先搜尋法 (DFS)
- 描述:
```
```
#### 廣度優先搜尋法 (BFS)
- 描述:
```
```
#### Dijkstra 最短路徑演算法
- 描述:
```
```
## 20240919
### 題目 1: 使用C語言宣告三個陣列並分別儲存這三個矩陣的值並印出
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

### 題目 2: 使用C語言宣告三個陣列並分別儲存這三個矩陣的值並印出
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

### 題目 3: 二維陣列自動填入並輸出
- 描述：
- 請使用C語言宣告一陣列 int A[9][9], 並自動填入9×9魔術方陣的值後印出
```
#include<stdlib.h>
#include<stdio.h>
int main(){
    int table[9][9]={0};
    int value=0;
    for(int i=0;i<9;i++){
        for(int j=0;j<9;j++){
            table[i][j]=table[i][j]+value;
            value = value+1;
        }
    }
    printf("9x9 Table Result:\n");
    for(int i=0;i<9;i++){
        for(int j=0;j<9;j++){
            printf("%d\t",table[i][j]);
        }
        printf("\n");
    }
    return 0;
}
```
- 結果
- ![image](https://github.com/user-attachments/assets/d8fdf9d4-bbc5-4c9f-a678-330c13a7dd72)


