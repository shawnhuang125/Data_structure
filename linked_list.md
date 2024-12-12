# Linked List鏈結串列
> 鏈結串列主要分為四個步驟

> create-->add-->insert-->delete

> create是從0到1去建立鏈結串列

> add是已經在1(初始化鏈結串列)之後要加入新的節點

> insert是在已經建立完的鏈結串列之下,指定節點去加入新節點

> delete是刪除已經建立好的鏈結串列裡面的指定節點

> 像這種鏈結串列需要用到雙重指標,因為他是先使用指標先製作一個串列,再讓每個節點都帶上一個位址。
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

