# Ex17 AVL Tree – Rotation
## DATE:
## AIM:
To write a C function to perform right rotation in an AVL Tree.

## Algorithm
1.Start the program
2.Define structure for AVL node (data, left, right, height)
3.Create nodes for AVL tree
4.Identify the unbalanced node (Left-Left case)
5.Perform right rotation:
6.Make left child as new root
7.Move right subtree of left child to left of original root
8.Update heights of nodes
9.Display inorder traversal
10.Stop  

## Program:
```
/*
Program to perform right rotation in AVL Tree
Developed by: SANGAVI S
RegisterNumber:  212222230130
*/

#include<stdio.h>
#include<stdlib.h>

struct node
{
    int data;
    struct node *left, *right;
    int height;
};

// Utility functions
int max(int a, int b)
{
    return (a > b) ? a : b;
}

int height(struct node *n)
{
    if(n == NULL)
        return 0;
    return n->height;
}

// Create node
struct node* newNode(int data)
{
    struct node* node = (struct node*)malloc(sizeof(struct node));
    node->data = data;
    node->left = node->right = NULL;
    node->height = 1;
    return node;
}

// Right Rotation
struct node* rightRotate(struct node* y)
{
    struct node* x = y->left;
    struct node* T2 = x->right;

    // Rotation
    x->right = y;
    y->left = T2;

    // Update heights
    y->height = max(height(y->left), height(y->right)) + 1;
    x->height = max(height(x->left), height(x->right)) + 1;

    return x;
}

// Inorder traversal
void inorder(struct node* root)
{
    if(root != NULL)
    {
        inorder(root->left);
        printf("%d ", root->data);
        inorder(root->right);
    }
}

int main()
{
    struct node* root;

    // Creating unbalanced tree (Left-Left case)
    root = newNode(30);
    root->left = newNode(20);
    root->left->left = newNode(10);

    printf("Before Rotation (Inorder):\n");
    inorder(root);

    // Perform right rotation
    root = rightRotate(root);

    printf("\nAfter Right Rotation (Inorder):\n");
    inorder(root);

    return 0;
}
```

## Output:


<img width="487" height="287" alt="image" src="https://github.com/user-attachments/assets/89a26280-9009-48c9-a49c-14dacebacfe2" />

## Result:
Thus, the function to perform right rotation in an AVL Tree is implemented successfully.
