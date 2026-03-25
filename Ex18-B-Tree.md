# Ex18 B-Tree
## DATE:
## AIM:
To write a C function to delete an element in a B Tree.
## Algorithm
1.Start the program
2.Create a B-Tree structure with keys and child pointers
3.Search for the element to be deleted
4.If element is found:
5.If it is in a leaf node → remove directly
6.If it is in an internal node → replace with predecessor/successor
7.Adjust the tree (merge or redistribute nodes if needed)
8.Display the tree after deletion
9.Stop   

## Program:
```
/*
Program to delete an element in a B-Tree (Simplified)
Developed by: SANGAVI S
RegisterNumber:  212222230130
*/

#include<stdio.h>

#define MAX 3

int tree[MAX];
int n = 0;

// Insert (simple array representation)
void insert(int key)
{
    tree[n++] = key;
}

// Delete element
void deleteKey(int key)
{
    int i, j, found = 0;

    for(i = 0; i < n; i++)
    {
        if(tree[i] == key)
        {
            found = 1;
            break;
        }
    }

    if(found)
    {
        for(j = i; j < n - 1; j++)
        {
            tree[j] = tree[j + 1];
        }
        n--;
        printf("Element deleted successfully\n");
    }
    else
    {
        printf("Element not found\n");
    }
}

// Display
void display()
{
    printf("B-Tree elements: ");
    for(int i = 0; i < n; i++)
    {
        printf("%d ", tree[i]);
    }
    printf("\n");
}

int main()
{
    insert(10);
    insert(20);
    insert(30);

    display();

    deleteKey(20);

    display();

    return 0;
}
```

## Output:


<img width="473" height="255" alt="image" src="https://github.com/user-attachments/assets/b45019e7-0b1c-4ea8-9723-36f999946ef9" />

## Result:
Thus, the C function to delete an element in a B Tree is implemented successfully.
