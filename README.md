# Assignment1
#include<iostream>
#include<string.h>
using namespace std;

struct node
{
  int v;
node* next;
}*HashTable[10];	//create hash table of size 10

class hashing
{   
public:
hashing()			// constructor of hashing class
{
for(int i=0 ; i<10 ; i++)  //initializaton
{
        HashTable[i]=NULL;	 // assign null value to hash table
    }
 }

int HashFunction(int v)
{
  return (v%10);   //division method used
 }
 node* create_node(int x)   //  create node
{
     node* temp=new node;
    temp->next=NULL;
    temp->v=x;
    return temp;
 }

 void display()
{
     for(int i=0 ; i< 10; i++)
{
        node * temp=new node;
        temp=HashTable[i];
        cout<<"a["<<i<<"] : ";
        while(temp !=NULL)
{
                cout<<" ->"<<temp->v;
                temp=temp->next;
         }
        cout<<"\n";
}
 }
//for searching 
int searchElement(int v)
{
     bool flag = false;
              int hash_val = HashFunction(v);
              node* entry = HashTable[hash_val];
              cout<<"\nElement found at : ";
              while (entry != NULL)
         {
                    if (entry->v==v)
                 {
                            cout<<hash_val<<" : "<<entry->v<<endl;
                            flag = true;
                     }
                    entry = entry->next;
              }
              if (!flag)
              return -1;
 }
//for deletion
 void deleteElement(int v)
{
     int hash_val = HashFunction(v);	//find the index of v using hashfunction
              node* entry = HashTable[hash_val];
              if (entry == NULL )	// no element is present 
              {
                 cout<<"No Element found ";
                      return;
              }

              if(entry->v==v)
{
                HashTable[hash_val]=entry->next;	//link pointer to next 
                return;
              }
              while ((entry->next)->v != v)
        {
                  entry = entry->next;
              }
              entry->next=(entry->next)->next;
 }

 //for insertion
 void insertElement(int v)
{
     int hash_val = HashFunction(v);	//index of v using hashfunction
              node* temp=new node;		//create temporary node
              node* head=new node;		//create head node
              head = create_node(v); //create node to be inseted as head node
              temp=HashTable[hash_val];//position element in hashtable
              if (temp == NULL)		
                               {
                              HashTable[hash_val] =head; //if temp null then insert head node in that position
                               }
              else
{
                 while (temp->next != NULL)	//traverse the hashtable until we get null
                {
                      temp = temp->next;
                   }    
                     temp->next =head;  	// when found null then insert head node in that position
              }
 }
};

int main()
{
    int ch;		//take choice
 int data,search,del;
    hashing h;	//object
    do
{
cout<<"\nTelephone : \n1.Insert \n2.Display \n3.Search \n4.Delete \n5.Exit";
        cin>>ch;
        switch(ch)
{
            case 1:cout<<"\nEnter phone no. to be inserted : ";
                    cin>>data;
h.insertElement(data);
                 break;
            case 2:h.display();
                    break;
            case 3:cout<<"\nEnter the no to be searched : ";
                    cin>>search;

                 if (h.searchElement(search) == -1)
                            {
                                cout<<"No element found at key ";
                                 continue;
                            }
                    break;
            case 4:cout<<"\nEnter the phno. to be deleted : ";
                 cin>>del;
                 h.deleteElement(del);
                  cout<<"Phno. Deleted"<<endl;
                    break;
                }
        }while(ch!=5);
        return 0;

}
#include <iostream>
using namespace std;

int HT1[10];  // for set A
int HT2[10];  // for set B

int size = 10;

void init()  //initializes Hash Tables
{
    for (int i = 0; i < size; i++)
    {
        HT1[i] = 0;
        HT2[i] = 0;
    }
}

void display()
{
    int i;
    cout << "\n Hash Table No 1";
    cout << "\n Index - Key";
    for (int i = 0; i < size; i++)
    {
        cout << "\n " << i << " \t  " << HT1[i];
    }
    cout << "\n Hash Table No 2";
    cout << "\n Index - Key";
    for (int i = 0; i < size; i++)
    {
        cout << "\n " << i << " \t  " << HT2[i];
    }
}

void insertSetA(int key)
{
    int index;
    index = key % size;

    if(HT1[index]== 0)
    {
        HT1[index] = key;
    }
    else
    {
        index = (key + 1) % size;
        HT1[index] = key;
    }
}

void insertSetB(int key)
{
    int index;
    index = key % size;
    HT2[index] = key;
}

void searchSetA(int key)
{
    int index;
    cout << "\n Searching " << key << " in Set A";
    index = key % size;
    if (HT1[index] == key)
    {
        cout << "\n Key " << key << " Found at :" << index;
    }
    else
    {
        cout << "\n Key " << key << " Not Found";
    }
}

void searchSetB(int key)
{
    int index;
    cout << "\n Searching " << key << " in Set B";
    index = key % size;
    if (HT2[index] == key)
    {
        cout << "\n Key " << key << " Found at :" << index;
    }
    else
    {
        cout << "\n Key " << key << " Not Found";
    }
}

void deleteSetA(int key)
{
    int index;
    cout << "\n Deleting " << key << "From Set A";
    index = key % size;
    if (HT1[index] == key)
    {
        HT1[index] = 0;
        cout << "\n Deleting " << key << " Found at" << index << " and Deleted";
    }
    else
    {
        cout << "\n Key : " << key << " Not Found";
    }
}

void deleteSetB(int key)
{
    int index;
    cout << "\n Deleting " << key << "From Set B";
    index = key % size;
    if (HT2[index] == key)
    {
        HT2[index] = 0;
        cout << "\n Deleting " << key << " Found at" << index << " and Deleted";
    }
    else
    {
        cout << "\n Key : " << key << " Not Found";
    }
}

int dup(int val)
{
    int i, dupl = 0;
    for (i = 0; i < size; i++)
    {
        if (val == HT1[i])
            dupl = 1;
    }
    return dupl;
}

void unionAB()
{
    int i, j;
    int C[10];
    j = 0;
    for (i = 0; i < size; i++)
    {
        if (HT1[i] != 0)   //copy setA in setC
        {
            C[j] = HT1[i];
            j++;
        }
    }
    for (i = 0; i < size; i++)
    {
        if (HT2[i] != 0)  //copy SetA in Set C
        {
            if (dup(HT2[i]) == 0)
            {
                C[j] = HT2[i];
                j++;
            }
        }
    }
    cout << "\n Union of SET-A,B = ";
    for (i = 0; i < j; i++)
        cout << C[i] << ", ";
}

int main()
{
    cout << "\n Initializing the HashTables";
    init();
    display();
    insertSetA(123);
    insertSetA(81);
    insertSetA(63);
    insertSetA(82);
    insertSetA(92);
    insertSetB(69);
    insertSetB(96);
    insertSetB(72);
    cout << "\n After Inserting the values";
    display();
    cout << "\n Searching Values";
    searchSetA(69);
    searchSetB(69);
    cout << "\n Deleting Values";
    deleteSetA(123);
    deleteSetB(96);
    display();
    cout << "\n Union of Set A and B";
    unionAB();
    cout << "\n";
}
