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
