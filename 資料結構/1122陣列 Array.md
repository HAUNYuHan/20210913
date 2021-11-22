# 陣列 Array
```
缺點一:
因記憶體破碎, 雖記憶體空間足夠, 但沒有足夠的連續記憶體空間, 而無法放置
缺點二:
當陣列宣告完成時, 記憶體空間配置就固定無法再調整
缺點三:
陣列空間管理不易
```
# 單向鏈結串列(Single Linked List)程式碼
```

SingleLinklist.h\\\\\\\\\\\\\\\\\\\
struct node* Createnode(struct node*, int);
struct node* Add(struct node*, int);
struct node* Insertnode(struct node*, int, int);
struct node* Delete(struct node*, int);
struct node* Show(struct node*);

SingleLinklist.cpp\\\\\\\\\\\\\\\\\\\
#include "stdio.h"
#include "stdlib.h"
#include "SingleLinklist.h"

struct node{
		struct node* next=NULL;
		int data;
	};
static struct node* header;

int main(){
	int s=0, value, number;
	header = NULL;
	while(s!=5){
		printf("1. Add a new element, 2. Insert a new element, 3. Delete an element, 4. Show the list, 5. Exit\n");
		scanf("%d",&s);
		if(s==1){
			printf("Input the element:");
			scanf("%d", &value);
			if(header == NULL){
				header = Createnode(header, value);
			}
			else header = Add(header, value);
		}
		if(s==2){
			printf("Input the number of the new node:");
			scanf("%d", &number);
			printf("Input the data of the new node:");
			scanf("%d", &value);
			header = Insertnode(header, number, value);
		}
		if(s==3){
			printf("Delete the element:");
			scanf("%d", &value);
			header = Delete(header, value);
		}
		if(s==4){
			header = Show(header);
		}
	}
	return 0;	
}


struct node* Createnode(struct node* header, int value){
	header = (struct node*)malloc(sizeof(struct node));
	if(header == NULL) return NULL;
	header->data = value;
	header->next = NULL;
	return header;
}

struct node* Add(struct node* header, int value){
	struct node* current;
	current = header;
	while(current->next != NULL){
		current = current->next;
	}	
	current->next = (struct node*)malloc(sizeof(struct node));
	current->next->data = value;
	current->next->next = NULL;
	return header;
}

struct node* Insertnode (struct node* header, int number, int value){
	struct node* current;
	struct node* nextnode;
	current = header;
	if(number==1){
		header = (struct node*)malloc(sizeof(struct node));
		header->data = value;
		header->next = current;
	}
	else{
		for(int i=1; i<= number-1; i++){
			current = current->next;
		}
		nextnode = current->next;
current->next = (struct node*)malloc(sizeof(struct node));
		current->next->data = value;
		current->next->next = nextnode;
	}
	return header;
}

struct node* Delete(struct node* header, int value){
	struct node* current;
	struct node* currentpri;
	current = header;
	while(current->data != value){
		currentpri = current;
		current = current->next;
	}
	if (current == header){
		header = current->next;
	}
	else{
		currentpri->next = current->next;
	}
	free(current);
	return header;
}

struct node* Show(struct node* header){
	struct node* current;
	current = header;
	while(current!=NULL){
		printf("%d, ", current->data);
		current = current->next;
	}
	printf("\n");
	return header;
}
```
# 單向鏈結串列(Single Linked List)程式碼說明:
```
宣告節點node的結構
struct node{
		struct node* next=NULL; 
//指向下一個節點node的指標, , 初始預設為空指標 NULL
		int data;
		//節點node的資料值
	};

宣告node的靜態指標 header, 用來指向第一個節點, 初始預設為空指標 NULL
static struct node* header;
header = NULL;


while(s!=4){ //當使用者輸入選項為4, 跳出迴圈
		printf("1. Add a new element, 2. Delete an element, 3. Show the list, 4. Exit\n");
		scanf("%d",&s); //使用者輸入選項
		if(s==1){ //當使用者輸入選項為1
			printf("Input the element:");
			scanf("%d", &value); //使用者輸入節點的值存入變數value中
			if(header == NULL){ 
//當header指標為空指標, 表示串列沒有任何節點
				header = createnode(header, value);
				//呼叫建立節點的函式, 並將header與value傳入函式
				//當函式建立節點後, 會將結點位址傳入 header指標
			}
			else header = Add(header, value);
			//當header指標不為空指標, 表示串列已有節點
//header指向第一個節點
//呼叫加入節點的函式, 並將header與value傳入函式
		}
		if(s==2){ //當使用者輸入選項為2
			printf("Delete the element:");
			scanf("%d", &value); //使用者輸入要刪除的值到變數value中
			header = Delete(header, value);
			//呼叫刪除節點的函式, 並將header與value傳入函式
		}
		if(s==3){ //當使用者輸入選項為3
			header = Show(header);
			//呼叫印出所有節點值的函式, 並將header傳入函式
		}
	}

建立節點

struct node* createnode(struct node* header, int value){
	header = (struct node*)malloc(sizeof(struct node));
	//在記憶體配置struct node大小的記憶體空間,並把位址傳給header
	if(header == NULL) return NULL;
	//若header的值是NULL, 則表示配置失敗, 函式結束, 回傳NULL
	header->data = value;
	//將value的值是存放在header位址的data欄位
	header->next = NULL;
	//將header位址的next欄位設為NULL
	return header;
	//函式結束, 回傳header位址
}

加入節點
struct node* Add(struct node* header, int value){
	struct node* current;
	current = header;
	while(current->next != NULL){
		current = current->next;
	}//找出在鏈結串列中最後一個節點,並把位址傳給current
	current->next = (struct node*)malloc(sizeof(struct node));
	//在記憶體配置記憶體空間給node,並把位址傳給current中的next欄位
	current->next->data = value;
	//將value的值是存放在current->next位址的data欄位
	current->next->next = NULL;
	//將current->next位址的next欄位設為NULL
	return header;
	//函式結束, 回傳header位址
}
 

插入節點
struct node* Insertnode (struct node* header, int number, int value){
	struct node* current;
	struct node* nextnode;
	current = header;
	if(number==1){
		header = (struct node*)malloc(sizeof(struct node));
		header->data = value;
		header->next = current;
	}//若要插入為第一個節點, 記憶體配置的記憶體空間位置傳給header
//並把原先第一個節點位址傳給第一個節點的next欄位
	else{
		for(int i=2; i<= number-1; ++i){
			current = current->next;
		}//找出要插入節點的前一個節點, 並把其記憶體位址傳給current
		nextnode = current->next;
		//要插入節點的下一個節點記憶體位址傳給nextnode
		current->next = (struct node*)malloc(sizeof(struct node));
		//記憶體配置的記憶體空間位置傳給前一個節點的next欄位
		current->next->data = value;
		//把值存入新配置節點的data欄位
		current->next->next = nextnode;
		//下一個節點記憶體位址存入新配置節點的next欄位
	}
	return header;
}

 


刪除節點
struct node* Delete(struct node* header, int value){
	struct node* current;
	struct node* currentpri;
	current = header;
	while(current->data != value){
		currentpri = current;
		current = current->next;
	}//從第一個節點依序找出要刪除的節點
	//current指標指向要刪除節點的位址
//currentpri指標指向要刪除節點的前一個節點位址
	if (current == header){
		header = current->next;
	}//若要刪除的是第一個節點, header指標指向第一個節點的下個節點位址
	else{
		currentpri->next = current->next;
	}//把要刪除節點的上一個節點的next指標指向要刪除節點的下個節點位址
	free(current);
	//把要刪除的節點從記憶體清除
	return header;
	//函式結束, 回傳header位址
}

 ![image](https://user-images.githubusercontent.com/71476327/142787797-286789ff-bbbe-4c61-9b40-81f0e9336ebe.png)



顯示串列所有節點的資料值
struct node* Show(struct node* header){
	struct node* current;
	current = header;
	while(current!=NULL){
		printf("%d, ", current->data);
		current = current->next;
	}//依序顯示串列中每個節點資料欄位地值
	printf("\n");
	return header;
}
```
# 雙向鏈結串列(Doubly Linked List)
```
雙向鏈結串列(doubly linked list)乃是每個節點皆具有三個欄位，
左鏈結（LLINK）, 資料（DATA）,右鏈結（RLINK）

struct node{
		struct list* pri=NULL;
		struct list* next=NULL;
		int data;
	};
```
# 雙向鏈結程式碼
```
DLinklist.h\\\\\\\\\\\\\\\\\\\
struct node* createnode(struct node*, int);
struct node * Add(struct node*, int);
struct node * Delete(struct node*, int);
struct node * Show(struct node*);

DLinklist.cpp\\\\\\\\\\\\\\\\\\\
#include "stdio.h"
#include "stdlib.h"
#include "DLinklist.h"

struct node{
		struct node* pri=NULL;
		struct node* next=NULL;
		int data;
	};
static struct node* header;

int main(){
	int s=0, value;
	header = NULL;
	while(s!=4){
		printf("1. Add a new element, 2. Delete an element, 3. Show the list, 4. Exit\n");
		scanf("%d",&s);
		if(s==1){
			printf("Input the element:");
			scanf("%d", &value);
			if(header == NULL){
				header = createnode(header, value);
			}
			else header = Add(header, value);
		}
		if(s==2){
			printf("Delete the element:");
			scanf("%d", &value);
			header = Delete(header, value);
		}
		if(s==3){
			header = Show(header);
		}
	}
	return 0;	
}


struct node* createnode(struct node* header, int value){
	header = (struct node *)malloc(sizeof(struct node));
	if(header == NULL) return NULL;
	header->data = value;
	header->next = NULL;
	header->pri = NULL;
	return header;
}

struct node * Add(struct node * header, int value){
	struct node * current;
	current = header;
	while(current->next != NULL){
		current = current->next;
	}	
	current->next = (struct node *)malloc(sizeof(struct node));
	current->next->data = value;
	current->next->pri = current;
	current->next->next = NULL;
	return header;
}

struct node * Delete(struct node * header, int value){
	struct node * current;
	current = header;
	while(current->data != value){
		current = current->next;
	}
	if (current->pri == NULL){
		header = current->next;
		header->pri = NULL;
		header->next = current->next->next;
		
	}
	else{
		current->pri->next = current->next;
		current->next->pri = current->pri;
	}
	free(current);
	return header;
}

struct node * Show(struct node * header){
	struct node * current;
	current = header;
	while(current!=NULL){
		printf("%d, ", current->data);
		current = current->next;
	}
	printf("\n");
	return header;
}

```
