# Ex20 AVL Tree - Deletion
## DATE:
## AIM:
To write a C function to delete an element from an AVL Tree.
## Algorithm
1.Start the program
2.Define AVL node structure (data, left, right, height)
3.Perform deletion like BST:
4.If node has no child → delete directly
5.If one child → replace node with child
6.If two children → replace with inorder successor
7.Update height of the node
8.Calculate balance factor
9.Perform rotations if unbalanced
10.Display tree using inorder traversal
11.Stop   

## Program:
```
/*
Program to delete an element from an AVL Tree
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

struct node* newNode(int data)
{
    struct node* node = (struct node*)malloc(sizeof(struct node));
    node->data = data;
    node->left = node->right = NULL;
    node->height = 1;
    return node;
}

// Rotations
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

int getBalance(struct node* n)
{
    if(n == NULL)
        return 0;
    return height(n->left) - height(n->right);
}

// Find minimum node
struct node* minValueNode(struct node* node)
{
    struct node* current = node;
    while(current->left != NULL)
        current = current->left;
    return current;
}

// Delete node
struct node* deleteNode(struct node* root, int key)
{
    if(root == NULL)
        return root;

    if(key < root->data)
        root->left = deleteNode(root->left, key);
    else if(key > root->data)
        root->right = deleteNode(root->right, key);
    else
    {
        // Node with one or no child
        if((root->left == NULL) || (root->right == NULL))
        {
            struct node *temp = root->left ? root->left : root->right;

            if(temp == NULL)
            {
                temp = root;
                root = NULL;
            }
            else
                *root = *temp;

            free(temp);
        }
        else
        {
            struct node* temp = minValueNode(root->right);
            root->data = temp->data;
            root->right = deleteNode(root->right, temp->data);
        }
    }

    if(root == NULL)
        return root;

    root->height = 1 + max(height(root->left), height(root->right));

    int balance = getBalance(root);

    // Balance cases
    if(balance > 1 && getBalance(root->left) >= 0)
        return rightRotate(root);

    if(balance > 1 && getBalance(root->left) < 0)
    {
        root->left = leftRotate(root->left);
        return rightRotate(root);
    }

    if(balance < -1 && getBalance(root->right) <= 0)
        return leftRotate(root);

    if(balance < -1 && getBalance(root->right) > 0)
    {
        root->right = rightRotate(root->right);
        return leftRotate(root);
    }

    return root;
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

    root = newNode(50);
    root->left = newNode(30);
    root->right = newNode(70);
    root->left->left = newNode(20);
    root->left->right = newNode(40);
    root->right->left = newNode(60);
    root->right->right = newNode(80);

    printf("Before Deletion:\n");
    inorder(root);

    root = deleteNode(root, 50);

    printf("\nAfter Deletion:\n");
    inorder(root);

    return 0;
}
```

## Output:


<img width="528" height="286" alt="image" src="https://github.com/user-attachments/assets/83ae3a7e-c1ae-41aa-8e2b-fcd64af1a7ff" />

## Result:
Thus, the C program to delete an element from an AVL Tree is implemented successfully.
