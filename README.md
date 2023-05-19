#include <stdio.h>
#include <stdlib.h>

/*__________________________________________________________________________*/

// Linked List Node
typedef struct node
{
    int Data;
    struct node *Next;
} node; // end of struct

/*__________________________________________________________________________*/

typedef node *LinkedList;
typedef node *Node;

/*__________________________________________________________________________*/

LinkedList MakeEmpty(LinkedList ist);
int IsEmpty(LinkedList tmp);
int IsLast(Node tmp, LinkedList list);
Node Find(int z, LinkedList list);
void Delete(int z, LinkedList list);
Node FindPrevious(int z, LinkedList list);
void Insert(int z, LinkedList list, Node pre);
void PrintList(LinkedList list);
void DeleteList(LinkedList list);
int Size(LinkedList list);

/*__________________________________________________________________________*/

int main(void)
{
    
} // end of main()

/*__________________________________________________________________________*/

LinkedList MakeEmpty(LinkedList list)
{
    if (list != NULL)
    {
        DeleteList(list);
    } // end if()
    list = malloc(sizeof(node));
    if (list == NULL)
    {
        printf("The Memory Is Full");
        return NULL;
    }
    list->Next = NULL;
    return list;
} // end of MakeEmpty()

/*__________________________________________________________________________*/

int IsEmpty(LinkedList tmp)
{
    return tmp->Next == NULL;
} // end of IsEmpty()

/*__________________________________________________________________________*/

int IsLast(Node tmp, LinkedList list)
{
    return tmp->Next == NULL;
} // end of IsLast()

/*__________________________________________________________________________*/

Node Find(int z, LinkedList list)
{
    Node tmp = list->Next;

    while (tmp != NULL && tmp->Data != z)
    {   
        tmp = tmp->Next;
    } // end of while()
    return tmp;
} // end of Find()

/*__________________________________________________________________________*/

Node FindPrevious(int z, LinkedList list)
{
    Node tmp = list;
    while (tmp->Next != NULL && tmp->Next->Data != z)
    {
        tmp = tmp->Next;
    } // end of while()
    return tmp;
} // end of FindPrevious()

/*__________________________________________________________________________*/

void Delete(int z, LinkedList list)
{
    Node pre, tmp;
    pre = FindPrevious(z, list);

    if (!IsLast(pre, list))
    {
        tmp = pre->Next;
        pre->Next = tmp->Next;
        free(tmp);
    } // end of if()
    else
    {
        printf("\"%d\" Is Not Found!", z);
    } // end of else
} // end of Delete()

/*__________________________________________________________________________*/

void Insert(int z, LinkedList list, Node pre)
{
    Node tmp = malloc(sizeof(node));
    if (tmp == NULL)
    {
        printf("The Memory Is Full");
        return;
    } // end of if()
    tmp->Data = z;
    tmp->Next = pre->Next;
    pre->Next = tmp;
} // end of Insert()

/*__________________________________________________________________________*/

void PrintList(LinkedList list)
{
    Node tmp = list;
    if (IsEmpty(list))
    {
        printf("Is Empty List!\n\n");
        return;
    } // end of if()
    do
    {
        tmp = tmp->Next;
        printf("%d => ", tmp->Data);
    } while (!IsLast(tmp, list));
    printf("\n");
} // end of PrintList()

/*__________________________________________________________________________*/

void DeleteList(LinkedList list)
{
    Node post, tmp;
    post = list;
    while (post != NULL)
    {
        tmp = post->Next;
        free(post);
        post = tmp;
    } // end of while()
} // end of DeleteList()

/*__________________________________________________________________________*/

int Size(LinkedList list)
{
    Node tmp = list;
    int size = 0;
    while (tmp->Next != NULL)
    {
        tmp = tmp->Next;
        size++;
    } // end of while()
    return size;
} // end of Size()

/*__________________________________________________________________________*/

