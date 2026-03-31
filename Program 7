#include <stdio.h>
#include <stdlib.h>
#include <ctype.h>
#include <string.h>

// Enum for node types
typedef enum {
    NODE_NUMBER,
    NODE_OPERATOR
} NodeType;

// AST Node structure
typedef struct ASTNode {
    NodeType type;
    union {
        int value; // For numbers
        struct {
            char op;                // Operator: +, -, *, /
            struct ASTNode *left;   // Left child
            struct ASTNode *right;  // Right child
        } opr;
    };
} ASTNode;

// Function to create a number node
ASTNode* createNumberNode(int value) {
    ASTNode* node = (ASTNode*)malloc(sizeof(ASTNode));
    if (!node) {
        fprintf(stderr, "Memory allocation failed\n");
        exit(EXIT_FAILURE);
    }
    node->type = NODE_NUMBER;
    node->value = value;
    return node;
}

// Function to create an operator node
ASTNode* createOperatorNode(char op, ASTNode* left, ASTNode* right) {
    ASTNode* node = (ASTNode*)malloc(sizeof(ASTNode));
    if (!node) {
        fprintf(stderr, "Memory allocation failed\n");
        exit(EXIT_FAILURE);
    }
    node->type = NODE_OPERATOR;
    node->opr.op = op;
    node->opr.left = left;
    node->opr.right = right;
    return node;
}

// Function to print AST in preorder (for debugging)
void printAST(ASTNode* node) {
    if (!node) return;
    if (node->type == NODE_NUMBER) {
        printf("%d ", node->value);
    } else {
        printf("%c ", node->opr.op);
        printAST(node->opr.left);
        printAST(node->opr.right);
    }
}

// Function to free AST memory
void freeAST(ASTNode* node) {
    if (!node) return;
    if (node->type == NODE_OPERATOR) {
        freeAST(node->opr.left);
        freeAST(node->opr.right);
    }
    free(node);
}

// Example: manually constructing AST for (3 + 5) * (10 - 2)
int main() {
    // Left subtree: (3 + 5)
    ASTNode* left = createOperatorNode('+',
                        createNumberNode(3),
                        createNumberNode(5));

    // Right subtree: (10 - 2)
    ASTNode* right = createOperatorNode('-',
                        createNumberNode(10),
                        createNumberNode(2));

    // Root: (*)
    ASTNode* root = createOperatorNode('*', left, right);

    printf("Preorder traversal of AST: ");
    printAST(root);
    printf("\n");

    // Cleanup
    freeAST(root);
    return 0;
}
