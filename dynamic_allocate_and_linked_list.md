# Dynamic Allocate動態配置與Linked List鏈結串列
> 甚麼是動態配置Dynamic Allocate?為何每個節點變數記憶體位址是不連續的?

> 每次新增一個節點變數(登記戶籍居住地)就會隨機找到空地去蓋房子,戶籍居住地地址是隨機不連續分配的(也就是形成片段的記憶體位址的原因)

> 為何使用動態配置? 為何使用雙重指標?

> 因為是多層的資料結構,所以使用靜態配置已經不夠,需要靈活性更高的動態配置,只有動態配置可以滿足多層次資料結構的宣告需求

> 甚麼是節點? 甚麼是鏈結?

> 節點:每個節點比較像是每一個戶籍居住地的概念

> 鏈結:就是一個地址列表的戶籍謄本的概念,主要紀錄戶籍地址

## 使用C語言編寫(單向鏈結串列)

   - 使用struct定義結構方便後續使用結構體(單向鏈結串列)
 
   ```
   struct node {
	//宣告節點的儲存數據欄位
	int data;
	//宣告鏈結列表本體,也就是指標變數
	struct node* next;
   };
   ```
  
   - 主程式初始化head(單向鏈結串列)
     
   ```
   int main(){
	//初始化linked list的head
 	//只要是使用struct定義新的結構運算變數就一定要加上struct node*
	struct node* head = NULL;
 	//這邊是return NULL回傳空的數值
	return 0;
 
   }
   ```
 
   - 為甚麼要初始化head?
   > 因為如果沒有head,linked list將無法借助任何指標當作起點來輸入數據,沒有這個將會顯示錯誤
  
   ```
   [ERROR] 'head' was not declared in this scope
   ```
 
   - create node建立節點的函數(單向鏈結串列):

   ```
   struct node* createnode(int node_data){
 	struct node* newnode = (struct node*)malloc(sizeof(struct node));
 	if(newnode==NULL){
 		printf("memory allocation failed!");
 	}
 	newnode->data = node_data;
 	newnode->next = NULL;
 	//這邊如果是return 0就會回傳空的數值,所以一定要return newnode這樣新的節點位址才會更新
 	return newnode;
   }
   ```
 
   > Tips:只要會用到結構體的變數一定要用struct
   > Tips:一定要想清楚是用原本的指標還是搜尋後已經更新的指標
   > 如果head指向的下一個位址為NULL則新增結點到head後面,反之就一直往下搜尋node值到最後一個node的指向位址為NULL
   > 之後其他含是需要建立節點就可直接呼叫
	
   - Add node新增節點的函式(單向鏈結串列):

   ```
   int AddEnd(struct node** head,int node_data){
	//node**是指標的指標,第一層指標是node(每個節點)第二層指標是node->next(結點內部的next指標)
	struct node* newnode = createnode(node_data);
	if(*head==NULL){
		//如果節點為空就在head後新增節點
		*head = newnode;
	}else{
 		//邏輯是當節點指向下一個地位址不為空則印出該節點,直到節點下一個地位址為空
		struct node* temp = *head;
		while(temp->next!=NULL){
			temp = temp->next;
		}
		*head = newnode;	
	}
	
   }
 	
   ```
  
  - Print node列印list的函式(單向鏈結串列):

  ```
	int PrintList(struct node* head){
		printf("head   --->   ");
		struct node* temp = head;
 		//邏輯是當節點指向下一個地位址不為空則印出該節點,直到節點下一個地位址為空
		while(temp!=NULL){
			printf("%d   --->   ",temp->data);
			temp = temp->next;
		}
 		printf("NULL\n");
	
	}
  ```
  
  - insert node插入節點的函數(單向鏈結串列):
   
  ```
     struct node* insertnode(struct node* head,int target,int value){
	//找到指定的node
	struct node* temp = head;
	while(temp!=NULL && temp->data!=target){
		//當節點不為空且DATA不為TARGET就更新TEMP->NEXT
		temp = temp->next; 
	} 
	if(temp==NULL){
		printf("cannot find the particular node!");
		//返回head是因為要返回整個更新之後的鏈結串列 
		return head;
	}
	//加入新節點
	struct node* newnode = (struct node*)malloc(sizeof(struct node));
	if (newnode == NULL) {
        printf("Memory allocation failed!\n");
        return head; // 如果記憶體分配失敗，返回原鏈結串列
    	}
	//先把data加到新節點的數據欄位 
	newnode->data = value;
	//新節點的next指向目標節點的next 
	newnode->next = temp->next;
	//再目標節點的next指向新節點
	temp->next =  newnode;
	//返回head是因為要返回整個更新之後的鏈結串列 
	return head;
	}
   ```
 
   - delete node刪除節點的函數(單向鏈結串列):
   ```
	struct node* delnode(struct node** head,int ptcl_nodata){
		//定義一個用來修改結構體的指標變數
		struct node* current = *head;
		//初始化一個用來儲存指定節點的前一個節點的指針列表
		struct node* bfnode = NULL;
		//判斷是不是空列表
		if(current==NULL){
		printf("The linked list is empty!Please add something!\n");
		return *head;
		}
		//判斷指定節點是不是頭節點
		if(current->data==ptcl_nodata){
			*head = current->next;
			free(current);
			printf("Deleted head node containing: %d\n",ptcl_nodata);
			return *head;
		}
		// 如果未找到指定節點
    		if (current == NULL) {
        		printf("Node containing %d not found in the list.\n", ptcl_nodata);
        		return *head;
		}
		while(temp!=NULL && temp->data != ptcl_nodata){
			bfnode = current;
			temp = temp->next;
		}
		//將指定節點的前一個節點指向指定節點的後一個節點的記憶體位址
		bfnode->next = current->next;
		free(current);
		printf("Successfully delete node:%d\n",ptcl_nodata);
		return *head;
	}
   ```

   - 單向鏈結串列完整程式碼:
   ```
   #include<stdio.h>
   #include<stdlib.h>
   struct node {
	//使用struct定義linked list結構 
	int data;
	//每個node會指向下一個記憶體空間 
	struct node* next;
   } node;
   struct node* createnode(int node_data){
	//為了定義新nod所以要記憶體空間
	struct node* newnode = (struct node*)malloc(sizeof(struct node));
	//如果沒有要到記憶體空間回傳錯誤 
	if(newnode == NULL){
		printf("memory allocation failed!");
	}
	newnode->data =  node_data;
	newnode->next = NULL;
	return newnode;
   }
   struct node* AddEnd(struct node** head,int node_data){
	//進行新節點的定義與data的輸入 
	struct node* newnode =  createnode(node_data);
	 
	if(*head == NULL){
		//如果head的記憶體位址值指向為NULl就在head後面加入新節點
		*head = newnode;
	}else{
		//如果head沒有指向NULl就一直遍歷到節點的指向為NULL
		struct node* temp = *head;
		while(temp->next != NULL){
			//遍歷到節點的指向為NULL
			temp = temp->next;
		}
		//從最後一個指向為NULL的節點後開始建置新結點 
		temp->next = newnode;
		
	}	
   }
   struct node* insertnode(struct node* head,int ptcl_nodata,int insert_data){
	//先遍歷到節點直到節點的data為ptcl_node
	struct node* temp = head;
	while(temp->data!=ptcl_nodata){
		temp = temp->next;
	}
	if(temp==NULL){
		//如果找不到該節點則回傳錯誤 
		printf("Can not find the particular node!Please try again!");
		//返回head是因為要返回整個更新之後的鏈結串列 
		return head;
	}
	//在ptcl_node後加入新節點 
	struct node* newnode = createnode(insert_data);
	//如果沒有要到記憶體空間回傳錯誤 
	if(newnode == NULL){
		printf("memory allocation failed!");
	}
	//將資料放入新節點 
	newnode->data = insert_data;
	//將新節點的記憶位址指向為指定節點的記憶位址指向 
	newnode->next = temp->next;
	//加上後續已經更新後的linked list 
	temp->next = newnode;
	return head;
	
   }
   struct node* delnode(struct node** head,int ptcl_nodata){
	//定義一個用來修改結構體的指標變數
	struct node* current = *head;
	//初始化一個用來儲存指定節點的前一個節點的指針列表
	struct node* bfnode = NULL;
	//判斷是不是空列表
	if(current==NULL){
		printf("The linked list is empty!Please add something!\n");
		return *head;
	}
	//判斷指定節點是不是頭節點
	if(current->data==ptcl_nodata){
		*head = current->next;
		free(current);
		printf("Deleted head node containing: %d\n",ptcl_nodata);
		return *head;
	}
	// 如果未找到指定節點
    	if (current == NULL) {
        	printf("Node containing %d not found in the list.\n", ptcl_nodata);
        	return *head;
	}
	while(current!=NULL && current->data != ptcl_nodata){
		bfnode = current;
		current = current->next;
	}
	//將指定節點的前一個節點指向指定節點的後一個節點的記憶體位址
	bfnode->next = current->next;
	free(current);
	printf("Successfully delete node:%d\n",ptcl_nodata);
	return *head;
   }
   int PrintList(struct node* head){
	struct node* temp = head;
	printf("Head   --->   ");
	while(temp!=NULL){
		//如果head記憶體位址值指向不為NULl就一直遍歷到節點的指向為NULL
		printf("%d   --->   ",temp->data);
		temp = temp->next;
	}
	printf("NULL\n");
   }
   int main(){
	//定義head 
	struct node* head = NULL;
	int i;
	while(1){
		printf("1: CREATE NEW NODE;\n2:INSERT NEWNODE IN PARTICIPATION;\n3: TO CHECK LINKED LIST;\n4:DELETE NODE PARTICIPATELY;\n5: LEAVE\n");
		printf("Insert num:");
		scanf("%d",&i);
		if(i==1){
			//建立節點,輸入節點資料
			printf("loading to createnode.\n"); 
			printf("insert data to create node:");
			int insert_data;
			scanf("%d",&insert_data);
			AddEnd(&head,insert_data);
			printf("Seccesfully insert data:%d\n",insert_data);
		}else if(i==2){
			//插入節點,輸入節點資料
			printf("particularilly insert new node.\n");
			printf("To choose a particular node:");
			int node;
			scanf("%d",&node);
			printf("insert data :");
			int newnodata;
			scanf("%d",&newnodata);
			printf("Seccesfully insert data:%d after %d\n",newnodata,node);
			insertnode(head,node,newnodata);   
		}else if(i==3){
			//查看Linked List 
			printf("loading to check the linked list.\n"); 
			PrintList(head);
		}else if(i==4){
			//刪除指定節點 
			int nodata;
			printf("particularilly delete node.\n"); 
			printf("Insert data of the node you want:");
			scanf("%d",&nodata);
			delnode(&head,nodata);
		}else if(i==5){
			//跳出while迴圈
			printf("leaving...\n"); 
			break; 
		}else{
			printf("Insert ERROR!Please try again!\n");
		}
	}
	
	return 0;
   } 
   ```
   - 輸出:
   ```
   1: CREATE NEW NODE;
   2:INSERT NEWNODE IN PARTICIPATION;
   3: TO CHECK LINKED LIST;
   4:DELETE NODE PARTICIPATELY;
   5: LEAVE
   Insert num:1
   loading to createnode.
   insert data to create node:3
   Seccesfully insert data:3
   1: CREATE NEW NODE;
   2:INSERT NEWNODE IN PARTICIPATION;
   3: TO CHECK LINKED LIST;
   4:DELETE NODE PARTICIPATELY;
   5: LEAVE
   Insert num:1
   loading to createnode.
   insert data to create node:4
   Seccesfully insert data:4
   1: CREATE NEW NODE;
   2:INSERT NEWNODE IN PARTICIPATION;
   3: TO CHECK LINKED LIST;
   4:DELETE NODE PARTICIPATELY;
   5: LEAVE
   Insert num:1
   loading to createnode.
   insert data to create node:6
   Seccesfully insert data:6
   1: CREATE NEW NODE;
   2:INSERT NEWNODE IN PARTICIPATION;
   3: TO CHECK LINKED LIST;
   4:DELETE NODE PARTICIPATELY;
   5: LEAVE
   Insert num:1
   loading to createnode.
   insert data to create node:7
   Successfully insert data:7
   1: CREATE NEW NODE;
   2:INSERT NEWNODE IN PARTICIPATION;
   3: TO CHECK LINKED LIST;
   4:DELETE NODE PARTICIPATELY;
   5: LEAVE
   Insert num:1
   loading to createnode.
   insert data to create node:8
   Successfully insert data:8
   1: CREATE NEW NODE;
   2:INSERT NEWNODE IN PARTICIPATION;
   3: TO CHECK LINKED LIST;
   4:DELETE NODE PARTICIPATELY;
   5: LEAVE
   Insert num:3
   loading to check the linked list.
   Head   --->   3   --->   4   --->   6   --->   7   --->   8   --->   NULL
   1: CREATE NEW NODE;
   2:INSERT NEWNODE IN PARTICIPATION;
   3: TO CHECK LINKED LIST;
   4:DELETE NODE PARTICIPATELY;
   5: LEAVE
   Insert num:2
   particularilly insert new node.
   To choose a particular node:4
   insert data :5
   Seccesfully insert data:5 after 4
   1: CREATE NEW NODE;
   2:INSERT NEWNODE IN PARTICIPATION;
   3: TO CHECK LINKED LIST;
   4:DELETE NODE PARTICIPATELY;
   5: LEAVE
   Insert num:3
   loading to check the linked list.
   Head   --->   3   --->   4   --->   5   --->   6   --->   7   --->   8   --->   NULL
   1: CREATE NEW NODE;
   2:INSERT NEWNODE IN PARTICIPATION;
   3: TO CHECK LINKED LIST;
   4:DELETE NODE PARTICIPATELY;
   5: LEAVE
   Insert num:4
   particularilly delete node.
   Insert data of the node you want:8
   Successfully delete node:8
   1: CREATE NEW NODE;
   2:INSERT NEWNODE IN PARTICIPATION;
   3: TO CHECK LINKED LIST;
   4:DELETE NODE PARTICIPATELY;
   5: LEAVE
   Insert num:3
   loading to check the linked list.
   Head   --->   3   --->   4   --->   5   --->   6   --->   7   --->   NULL
   1: CREATE NEW NODE;
   2:INSERT NEWNODE IN PARTICIPATION;
   3: TO CHECK LINKED LIST;
   4:DELETE NODE PARTICIPATELY;
   5: LEAVE
   Insert num:5
   leaving...

   ```
- 總結:
- 如果要加在所有節點為value後面:確認是否為空串列,開始遍歷節點直到節點末端,如果節點值為target則加入新節點,把temp->next的位址值丟給新節點的next,把temp->next指向給新節點,然後把newnode更新到temp,count加一紀錄已增加一筆資料,這樣下次會從新節點的下一個位址繼續遍歷
### 單向鏈結串列習題
- **練習(已完成)**
- 建立一鏈結串列, 有三個節點, 其值分別為24,36,48
- **練習(已完成)**
- 建立一鏈結串列, 有三個節點, 其值分別為24,36,48, 並依序顯示鏈結串列所有節點的值
- **練習(已完成)**
- 讓使用者輸入三個值, 建立一鏈結串列儲存這三個值, 依序顯示鏈結串列所有節點的值, 這些值的總和與平均值
- 例如: 使用者輸入三個值為: 23,34,45
```
顯示:使用者輸入的值為: 23,34,45
總和為: 102
平均為: 34
```
- **練習(已完成)**
- 已知一鏈結串列, 有三個節點, 其值分別為24,36,48,插入一個新節點其值為40至鏈結串列中第三個節點位置,並依序顯示鏈結串列所有節點的值
- 讓使用者輸入4個數, 依序按數的大小(從小到大)建立一鏈結串列, ,並依序顯示鏈結串列所有節點的值 (例如當使用者輸入4個數, 其值分別為32,38,24,36,則鏈結串列建立過程如下)
- **練習**
- 建立一鏈結串列, 有五個節點, 其值分別為24,36,48,60,72
- (1)並依序顯示鏈結串列所有節點的值(已完成)
- (2)刪除串列中第三個節點,依序顯示鏈結串列所有節點的值
- (3)找出串列中值為36的節點並刪除,依序顯示鏈結串列所有節點的值
- **練習**
- 建立一鏈結串列, 輸入十個任意值, 
- (1)顯示鏈結串列所有節點的值及其總和
- (2)顯示鏈結串列最大值及其節點位置與最小值及其節點位置
- (3)刪除鏈結串列最大值後再顯示鏈結串列所有節點的值
- (4)新增一任意值在鏈結串列最大值後再顯示鏈結串列所有節點的值
- (5)新增一任意值在鏈結串列最大值前再顯示鏈結串列所有節點的值
## 雙向鏈結串列
   - 結構體定義:
   ```
   struct node {
   	int data;
   	struct node* next;
   	struct node* prev;
   } node;
   ```
   - create node建立節點的函數(雙向鏈結串列):
   ```
   struct node* create(int value){
   	struct node* newnode = (struct node*)malloc(sizeof(struct node);
   	if(newnode==NULL){	printf("memory allocation failed!};
   	newnode->data = value;
   	newnode->prev = NULL;
   	newnode->next = NULL;
   	return newnode;
   }
   ```
   - Add node新增節點的函式(雙向鏈結串列):
   ```
   struct node* add(struct node** head,int value){
   	struct node* newnode = create(value);
   	if(*head==NULL){
		// if the node is the head node
		*head = newnode;
   	}else{
		struct node* temp = *head;
		while(temp->next!=NULL){
			temp = temp->next;
		}
		temp->next = newnode;
		newnode->prev = temp;
	}
	return *head;
   }
   ```
   - insert node插入節點的函數(雙向鏈結串列):
   ```
   struct node* insert_by_value(struct node** head, int number, int value){
   	struct node* temp = *head;
    	if(*head==NULL){	printf("the linked list is empty!");}
	if(number==1){
		// if the node is the head node
		struct node* newnode = createnode(value);
		newnode->next = *head;
		(*head)->prev = newnode;
		(*head) = newnode;
		return *head;
	}
	int count=1;
	while(temp!=NULL && count < target-1){
		temp= temp->next;
		count++;
   	}
	
 	struct node* newnode = createnode(value);
	temp->next = newnode;
	newnode->next = temp->next;
	temp->next->prev = newnode;
	newnode->prev = temp;
	return *head;
   }
   ```
   - delete node刪除節點的函數(雙向鏈結串列):
   ```
   struct node* del(struct node** head, int value){
   	struct node* temp = *head;
	struct node* pri = NULL;
	while(temp!=NULL && temp->data!=value){
		pri = temp;
		temp = temp->next;
   	}
	if(temp->next==NULL){
		printf("cannot find the node!");
	}
	if(temp== *head){
		if(temp->next!=NULL){
			temp->next->pri = NULL;
		}
		*head = temp->next;
		free(temp);
	}else{
		pri->next = temp->next;
		temp->next->prev = pri;
		free(temp);
	}
	return *head;
   }
   ```
   - 找最大值或最小值的函式
   ```
   int show_max(struct node* head){
	struct node* temp = head;
	int count=1,position=1,max = temp->data;
	while(temp!=NULL){
		if(temp->data > max){
			max = temp->data;
			count = position;
		}
		temp = temp->next;
		position++;
	}
 	printf("the position of %d is:%d\n",max,count);
   }
   ```
   - 完整程式碼:
   ```
   #include<stdio.h>
#include<stdlib.h>
#include <string.h>
struct node {
	int data;
	struct node* prev;
	struct node* next;
}; 
struct node* createnode(int node_data){
	struct node* newnode = (struct node*)malloc(sizeof(struct node));
	if(newnode==NULL){	printf("memory allocate error!");}
	newnode->data = node_data;
	newnode->next = NULL;
	newnode->prev = NULL;
	return newnode;
}
struct node* add(struct node** head, int node_data){
	struct node* newnode = createnode(node_data);
	if(*head == NULL){
		*head = newnode;
		return *head;
	}
	struct node* temp = *head;
	while(temp->next!=NULL){
		temp = temp->next;
	}
	temp->next = newnode;
	newnode->prev = temp;
	return *head;
}
struct node* insert(struct node** head, int number, int value){
	
	if(*head==NULL){
		printf("the linked list is empty!");
	}
	
	if(number == 1){
		struct node* newnode = createnode(value);
		newnode->next = *head;
		(*head)->prev = newnode;
		*head = newnode;
		return *head;
	}
	struct node* temp = *head;
	int count=1;
	while(temp!=NULL && count < number-1){
		temp = temp->next;
		count++;
	}
	struct node* newnode = createnode(value);
	newnode->next = temp->next;
	temp->next = newnode;
	newnode->prev = temp;
	return *head;
}
struct node* del(struct node** head, int value){
	if(*head==NULL){
		printf("the list is enpty!");
	}
	struct node* pri = NULL;
	struct node* temp = *head;
	while(temp!=NULL && temp->data!=value){
		pri = temp;
		temp = temp->next;
	}
	if(temp->next==NULL){
		printf("cannot find the node!");
	}
	if(temp==*head){
        //head node situation
        if(temp->next != NULL){
			temp->next->prev = NULL;
		}
		*head = temp->next;
	}else{
		pri->next = temp->next;
		temp->next->prev = temp->prev;
	}
    free(temp);
	return *head;
	
}
int show_max(struct node* head){
    struct node* temp = head;
    int max=temp->data;
    int count=1,temp_count=1;
    while(temp!=NULL){
        if(temp->data > max){
            max = temp->data;
            count = temp_count;
        }
        temp = temp->next;
        temp_count++;
    }
    printf("position of %d is:%d\n",max,count);
}
int show(struct node* head){
	struct node* temp = head;
	while(temp!=NULL){
		printf("%d --> ",temp->data);
		temp = temp->next;
	}
	printf("NULL\n");
}
int total(struct node* head){
	struct node* temp = head;
	int total=0;
	while(temp!=NULL){
		total = total + temp->data;
		temp = temp->next;
	}
	printf("total:%d\n",total);
	return 0;
}
int main(){
	int i=0;
	struct node* head = NULL;
	while(i!=7){
		printf("1:add\n2:show\n3:delete\n4:total\n5:insert\n6:position of maximum\n7:exit\n");
		printf("insert i:");
		scanf("%d",&i);
		if(i==1){
			//add
			int value;
			printf("insert value:");
			scanf("%d",&value);
			add(&head,value);
		}else if(i==2){
			//show
			show(head);
		}else if(i==3){
			//del
			int value;
			printf("insert value:");
			scanf("%d",&value);
			del(&head,value);
		}else if(i==4){
			//total
			total(head);
		}else if(i==5){
			//insert
			int value,number;
			printf("insert number:");
			scanf("%d",&number);
			printf("insert value:");
			scanf("%d",&value);
			insert(&head,number,value);
		}else if(i==6){
			//maximum
            show_max(head);
		}else if(i==7){
			break;
		}else{
			printf("insert error!");
			break;
		}
	}
	return 0;
}
   ```
### 雙向鏈結練習題
- 建立一雙向鏈結串列, 輸入十個任意值, 
- (1)顯示鏈結串列所有節點的值及其總和(已做)
- (2)顯示鏈結串列最大值及其節點位置與最小值及其節點位置
- (3)刪除鏈結串列最大值後再顯示鏈結串列所有節點的值
- (4)新增一任意值在鏈結串列最大值後再顯示鏈結串列所有節點的值
- (5)新增一任意值在鏈結串列最大值前再顯示鏈結串列所有節點的值
### APCS實作題
- **問題描述**:「定時 K 彈」是一個團康遊戲，N 個人圍成一個圈，由 1 號依序到 N 號，從 1 號開始依序傳遞一枚玩具炸彈，炸彈每次到第 M 個人就會爆炸，此人即淘汰，被淘汰的人要離開圓圈，然後炸彈再從該淘汰者的下一個開始傳遞。遊戲之所以稱 K 彈是因為這枚炸彈只會爆炸 K 次，在第 K 次爆炸後，遊戲即停止，而此時在第 K 個淘汰者的下一位遊戲者被稱為幸運者，通常就會被要求表演節目。例如 N=5 ， M=2 ，如果 K=2 ，炸彈會爆炸兩次，被爆炸淘汰的順序依序是 2 與 4（參見下圖），這時 5 號就是幸運者。如果 K=3，剛才的遊戲會繼續，第三個淘汰的是 1 號，所以幸運者是 3 號。如果K=4，下一輪淘汰 5 號，所以 3 號是幸運者。此題輸入 N、M 與 K，請你計算出誰是幸運者。
- **輸入格式**:輸入只有一行包含三個正整數，依序為 N、M 與 K，兩數中間有一個空格分開。其中 `1≤𝐾<𝑁`
- **輸出格式**:請輸出幸運者的號碼，結尾有換行符號。
- **詳解**

