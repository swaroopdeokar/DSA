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


#include <stdio.h>
#include <stdlib.h>
#include <stdbool.h>

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

void insertNode(struct TreeNode** root, int data) {
    struct TreeNode* newNode = createNode(data);
    if (*root == NULL) {
        *root = newNode;
    } else {
        struct TreeNode* current = *root;
        while (1) {
            if (data < current->data) {
                if (current->left == NULL) {
                    current->left = newNode;
                    break;
                } else {
                    current = current->left;
                }
            } else if (data > current->data) {
                if (current->right == NULL) {
                    current->right = newNode;
                    break;
                } else {
                    current = current->right;
                }
            } else {
                printf("Duplicate keys are not allowed\n");
                free(newNode);
                break;
            }
        }
    }
}

void levelwiseDisplay(struct TreeNode* root) {
    if (root == NULL) {
        printf("Tree is empty\n");
        return;
    }

    struct TreeNode* queue[100];
    int front = -1, rear = -1;
    queue[++rear] = root;

    while (front != rear) {
        int nodesInLevel = rear - front;
        while (nodesInLevel > 0) {
            struct TreeNode* current = queue[++front];
            printf("%d ", current->data);

            if (current->left != NULL)
                queue[++rear] = current->left;
            if (current->right != NULL)
                queue[++rear] = current->right;

            nodesInLevel--;
        }
        printf("\n");
    }
}

void mirrorImage(struct TreeNode* root) {
    if (root == NULL)
        return;

    struct TreeNode* temp = root->left;
    root->left = root->right;
    root->right = temp;

    mirrorImage(root->left);
    mirrorImage(root->right);
}

int height(struct TreeNode* root) {
    if (root == NULL)
        return 0;

    int leftHeight = height(root->left);
    int rightHeight = height(root->right);

    return 1 + (leftHeight > rightHeight ? leftHeight : rightHeight);
}

struct TreeNode* search(struct TreeNode* root, int key) {
    while (root != NULL && root->data != key) {
        if (key < root->data)
            root = root->left;
        else
            root = root->right;
    }
    return root;
}

int main() {
    struct TreeNode* root = NULL;
    int choice, data, key;

    do {
        printf("\n1. Insert\n2. Levelwise Display\n3. Mirror Image\n4. Display Height\n5. Search\n6. Exit\n");
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                printf("Enter data to insert: ");
                scanf("%d", &data);
                insertNode(&root, data);
                break;
            case 2:
                printf("Levelwise Display:\n");
                levelwiseDisplay(root);
                break;
            case 3:
                printf("Mirror Image:\n");
                mirrorImage(root);
                levelwiseDisplay(root);
                break;
            case 4:
                printf("Height of the tree: %d\n", height(root));
                break;
            case 5:
                printf("Enter key to search: ");
                scanf("%d", &key);
                if (search(root, key) != NULL)
                    printf("%d found in the tree.\n", key);
                else
                    printf("%d not found in the tree.\n", key);
                break;
            case 6:
                printf("Exiting...\n");
                break;
            default:
                printf("Invalid choice!\n");
        }
    } while (choice != 6);

    return 0;
}

*******************

4) Write a program to illustrate operations on a BST holding numeric keys. The menu must include: • Insert • Delete • Find • display in Inorder way

#include <stdio.h>
#include <stdlib.h>

struct TreeNode {
    int key;
    struct TreeNode* left;
    struct TreeNode* right;
};

struct TreeNode* createNode(int key) {
    struct TreeNode* newNode = (struct TreeNode*)malloc(sizeof(struct TreeNode));
    if (newNode == NULL) {
        printf("Memory allocation failed\n");
        exit(1);
    }
    newNode->key = key;
    newNode->left = NULL;
    newNode->right = NULL;
    return newNode;
}

struct TreeNode* insertNode(struct TreeNode* root, int key) {
    if (root == NULL)
        return createNode(key);

    if (key < root->key)
        root->left = insertNode(root->left, key);
    else if (key > root->key)
        root->right = insertNode(root->right, key);
    else
        printf("Key already exists in the tree.\n");

    return root;
}

struct TreeNode* minValueNode(struct TreeNode* node) {
    struct TreeNode* current = node;
    while (current && current->left != NULL)
        current = current->left;
    return current;
}

struct TreeNode* deleteNode(struct TreeNode* root, int key) {
    if (root == NULL)
        return root;

    if (key < root->key)
        root->left = deleteNode(root->left, key);
    else if (key > root->key)
        root->right = deleteNode(root->right, key);
    else {
        if (root->left == NULL) {
            struct TreeNode* temp = root->right;
            free(root);
            return temp;
        } else if (root->right == NULL) {
            struct TreeNode* temp = root->left;
            free(root);
            return temp;
        }

        struct TreeNode* temp = minValueNode(root->right);
        root->key = temp->key;
        root->right = deleteNode(root->right, temp->key);
    }
    return root;
}

struct TreeNode* searchNode(struct TreeNode* root, int key) {
    if (root == NULL || root->key == key)
        return root;

    if (key < root->key)
        return searchNode(root->left, key);
    return searchNode(root->right, key);
}

void inorderTraversal(struct TreeNode* root) {
    if (root == NULL)
        return;

    inorderTraversal(root->left);
    printf("%d ", root->key);
    inorderTraversal(root->right);
}

void displayMenu() {
    printf("\nMenu:\n");
    printf("1. Insert\n");
    printf("2. Delete\n");
    printf("3. Find\n");
    printf("4. Display Inorder\n");
    printf("5. Exit\n");
}

int main() {
    struct TreeNode* root = NULL;
    int choice, key;
    struct TreeNode* found;

    do {
        displayMenu();
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                printf("Enter the key to insert: ");
                scanf("%d", &key);
                root = insertNode(root, key);
                break;
            case 2:
                printf("Enter the key to delete: ");
                scanf("%d", &key);
                root = deleteNode(root, key);
                break;
            case 3:
                printf("Enter the key to find: ");
                scanf("%d", &key);
                found = searchNode(root, key);
                if (found != NULL)
                    printf("Key %d found in the tree.\n", key);
                else
                    printf("Key %d not found in the tree.\n", key);
                break;
            case 4:
                printf("Inorder Traversal: ");
                inorderTraversal(root);
                printf("\n");
                break;
            case 5:
                printf("Exiting the program.\n");
                break;
            default:
                printf("Invalid choice! Please enter a valid option.\n");
        }
    } while (choice != 5);

    return 0;
}

  *******************

5)	Write a program to illustrate operations on a BST holding numeric keys. The menu must include: • Insert • Mirror Image • Find • Post order (nonrecursive)

  #include <stdio.h>
#include <stdlib.h>

struct TreeNode {
    int key;
    struct TreeNode* left;
    struct TreeNode* right;
};

struct TreeNode* createNode(int key) {
    struct TreeNode* newNode = (struct TreeNode*)malloc(sizeof(struct TreeNode));
    if (newNode == NULL) {
        printf("Memory allocation failed\n");
        exit(1);
    }
    newNode->key = key;
    newNode->left = NULL;
    newNode->right = NULL;
    return newNode;
}

struct TreeNode* insertNode(struct TreeNode* root, int key) {
    if (root == NULL)
        return createNode(key);

    if (key < root->key)
        root->left = insertNode(root->left, key);
    else if (key > root->key)
        root->right = insertNode(root->right, key);
    else
        printf("Key already exists in the tree.\n");

    return root;
}

struct TreeNode* minValueNode(struct TreeNode* node) {
    struct TreeNode* current = node;
    while (current && current->left != NULL)
        current = current->left;
    return current;
}

struct TreeNode* deleteNode(struct TreeNode* root, int key) {
    if (root == NULL)
        return root;

    if (key < root->key)
        root->left = deleteNode(root->left, key);
    else if (key > root->key)
        root->right = deleteNode(root->right, key);
    else {
        if (root->left == NULL) {
            struct TreeNode* temp = root->right;
            free(root);
            return temp;
        } else if (root->right == NULL) {
            struct TreeNode* temp = root->left;
            free(root);
            return temp;
        }

        struct TreeNode* temp = minValueNode(root->right);
        root->key = temp->key;
        root->right = deleteNode(root->right, temp->key);
    }
    return root;
}

struct TreeNode* searchNode(struct TreeNode* root, int key) {
    if (root == NULL || root->key == key)
        return root;

    if (key < root->key)
        return searchNode(root->left, key);
    return searchNode(root->right, key);
}

void inorderTraversal(struct TreeNode* root) {
    if (root == NULL)
        return;

    inorderTraversal(root->left);
    printf("%d ", root->key);
    inorderTraversal(root->right);
}

void displayMenu() {
    printf("\nMenu:\n");
    printf("1. Insert\n");
    printf("2. Delete\n");
    printf("3. Find\n");
    printf("4. Display Inorder\n");
    printf("5. Exit\n");
}

int main() {
    struct TreeNode* root = NULL;
    int choice, key;
    struct TreeNode* found;

    do {
        displayMenu();
        printf("Enter your choice: ");
        scanf("%d", &choice);

        switch (choice) {
            case 1:
                printf("Enter the key to insert: ");
                scanf("%d", &key);
                root = insertNode(root, key);
                break;
            case 2:
                printf("Enter the key to delete: ");
                scanf("%d", &key);
                root = deleteNode(root, key);
                break;
            case 3:
                printf("Enter the key to find: ");
                scanf("%d", &key);
                found = searchNode(root, key);
                if (found != NULL)
                    printf("Key %d found in the tree.\n", key);
                else
                    printf("Key %d not found in the tree.\n", key);
                break;
            case 4:
                printf("Inorder Traversal: ");
                inorderTraversal(root);
                printf("\n");
                break;
            case 5:
                printf("Exiting the program.\n");
                break;
            default:
                printf("Invalid choice! Please enter a valid option.\n");
        }
    } while (choice != 5);

    return 0;
}
