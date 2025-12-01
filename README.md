
#include<iostream>
using namespace std;
struct Node {
    int bookID;
    Node* left;
    Node* right;

    Node(int id) {
        bookID = id;
        left = right = nullptr;}
        };

// Insert Book ID 
Node* insertNode(Node* root, int id) {
    if (root == nullptr)
        return new Node(id);

    if (id < root->bookID)
        root->left = insertNode(root->left, id);
    else if (id > root->bookID)
        root->right = insertNode(root->right, id);

    return root;
}

// Search Book ID 
bool searchNode(Node* root, int id) {
    if (root == nullptr)
        return false;

    if (root->bookID == id)
        return true;
    else if (id < root->bookID)
        return searchNode(root->left, id);
    else
        return searchNode(root->right, id);
}

// Display BST in ascending order (inorder traversal)
void inorder(Node* root) {
    if (root == nullptr)
        return;
    inorder(root->left);
    cout << root->bookID << " ";
    inorder(root->right);
}

int main() {
    Node* root = nullptr;
    int choice, id;

    while (true) {
        cout << "\n===== SMART BOOK TRACKING SYSTEM =====\n";
        cout << "1. Return a Book (Store Book ID)\n";
        cout << "2. Check if Book ID is Returned\n";
        cout << "3. Display All Returned Book IDs (Sorted)\n";
        cout << "4. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice) {
        case 1:
            cout << "Enter Book ID to insert: ";
            cin >> id;
            root = insertNode(root, id);
            cout << "Book ID stored successfully!\n";
            break;

        case 2:
            cout << "Enter Book ID to search: ";
            cin >> id;
            if (searchNode(root, id))
                cout << "Book ID " << id << " has been returned.\n";
            else
                cout << "Book ID " << id << " has NOT been returned.\n";
            break;

        case 3:
            cout << "Returned Books in Sorted Order:\n";
            inorder(root);
            cout << endl;
            break;

        case 4:
            cout << "Exiting program...\n";
            return 0;

        default:
            cout << "Invalid choice! Please try again.\n";
        }
    }

    return 0;
}# Book-library-for-finding-book-
