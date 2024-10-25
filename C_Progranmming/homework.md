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
