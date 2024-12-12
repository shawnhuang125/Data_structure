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
## 20241031 | infix to prefix
```
#include<stdlib.h>
#include<stdio.h>
#include<string.h>
#include<ctype.h>
int precedence(char cha){
    switch (cha){
    
    case '*': case '/':
        return 2;
    
    case '+': case '-':
        return 1;
    //deflaut很重要,因為當檢查到除了'+','-','*','/'以外的運算符,如果沒有0的話,會隨機產生一個值,從而導致錯誤判斷
    default:
        return 0;
    }
}
void infix_to_prefix(char stack[], char charac, int *top, char output[]) {
    char flutter[2];
    
    if (charac == ')') {
        // 如果遇到右括號，將其壓入堆疊
        stack[++(*top)] = charac;
    } else if (charac == '(') {
        // 遇到左括號，彈出堆疊中的運算符直到遇到右括號
        //這邊是處理括號內已經壓入後的運算符,一直彈出運算符直到')'
        while (*top != -1 && stack[*top] != ')') {
            flutter[0] = stack[(*top)--];
            flutter[1] = '\0';
            strcat(output, flutter);
        }
        // 將')'的位址減一,實質上stack內的')'還在,反正只會輸出output陣列,所以沒關係
        if (*top != -1) {
            (*top)--;
        }
    } else if (precedence(charac) != 0) {
        //處理所有要壓入的運算符
        // 當遇到有效運算符時，根據優先順序處理
        while (*top != -1 && precedence(stack[*top]) >= precedence(charac)) {
            flutter[0] = stack[(*top)--];
            flutter[1] = '\0';
            strcat(output, flutter);
        }
        // 將當前運算符壓入堆疊
        stack[++(*top)] = charac;
    }
}
void reverse(char *str){
    int len = strlen(str);
    for(int i=0;i<len/2;i++){
        //只跑到一半而已
        //將第一格字元儲存
        char temp = str[i];
        //例如1跟6-1-1,下一次2跟6-1-2,下一次3跟6-1-3
        str[i] = str[len-1-i];
        str[len-1-i] = temp;
    }
    
}
int main(){
    char formula[100];  //輸入的formula
    char stack[100];    //壓入運算符用的stack
    char flutter[2];    //輸出到output陣列用的緩衝區
    char output[100]="";   //輸出prefix用的陣列
    int top = -1;   //指標初始化
    //輸入infix formula
    printf("infix formula:");
    scanf("%s",&formula);
    // 開始由右到左切割,並處理優先順序及判斷
    for(int i=strlen(formula)-1;i>=0;i--){
        //由右到左切割
        char charac = formula[i];

        if(isdigit(formula[i])){
            //推出到output
            flutter[0] = charac;
            flutter[1] = '\0';
            strcat(output,flutter);
        }else{
            //開始判斷
            infix_to_prefix(stack,charac,&top,output);
        }




    }

        //將堆疊清空
    while(top!=-1){
        //推出到output
        flutter[0] = stack[top--];
        flutter[1] = '\0';
        strcat(output,flutter);
    }
    //翻轉output成為prefix formula
    reverse(output);
    
    
    printf("prefix formula:");
    printf("%s\n",output);
    return 0;
}
```
- 輸出
```
infix formula:(9-7)*(5-2)
prefix formula:*-97-52
```
- 重點
- 如果遇到右括號，將其壓入堆疊
```
if (charac == ')') {
        stack[++(*top)] = charac;
    }
```
- 如果遇到左括號，彈出堆疊中的運算符直到遇到右括號
```
 else if (charac == '(') {
        while (*top != -1 && stack[*top] != ')') {
            flutter[0] = stack[(*top)--];
            flutter[1] = '\0';
            strcat(output, flutter);
        }
        if (*top != -1) {
            (*top)--;
        }
    }
```
- 這邊是處理括號內已經壓入後的運算符,一直彈出運算符直到')'
```
while (*top != -1 && stack[*top] != ')') {
            flutter[0] = stack[(*top)--];
            flutter[1] = '\0';
            strcat(output, flutter);
        }
```
- 處理所有要壓入的運算符,當遇到有效運算符時，根據優先順序處理
```
else if (precedence(charac) != 0) {
        while (*top != -1 && precedence(stack[*top]) >= precedence(charac)) {
            flutter[0] = stack[(*top)--];
            flutter[1] = '\0';
            strcat(output, flutter);
        }
        stack[++(*top)] = charac;
    }
```
