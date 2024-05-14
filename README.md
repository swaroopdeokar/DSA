# DSA
*******************
1) 1.	Write a Program to create a Binary Tree and perform following nonrecursive operations on it. a. Preorder Traversal, b. Postorder Traversal, c. Count total no. of nodes, d. Display height of a tree.
      
#include <stdio.h>
#include <stdlib.h>

struct TreeNode {
    int data;
    struct TreeNode* left;
    struct TreeNode* right;
};

struct TreeNode* createNode(int data) {
    struct TreeNode* newNode = (struct TreeNode*)malloc(sizeof(struct TreeNode));
    if (newNode == NULL) {
        printf("Memory allocation failed\n");
        exit(1);
    }
    newNode->data = data;
    newNode->left = NULL;
    newNode->right = NULL;
    return newNode;
}

void preorderTraversal(struct TreeNode* current) {
    if (current != NULL) {
        printf("%d ", current->data);
        preorderTraversal(current->left);
        preorderTraversal(current->right);
    }
}

void postorderTraversal(struct TreeNode* current) {
    if (current != NULL) {
        postorderTraversal(current->left);
        postorderTraversal(current->right);
        printf("%d ", current->data);
    }
}

int countNodes(struct TreeNode* root) {
    if (root == NULL)
        return 0;

    return 1 + countNodes(root->left) + countNodes(root->right);
}

int max(int a, int b) {
    return (a > b) ? a : b;
}

int height(struct TreeNode* root) {
    if (root == NULL)
        return 0;

    int leftHeight = height(root->left);
    int rightHeight = height(root->right);

    return 1 + max(leftHeight, rightHeight);
}

int main() {
    struct TreeNode* root = NULL;
    char choice;

    do {
        int data;
        struct TreeNode* newNode;

        printf("Enter the data for the new node: ");
        scanf("%d", &data);
        newNode = createNode(data);

        if (root == NULL) {
            root = newNode;
        } else {
            struct TreeNode* current = root;
            while (1) {
                printf("Do you want to insert '%d' to the left or right of '%d' (l/r): ", data, current->data);
                scanf(" %c", &choice);
                if (choice == 'l' || choice == 'L') {
                    if (current->left == NULL) {
                        current->left = newNode;
                        break;
                    } else {
                        current = current->left;
                    }
                } else if (choice == 'r' || choice == 'R') {
                    if (current->right == NULL) {
                        current->right = newNode;
                        break;
                    } else {
                        current = current->right;
                    }
                } else {
                    printf("Invalid choice! Please enter 'L' or 'R'.\n");
                }
            }
        }

        printf("Do you want to insert another node? (Y/N): ");
        scanf(" %c", &choice);
    } while (choice == 'Y' || choice == 'y');

    printf("\nPreorder Traversal: ");
    preorderTraversal(root);
    printf("\nPostorder Traversal: ");
    postorderTraversal(root);
    printf("\nTotal number of nodes: %d\n", countNodes(root));
    printf("Height of the tree: %d\n", height(root));

    return 0;
}
*******************
2)	Write a Program to create a Binary Tree and perform following nonrecursive operations on it. a. inorder Traversal; b. Count no. of nodes on longest path; c. display tree levelwise; d. Display height of a tree.
   
 #include <stdio.h>
#include <stdlib.h>

struct TreeNode {
    int data;
    struct TreeNode* left;
    struct TreeNode* right;
};

struct TreeNode* createNode(int data) {
    struct TreeNode* newNode = (struct TreeNode*)malloc(sizeof(struct TreeNode));
    if (newNode == NULL) {
        printf("Memory allocation failed\n");
        exit(1);
    }
    newNode->data = data;
    newNode->left = NULL;
    newNode->right = NULL;
    return newNode;
}

void inorderTraversal(struct TreeNode* root) {
    struct TreeNode* stack[100];
    int top = -1;
    struct TreeNode* current = root;

    while (current != NULL || top != -1) {
        while (current != NULL) {
            stack[++top] = current;
            current = current->left;
        }
        current = stack[top--];
        printf("%d ", current->data);
        current = current->right;
    }
}

int countNodesLongestPath(struct TreeNode* root) {
    if (root == NULL)
        return 0;

    int leftHeight = height(root->left);
    int rightHeight = height(root->right);

    return 1 + leftHeight + rightHeight;
}

void displayLevelWise(struct TreeNode* root) {
    if (root == NULL)
        return;

    struct TreeNode* queue[100];
    int front = -1, rear = -1;
    queue[++rear] = root;

    while (front != rear) {
        struct TreeNode* current = queue[++front];
        printf("%d ", current->data);
        if (current->left != NULL)
            queue[++rear] = current->left;
        if (current->right != NULL)
            queue[++rear] = current->right;
    }
}

int max(int a, int b) {
    return (a > b) ? a : b;
}

int height(struct TreeNode* root) {
    if (root == NULL)
        return 0;

    int leftHeight = height(root->left);
    int rightHeight = height(root->right);

    return 1 + max(leftHeight, rightHeight);
}

int main() {
    struct TreeNode* root = NULL;
    char choice;

    do {
        int data;
        struct TreeNode* newNode;

        printf("Enter the data for the new node: ");
        scanf("%d", &data);
        newNode = createNode(data);

        if (root == NULL) {
            root = newNode;
        } else {
            struct TreeNode* current = root;
            while (1) {
                printf("Do you want to insert '%d' to the left or right of '%d' (l/r): ", data, current->data);
                scanf(" %c", &choice);
                if (choice == 'l' || choice == 'L') {
                    if (current->left == NULL) {
                        current->left = newNode;
                        break;
                    } else {
                        current = current->left;
                    }
                } else if (choice == 'r' || choice == 'R') {
                    if (current->right == NULL) {
                        current->right = newNode;
                        break;
                    } else {
                        current = current->right;
                    }
                } else {
                    printf("Invalid choice! Please enter 'L' or 'R'.\n");
                }
            }
        }

        printf("Do you want to insert another node? (Y/N): ");
        scanf(" %c", &choice);
    } while (choice == 'Y' || choice == 'y');

    printf("\nInorder Traversal: ");
    inorderTraversal(root);
    printf("\nNumber of nodes on longest path: %d\n", countNodesLongestPath(root));
    printf("Tree levelwise: ");
    displayLevelWise(root);
    printf("\nHeight of the tree: %d\n", height(root));

    return 0;
}

*******************
3) Write a Program to create a Binary Search Tree holding numeric keys and perform following nonrecursive operations on it. a. Levelwise display, b. Mirror image, c. Display height of a tree, d. Find 

