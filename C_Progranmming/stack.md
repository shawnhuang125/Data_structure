# Stack堆疊
> First In Last Out
## Stack堆疊-push and pull功能(為了實現First In Last Out)
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
## infix to prefix-輸入並切割,判斷是否為運算子
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
## infix to prefix-判斷優先層級
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
