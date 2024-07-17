# FINAL-PROJECT
Final Project Title:

"Efficient Data Retrieval: Implementing a Binary Search Tree in Java"

Project Overview:

The goal of this project is to design and implement a Binary Search Tree (BST) data structure in Java. A BST is a data structure in which each node has at most two children (i.e., left child and right child) and each node represents a key-value pair. The main property of a BST is that for any node, all elements in its left subtree are less than the node, and all elements in its right subtree are greater than the node. This property allows for efficient searching, insertion, and deletion of nodes in the tree.
Project Objectives:

Implement a BST data structure in Java that supports the following operations:
Insertion of a new node with a given key-value pair
Deletion of a node with a given key
Searching for a node with a given key
Traversal of the tree (inorder, preorder, and postorder)
Ensure that the BST maintains its property after each insertion and deletion operation
Optimize the implementation for efficient memory usage and performance
Provide a user-friendly interface for interacting with the BST
Project Requirements:

The BST implementation should be able to handle a minimum of 1000 nodes
The implementation should include the following methods:
insertNode(int key, int value): inserts a new node with the given key-value pair
deleteNode(int key): deletes the node with the given key
searchNode(int key): searches for the node with the given key and returns its value
inorderTraversal(): performs an inorder traversal of the tree and prints the keys and values
preorderTraversal(): performs a preorder traversal of the tree and prints the keys and values
postorderTraversal(): performs a postorder traversal of the tree and prints the keys and values
The implementation should handle duplicate keys and ensure that the BST property is maintained
The implementation should be efficient in terms of time and space complexity
The project should include a test suite to validate the correctness of the implementation
Project Deliverables:
A Java implementation of the BST data structure
A test suite to validate the correctness of the implementation
A user manual that provides instructions on how to use the BST implementation
A report that discusses the design decisions, implementation details, and performance optimization techniques used in the project.

CODE OF IT:
public class BinarySearchTree {
    private Node root;

    public BinarySearchTree() {
        root = null;
    }

    public void insertNode(int key, int value) {
        Node newNode = new Node(key, value);
        if (root == null) {
            root = newNode;
        } else {
            insertNode(root, newNode);
        }
    }

    private void insertNode(Node current, Node newNode) {
        if (newNode.key < current.key) {
            if (current.left == null) {
                current.left = newNode;
            } else {
                insertNode(current.left, newNode);
            }
        } else if (newNode.key > current.key) {
            if (current.right == null) {
                current.right = newNode;
            } else {
                insertNode(current.right, newNode);
            }
        } else {
            // Handle duplicate keys
            System.out.println("Duplicate key: " + newNode.key);
        }
    }

    public void deleteNode(int key) {
        root = deleteNode(root, key);
    }

    private Node deleteNode(Node current, int key) {
        if (current == null) {
            return null;
        }

        if (key < current.key) {
            current.left = deleteNode(current.left, key);
        } else if (key > current.key) {
            current.right = deleteNode(current.right, key);
        } else {
            // Node found, delete it
            if (current.left == null) {
                return current.right;
            } else if (current.right == null) {
                return current.left;
            } else {
                // Node has two children, find the minimum node in the right subtree
                Node minNode = findMinNode(current.right);
                current.key = minNode.key;
                current.value = minNode.value;
                current.right = deleteNode(current.right, minNode.key);
            }
        }
        return current;
    }

    private Node findMinNode(Node node) {
        while (node.left != null) {
            node = node.left;
        }
        return node;
    }

    public int searchNode(int key) {
        return searchNode(root, key);
    }

    private int searchNode(Node current, int key) {
        if (current == null) {
            return -1;
        } else if (key == current.key) {
            return current.value;
        } else if (key < current.key) {
            return searchNode(current.left, key);
        } else {
            return searchNode(current.right, key);
        }
    }

    public void inorderTraversal() {
        inorderTraversal(root);
    }

    private void inorderTraversal(Node node) {
        if (node != null) {
            inorderTraversal(node.left);
            System.out.print(node.key + " ");
            inorderTraversal(node.right);
        }
    }

    public void preorderTraversal() {
        preorderTraversal(root);
    }

    private void preorderTraversal(Node node) {
        if (node != null) {
            System.out.print(node.key + " ");
            preorderTraversal(node.left);
            preorderTraversal(node.right);
        }
    }

    public void postorderTraversal() {
        postorderTraversal(root);
    }

    private void postorderTraversal(Node node) {
        if (node != null) {
            postorderTraversal(node.left);
            postorderTraversal(node.right);
            System.out.print(node.key + " ");
        }
    }

    private static class Node {
        int key;
        int value;
        Node left;
        Node right;

        public Node(int key, int value) {
            this.key = key;
            this.value = value;
            left = null;
            right = null;
        }
    }

    public static void main(String[] args) {
        BinarySearchTree bst = new BinarySearchTree();

        bst.insertNode(5, 10);
        bst.insertNode(2, 20);
        bst.insertNode(8, 30);
        bst.insertNode(3, 40);
        bst.insertNode(9, 50);

        System.out.println("Inorder Traversal: ");
        bst.inorderTraversal();

        System.out.println("\nPreorder Traversal: ");
        bst.preorderTraversal();

        System.out.println("\nPostorder Traversal: ");
        bst.postorderTraversal();

        System.out.println("\nSearch Node 2: " + bst.searchNode(2));
        System.out.println("Search Node 6: " + bst.searchNode(6));

        bst.deleteNode(2);

        System.out.println("\nInorder Traversal after deletion: ");
        bst.inorderTraversal();
    }
}
