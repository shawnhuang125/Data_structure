# Dynamic Allocate動態配置與Linked List鏈結串列
> 特性:動態配置Dynamic Allocate

> 記憶體空間是片段的,所以需要使用指標來儲存每個變數的記憶體位置

> 陣列就算是靜態配置,因為要先宣告記憶體空間。

> 針對鏈結串列可以做四個動作:create-->add-->insert-->delete

## 指標介紹
- **甚麼是指標?甚麼是雙重指標?**
- 舉例說明:
```
#include <stdio.h>

void updatePointer(int** pp, int* newAddr) {
    *pp = newAddr;  // 修改單層指標的內容
}

int main() {
    int a = 10, b = 20;
    int* p = &a;    // 單層指標，指向 a
    int** pp = &p;  // 雙層指標，指向 p

    printf("p 初始指向: %p\n", p);    // 指向 a 的地址
    printf("a 的值: %d\n", *p);       // a 的值 10

    updatePointer(pp, &b);            // 修改 p，讓它指向 b

    printf("p 修改後指向: %p\n", p);  // 指向 b 的地址
    printf("b 的值: %d\n", *p);       // b 的值 20

    return 0;
}
```
- 輸出
```
p 初始指向: 000000000062FE14
a 的值: 10
p 修改後指向: 000000000062FE10
b 的值: 20

```
- p單層指標可以用來讀取或修改另一個變數的數值(Call By Address),但是無法改變p單層指標中儲存的a變數的記憶體位址空間。
- 雙層指標儲存的是p單層指標本身的記憶體位址，它允許修改p單層指標的內容（即其儲存的地址）。
- 修改後的變化已經體現在記憶體中，無需回傳更新的目標變數地址或數值。
- 節點和一般簡單變數的差異
- 節點可以用來動態分配簡單變數的記憶體空間。
- 一般的簡單變數如整數或浮點數都是靜態需告的,除非使用指標去動態修改其記憶體位址。
- **甚麼時候需要使用單層指標?**
- 單層指標是用來對資料`Read`和`Write`
- **甚麼時候需要使用雙重層指標?**
- 當需要改變每個結構體時`change memory address spaces`
## 鏈結串列製作流程
- **Create linked list 建立鏈結串列**:初始化鏈結串列(0-1)
```
head -> NULL
```
- **Add Node新增節點**:在create完成後的鏈結串列之後再加入新的節點
```
head -> 10 -> NULL
```
- Add了第二個的時候
```
head -> 	10     ->     20        ->   NULL
          First:1001        Second:1005
        (memory address)  (memory address)
```
## 程式碼編寫
- 使用struct定義結構方便後續使用結構體
	```
	struct node {
		int data;
		struct node* next_mem;
	};
	```
- 主程式初始化head

	- 正確寫法
	```
	int main(){
		//初始化linked list的head
 		//只要是使用struct定義新的結構運算變數就一定要加上struct node*
		struct node* head = NULL;
 		//這邊是return NULL回傳空的數值
		return 0;
 
	}
	```
	- 為甚麼要初始化head?因為如果沒有head,linked list將無法借助任何指標當作起點來輸入數據,沒有這個將會顯示錯誤
	```
	[ERROR] 'head' was not declared in this scope
	```
- 定義一個新增節點的函數
	- 程式碼重點:只要會用到結構體的變數一定要用struct
	 ```
 	struct node* [variable]
	```
  	- 一定要想清楚適用原本的指標還是搜尋後已經更新的指標
  	```
   	*head = newnode; or temp->next = newnode;
   	```
	- 如果head指向的下一個位址為NULL則新增結點到head後面,反之就一直往下搜尋node值到最後一個node的指向位址為NULL
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
			//搜尋到最後一個node->next指標為NULL的時候就加入新節點
 			//一定要將temp的指向下一個位址的位址值傳給newnode,這樣節點的位址才會更新
			temp->next = newnode;	
		}
	
	}
	```
 	- 如果`temp->next = newnode`改成 `*head = newnode`會變成就算head後面已經有新節點,如果還是設定`*head = newnode`的話,每次都只會取代掉head後面的節點,並不會在head後面的尾端又再新增節點
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
- 列印linked list
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
 - 主程式呼叫
	```
	int main(){
		//使用struct定義linked list的初始值, `struct node* [argunment] = NULL;`
		struct node* head = NULL;
		AddEnd(&head,10);
		AddEnd(&head,20);
		AddEnd(&head,30);
		PrintList(head);
		return 0;
	} 
	```
 - 輸出結果
	```
	10  --->   20  --->   30  --->   NULL
	```
 - 練習:建立一鏈結串列, 有三個節點, 其值分別為24,36,48
 - 程式碼:
	```
	#include<stdio.h>
	#include<stdlib.h>
	struct node {
		//定義linked list結構 
		int data;
		struct node* next;
	} node;
	struct node* createnode(int node_data){
		struct node* newnode = (struct node*)malloc(sizeof(struct node));
		if(newnode==NULL){
			printf("Memory Allocation Failed!");
			exit(1);
		}
		newnode->data = node_data;
		newnode->next = NULL;
		return newnode;
	}
	int addnode(struct node** head,int node_data){
		struct node* newnode = createnode(node_data);
		if(*head == NULL){
		//如果加入新節點 
		*head = newnode;
		}else{
			//找到最後一個節點並加入新節點
			struct node* temp = *head;
			while(temp->next!=NULL){
				temp = temp->next;
			} 
			temp->next = newnode;
			//*head = newnode;
		}
	
	}
	int printlist(struct node* head){
		struct node* temp = head;
		printf("head   --->   ");
		while(temp != NULL){
			printf("%d   --->   ", temp->data); 
			temp = temp->next; 
		}
		printf("NULL\n");
	}
	int main(){
		//初始化linked list  
		struct node* head = NULL;
		int i;
		while(i!=5){
				printf("Description:\n1: Add node in the end;\n2: To see the list;\n3: Insert a node in the middle of the linked list;\n4: To delete a particular node;\n5: Exist\n");
				printf("\n");
				printf("please insert a num:");
				scanf("%d",&i);
			if(i==1){
				//addnode
				printf("Loading to.....Addnode,please insert data to add node:");
				int insert_data;
				scanf("%d",&insert_data);
				addnode(&head,insert_data);
			}else if(i==2){
				//to see the list
				printf("Loading to.....To see the list\n");
				printf("Linked list:");
				printlist(head);
			}else if(i==3){
				//Insert a node in the middle of the linked list
				printf("Loading to.....Insert a node in the middle of the linked list\n");
			}else if(i==4){
				//To delete a particular node
				printf("Loading to.....To delete a particular node\n");
			}else if (i==5){
				//Exist
				printf("Existing....\n");
			
			}else{
				printf("Insert Error\n");
			}
			printf("\n");
		}
	
	
		return 0;
	}
	```
 	- 輸出:
   	```
    	
    	Description:
	1: Add node in the end;
	2: To see the list;
	3: Insert a node in the middle of the linked list;
	4: To delete a particular node;
	5: Exist

	please insert a num:1
	Loading to.....Addnode,please insert data to add node:24

	Description:
	1: Add node in the end;
	2: To see the list;
	3: Insert a node in the middle of the linked list;
	4: To delete a particular node;
	5: Exist

	please insert a num:1
	Loading to.....Addnode,please insert data to add node:36

	Description:
	1: Add node in the end;
	2: To see the list;
	3: Insert a node in the middle of the linked list;
	4: To delete a particular node;
	5: Exist

	please insert a num:1
	Loading to.....Addnode,please insert data to add node:48

	Description:
	1: Add node in the end;
	2: To see the list;
	3: Insert a node in the middle of the linked list;
	4: To delete a particular node;
	5: Exist

	please insert a num:2
	Loading to.....To see the list
	Linked list:head   --->   24   --->   36   --->   48   --->   NULL

	Description:
	1: Add node in the end;
	2: To see the list;
	3: Insert a node in the middle of the linked list;
	4: To delete a particular node;
	5: Exist

	please insert a num:5
	Existing....


	--------------------------------
	Process exited after 20.46 seconds with return value 0
   	```
- 包含insert功能的linked list
```
#include<stdio.h>
#include<stdlib.h>
struct node {
	//定義linked list結構 
	int data;
	struct node* next;
} node;
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
struct node* createnode(int node_data){
	struct node* newnode = (struct node*)malloc(sizeof(struct node));
	if(newnode==NULL){
		printf("Memory Allocation Failed!");
		exit(1);
	}
	newnode->data = node_data;
	newnode->next = NULL;
	return newnode;
}
int addnode(struct node** head,int node_data){
	struct node* newnode = createnode(node_data);
	if(*head == NULL){
	//如果加入新節點 
	*head = newnode;
	}else{
		//找到最後一個節點並加入新節點
		struct node* temp = *head;
		while(temp->next!=NULL){
			temp = temp->next;
		} 
		temp->next = newnode;
		//*head = newnode;
	}

}
int printlist(struct node* head){
	struct node* temp = head;
	printf("head   --->   ");
	while(temp != NULL){
		printf("%d   --->   ", temp->data); 
		temp = temp->next; 
	}
	printf("NULL\n");
}
int main(){
	//初始化linked list  
	struct node* head = NULL;
	int i;
	while(i!=5){
			printf("Description:\n1: Add node in the end;\n2: To see the list;\n3: Insert a node in the middle of the linked list;\n4: To delete a particular node;\n5: Exist\n");
			printf("\n");
			printf("please insert a num:");
			scanf("%d",&i);
		if(i==1){
			//addnode
			printf("Loading to.....Addnode,insert data:");
			int insert_data;
			scanf("%d",&insert_data);
			addnode(&head,insert_data);
		}else if(i==2){
			//to see the list
			printf("Loading to.....To see the list\n");
			printf("Linked list:");
			printlist(head);
		}else if(i==3){
			//Insert a node in the middle of the linked list
			printf("Loading to.....Insertnode\n");
			int node_target;
			int node_insert_value;
			printf("choose a value of node to insert:");
			scanf("%d",&node_target);
			printf("insert data you want:");
			scanf("%d",&node_insert_value);
			insertnode(head,node_target,node_insert_value);
		}else if(i==4){
			//To delete a particular node
			printf("Loading to.....To delete a particular node\n");
		}else if (i==5){
			//Exist
			printf("Existing....\n");
		
		}else{
			printf("Insert Error\n");
		}
		printf("\n");
	}


	return 0;
}
```
- 輸出
```
Description:
1: Add node in the end;
2: To see the list;
3: Insert a node in the middle of the linked list;
4: To delete a particular node;
5: Exist

please insert a num:1
Loading to.....Addnode,insert data:2

Description:
1: Add node in the end;
2: To see the list;
3: Insert a node in the middle of the linked list;
4: To delete a particular node;
5: Exist

please insert a num:1
Loading to.....Addnode,insert data:5

Description:
1: Add node in the end;
2: To see the list;
3: Insert a node in the middle of the linked list;
4: To delete a particular node;
5: Exist

please insert a num:1
Loading to.....Addnode,insert data:6

Description:
1: Add node in the end;
2: To see the list;
3: Insert a node in the middle of the linked list;
4: To delete a particular node;
5: Exist

please insert a num:1
Loading to.....Addnode,insert data:7

Description:
1: Add node in the end;
2: To see the list;
3: Insert a node in the middle of the linked list;
4: To delete a particular node;
5: Exist

please insert a num:1
Loading to.....Addnode,insert data:8

Description:
1: Add node in the end;
2: To see the list;
3: Insert a node in the middle of the linked list;
4: To delete a particular node;
5: Exist

please insert a num:1
Loading to.....Addnode,insert data:9

Description:
1: Add node in the end;
2: To see the list;
3: Insert a node in the middle of the linked list;
4: To delete a particular node;
5: Exist

please insert a num:2
Loading to.....To see the list
Linked list:head   --->   2   --->   5   --->   6   --->   7   --->   8   --->   9   --->   NULL

Description:
1: Add node in the end;
2: To see the list;
3: Insert a node in the middle of the linked list;
4: To delete a particular node;
5: Exist

please insert a num:3
Loading to.....Insertnode
choose a value of node to insert:2
insert data you want:3

Description:
1: Add node in the end;
2: To see the list;
3: Insert a node in the middle of the linked list;
4: To delete a particular node;
5: Exist

please insert a num:2
Loading to.....To see the list
Linked list:head   --->   2   --->   3   --->   5   --->   6   --->   7   --->   8   --->   9   --->   NULL

Description:
1: Add node in the end;
2: To see the list;
3: Insert a node in the middle of the linked list;
4: To delete a particular node;
5: Exist

please insert a num:
```
- 製作刪除節點的函數:
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
Seccesfully insert data:7
1: CREATE NEW NODE;
2:INSERT NEWNODE IN PARTICIPATION;
3: TO CHECK LINKED LIST;
4:DELETE NODE PARTICIPATELY;
5: LEAVE
Insert num:1
loading to createnode.
insert data to create node:8
Seccesfully insert data:8
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
### 雙向鏈結串列習題



