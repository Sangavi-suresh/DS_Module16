# Ex16 AVL Tree - Insertion
## DATE:
## AIM:
To write a C function to insert the elements in an AVL Tree.

## Algorithm
1.Start the program
2.Define structure for AVL node (data, left, right, height)
3.Insert element like BST insertion
4.Update height of the node
5.Calculate balance factor
6.Perform rotations if unbalanced:
7.Left Rotation
8.Right Rotation
9.Left-Right Rotation
10.Right-Left Rotation
11.Display tree using inorder traversal
12.Stop   

## Program:
```
/*
Program to insert elements in AVL Tree
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

// Get height
int height(struct node *n)
{
    if(n == NULL)
        return 0;
    return n->height;
}

// Max of two numbers
int max(int a, int b)
{
    return (a > b) ? a : b;
}

// Create new node
struct node* newNode(int data)
{
    struct node* node = (struct node*)malloc(sizeof(struct node));
    node->data = data;
    node->left = node->right = NULL;
    node->height = 1;
    return node;
}

// Right rotation
struct node* rightRotate(struct node* y)
{
    struct node* x = y->left;
    struct node* T2 = x->right;

    x->right = y;
    y->left = T2;

    y->height = max(height(y->left), height(y->right)) + 1;
    x->height = max(height(x->left), height(x->right)) + 1;

    return x;
}

// Left rotation
struct node* leftRotate(struct node* x)
{
    struct node* y = x->right;
    struct node* T2 = y->left;

    y->left = x;
    x->right = T2;

    x->height = max(height(x->left), height(x->right)) + 1;
    y->height = max(height(y->left), height(y->right)) + 1;

    return y;
}

// Get balance factor
int getBalance(struct node* n)
{
    if(n == NULL)
        return 0;
    return height(n->left) - height(n->right);
}

// Insert into AVL
struct node* insert(struct node* node, int data)
{
    if(node == NULL)
        return newNode(data);

    if(data < node->data)
        node->left = insert(node->left, data);
    else if(data > node->data)
        node->right = insert(node->right, data);
    else
        return node;

    node->height = 1 + max(height(node->left), height(node->right));

    int balance = getBalance(node);

    // Left Left
    if(balance > 1 && data < node->left->data)
        return rightRotate(node);

    // Right Right
    if(balance < -1 && data > node->right->data)
        return leftRotate(node);

    // Left Right
    if(balance > 1 && data > node->left->data)
    {
        node->left = leftRotate(node->left);
        return rightRotate(node);
    }

    // Right Left
    if(balance < -1 && data < node->right->data)
    {
        node->right = rightRotate(node->right);
        return leftRotate(node);
    }

    return node;
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
    struct node* root = NULL;

    root = insert(root, 10);
    root = insert(root, 20);
    root = insert(root, 30);
    root = insert(root, 40);
    root = insert(root, 50);
    root = insert(root, 25);

    printf("Inorder Traversal of AVL Tree:\n");
    inorder(root);

    return 0;
}
```

## Output:
<img width="508" height="297" alt="image" src="https://github.com/user-attachments/assets/4419d0ab-29f5-4b2d-82a5-0c1208ad9715" />



## Result:
Thus, the function to insert the elements in an AVL Tree is implemented successfully in C programming language.
