# 資料結構
- 何謂資訊工程?
```
工程:
用有結構有方法的一套系統去處理資料
資訊:
客觀存在的現象,人為蒐集後所得到的結果
```
- 演算法的五大原則
  - 輸入/輸出:有定義好的輸入輸出,讓輸入輸出更有效率。
  - 有限性:在有限的處理步驟中處理完數據並產出結果。
  - 明確性:一定要定義好每個步驟的正確性,電腦才看得懂你定義的處理流程。
  - 正確性:讓輸出的結果有較高的正確性。
- 如何判斷演算法的好壞?(在有正確性的情況下)
  - 時間複雜度:取決於電腦的處理時間
  - Big O of g(n):意思是再n趨近於無限大時,演算法裡面的最高次方就會主導結果,所以冪次愈小的可以忽略不計因為當n趨近於無限大,冪次愈小其值愈小,所以可以小道忽略不計。
  - ![image](https://github.com/user-attachments/assets/6cb5c46f-4593-473a-b266-dc25e504d3fc)
  - Homework:
  - 1.計算1到n的總和,求其時間複雜度?
  - 2.計算1!到n!的值,求其時間複雜度?
  - 空間複雜度:取決於占用多少電腦資源
  - 
## 練習題
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

### 題目 4: 找出陣列中的最大值與最小值
- 描述：
- 撰寫一個程式，輸入一個整數陣列，然後找出該陣列中的最大值和最小值。
- 要求：
- 輸入：整數陣列，例如：[12, 34, 5, 67, 1, 90]
- 輸出：最大值和最小值
```
輸入: [12, 34, 5, 67, 1, 90]
輸出: 最大值 = 90, 最小值 = 1
```
### 題目 5: 陣列旋轉
- 描述：
- 給定一個整數陣列，撰寫一個函式來將陣列中的元素向右旋轉指定次數。
- 要求：
- 輸入：整數陣列和一個整數k，表示需要向右旋轉的次數，例如陣列[1, 2, 3, 4, 5]，旋轉2次變成[4, 5, 1, 2, 3]。
- 輸出：旋轉後的陣列
```
輸入: [1, 2, 3, 4, 5], k = 2
輸出: [4, 5, 1, 2, 3]
```
### 題目 6: 合併排序演算法實作
- 描述：
- 撰寫一個使用合併排序（Merge Sort）來排序整數陣列的程式。
- 要求：
- 輸入：未排序的整數陣列，例如[38, 27, 43, 3, 9, 82, 10]
- 輸出：排序後的陣列
```
輸入: [38, 27, 43, 3, 9, 82, 10]
輸出: [3, 9, 10, 27, 38, 43, 82]
```
