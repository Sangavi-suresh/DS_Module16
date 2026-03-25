# Ex19 B+ Tree
## DATE:
## AIM:
To write a C function to traverse the elements in a B+ Tree.

## Algorithm
1.Start the program
2.Create a B+ Tree node structure (keys and child pointers)
3.Insert elements into leaf nodes (simplified representation)
4.Link leaf nodes for sequential access
5.Traverse starting from the leftmost leaf node
6.Print all elements in order
7.Stop   

## Program:
```
/*
Program to traverse elements in a B+ Tree (Simplified)
Developed by: SANGAVI S
RegisterNumber:  212222230130
*/

#include<stdio.h>

#define MAX 5

int leaf[MAX];
int n = 0;

// Insert into leaf (sorted)
void insert(int key)
{
    int i = n - 1;

    while(i >= 0 && leaf[i] > key)
    {
        leaf[i + 1] = leaf[i];
        i--;
    }

    leaf[i + 1] = key;
    n++;
}

// Traverse (sequential access like B+ Tree leaf nodes)
void traverse()
{
    printf("B+ Tree Traversal: ");
    for(int i = 0; i < n; i++)
    {
        printf("%d ", leaf[i]);
    }
    printf("\n");
}

int main()
{
    insert(30);
    insert(10);
    insert(50);
    insert(20);
    insert(40);

    traverse();

    return 0;
}
```

## Output:

<img width="545" height="284" alt="image" src="https://github.com/user-attachments/assets/c0527463-a76d-4f45-958d-4a00e9d79b59" />


## Result:
Thus, the function to traverse the elements in a B+ Tree is implemented successfully.
