# DSA Practical Programs

This README contains the provided practicals and their complete C++ code. Each section includes the title and the unmodified code as requested.

---

## PRACTICAL 1: 1D Array Operations

```cpp
#include <iostream>
using namespace std;

void inputArray(int arr[], int n)
{
    cout << "Enter " << n << " elements:\n";

    for (int i = 0; i < n; i++)
        cin >> arr[i];
}

void displayArray(int arr[], int n)
{
    cout << "Array elements: ";

    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";

    cout << endl;
}

void linearSearch(int arr[], int n)
{
    int key;
    bool found = false;

    cout << "Enter element to search: ";
    cin >> key;

    for (int i = 0; i < n; i++)
    {
        if (arr[i] == key)
        {
            cout << "Element " << key
                 << " found at position "
                 << i + 1 << endl;

            found = true;
            break;
        }
    }

    if (!found)
        cout << "Element " << key
             << " not found in the array.\n";
}

void bubbleSort(int arr[], int n)
{
    int start = 0, end = n - 1;

    while (start < end)
    {
        swap(arr[start], arr[end]);
        start++;
        end--;
    }

    cout << "Array reversed successfully!\n";
    displayArray(arr, n);
}

int main()
{
    int arr[100], n, choice;

    cout << "Enter number of elements: ";
    cin >> n;

    inputArray(arr, n);

    do
    {
        cout << "\n---- MENU ----\n";
        cout << "1. Display Array\n";
        cout << "2. Search an Element\n";
        cout << "3. Sort the Array\n";
        cout << "4. Reverse the Array\n";
        cout << "5. Exit\n";

        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice)
        {
            case 1:
                displayArray(arr, n);
                break;

            case 2:
                linearSearch(arr, n);
                break;

            case 3:
                bubbleSort(arr, n);
                break;

            case 4:
                bubbleSort(arr, n);
                break;

            case 5:
                cout << "Exiting program...\n";
                break;

            default:
                cout << "Invalid choice! Please try again.\n";
        }

    } while (choice != 5);

    return 0;
}
```

---

## PRACTICAL 1a: Merge Two Arrays in Sorted Order
Aim: Read two arrays from the user, merge them, and display the elements in sorted order. (Menu Driven)

```cpp
#include <iostream>
using namespace std;

void inputArray(int arr[], int n, int arrayNum)
{
    cout << "Enter " << n << " elements for array "
         << arrayNum << ":\n";

    for (int i = 0; i < n; i++)
        cin >> arr[i];
}

void bubbleSort(int arr[], int n)
{
    for (int i = 0; i < n - 1; i++)
    {
        for (int j = 0; j < n - i - 1; j++)
        {
            if (arr[j] > arr[j + 1])
            {
                swap(arr[j], arr[j + 1]);
            }
        }
    }
}

void mergeArrays(int arr1[], int n1,
                 int arr2[], int n2,
                 int merged[])
{
    int i = 0, j = 0, k = 0;

    // Sort both arrays individually
    bubbleSort(arr1, n1);
    bubbleSort(arr2, n2);

    // Merge like the merge step of merge sort
    while (i < n1 && j < n2)
    {
        if (arr1[i] <= arr2[j])
            merged[k++] = arr1[i++];
        else
            merged[k++] = arr2[j++];
    }

    while (i < n1)
        merged[k++] = arr1[i++];

    while (j < n2)
        merged[k++] = arr2[j++];
}

void displayArray(int arr[], int n)
{
    for (int i = 0; i < n; i++)
        cout << arr[i] << " ";

    cout << endl;
}

int main()
{
    int arr1[100], arr2[100], merged[200];
    int n1 = 0, n2 = 0, choice;

    do
    {
        cout << "\n---- MENU ----\n";
        cout << "1. Enter array 1\n";
        cout << "2. Enter array 2\n";
        cout << "3. Merge and display in sorted order\n";
        cout << "4. Exit\n";

        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice)
        {
            case 1:
                cout << "Enter size of array 1: ";
                cin >> n1;

                inputArray(arr1, n1, 1);
                break;

            case 2:
                cout << "Enter size of array 2: ";
                cin >> n2;

                inputArray(arr2, n2, 2);
                break;

            case 3:
                if (n1 == 0 || n2 == 0)
                {
                    cout << "Please enter both arrays first.\n";
                    break;
                }

                mergeArrays(arr1, n1, arr2, n2, merged);

                cout << "Merged array in sorted order:\n";
                displayArray(merged, n1 + n2);
                break;

            case 4:
                cout << "Exiting program...\n";
                break;

            default:
                cout << "Invalid choice! Please try again.\n";
        }

    } while (choice != 4);

    return 0;
}
```

---

## practical 1c: Matrix Addition, Multiplication, and Transpose
Aim: Write a menu-driven program to perform matrix addition, multiplication, and transpose operations.

```cpp
#include <iostream>
#include <vector>
using namespace std;

int main()
{
    int r, c;

    cout << "Enter rows and columns: ";
    cin >> r >> c;

    vector<vector<int>> A(r, vector<int>(c));
    vector<vector<int>> B(r, vector<int>(c));

    cout << "Enter elements of matrix A:\n";

    for (int i = 0; i < r; i++)
    {
        for (int j = 0; j < c; j++)
            cin >> A[i][j];
    }

    cout << "Enter elements of matrix B:\n";

    for (int i = 0; i < r; i++)
    {
        for (int j = 0; j < c; j++)
            cin >> B[i][j];
    }

    int choice;

    do
    {
        cout << "\n--- Matrix Menu ---\n";
        cout << "1. Addition\n";
        cout << "2. Multiplication\n";
        cout << "3. Transpose of A\n";
        cout << "4. Exit\n";

        cout << "Enter choice: ";
        cin >> choice;

        switch (choice)
        {
            case 1:
            {
                cout << "Result (A + B):\n";

                for (int i = 0; i < r; i++)
                {
                    for (int j = 0; j < c; j++)
                        cout << A[i][j] + B[i][j] << " ";

                    cout << endl;
                }

                break;
            }

            case 2:
            {
                if (c != r)
                {
                    cout << "Multiplication requires compatible matrices.\n";
                    break;
                }

                vector<vector<int>> C(r, vector<int>(c, 0));

                for (int i = 0; i < r; i++)
                {
                    for (int j = 0; j < c; j++)
                    {
                        for (int k = 0; k < c; k++)
                            C[i][j] += A[i][k] * B[k][j];
                    }
                }

                cout << "Result (A * B):\n";

                for (int i = 0; i < r; i++)
                {
                    for (int j = 0; j < c; j++)
                        cout << C[i][j] << " ";

                    cout << endl;
                }

                break;
            }

            case 3:
            {
                cout << "Transpose of A:\n";

                for (int i = 0; i < c; i++)
                {
                    for (int j = 0; j < r; j++)
                        cout << A[j][i] << " ";

                    cout << endl;
                }

                break;
            }

            case 4:
                cout << "Exiting program...\n";
                break;

            default:
                cout << "Invalid choice! Please try again.\n";
        }

    } while (choice != 4);

    return 0;
}
```

---

## PRACTICAL-2

### Q1. Singly Linked List — Display in Reverse Order

```cpp
#include <iostream>
using namespace std;

struct Node
{
    int data;
    Node *next;
};

Node *head = nullptr;

void insert(int value)
{
    Node *newNode = new Node{value, nullptr};

    if (!head)
    {
        head = newNode;
        return;
    }

    Node *temp = head;

    while (temp->next)
        temp = temp->next;

    temp->next = newNode;
}

void displayReverse(Node *node)
{
    if (!node)
        return;

    displayReverse(node->next);
    cout << node->data << " ";
}

int main()
{
    int n, val;

    cout << "Enter number of nodes: ";
    cin >> n;

    cout << "Enter elements:\n";

    for (int i = 0; i < n; i++)
    {
        cin >> val;
        insert(val);
    }

    cout << "Linked list in reverse order: ";
    displayReverse(head);
    cout << endl;

    return 0;
}
```

### Q2. Search for an Element in a Linked List

```cpp
#include <iostream>
using namespace std;

struct Node
{
    int data;
    Node *next;
};

Node *head = nullptr;

void insert(int value)
{
    Node *newNode = new Node{value, nullptr};

    if (!head)
    {
        head = newNode;
        return;
    }

    Node *temp = head;

    while (temp->next)
    {
        temp = temp->next;
    }

    temp->next = newNode;
}

void search(int key)
{
    Node *temp = head;
    int pos = 1;

    while (temp)
    {
        if (temp->data == key)
        {
            cout << "Element " << key
                 << " found at position "
                 << pos << endl;
            return;
        }

        temp = temp->next;
        pos++;
    }

    cout << "Element " << key
         << " not found in the list.\n";
}

int main()
{
    int n, val, key;

    cout << "Enter number of nodes: ";
    cin >> n;

    cout << "Enter elements:\n";

    for (int i = 0; i < n; i++)
    {
        cin >> val;
        insert(val);
    }

    cout << "Enter element to search: ";
    cin >> key;

    search(key);

    return 0;
}
```

---

## Practical 3(a): Stack Implementation using Push, Pop and Display.

```cpp
#include <iostream>
using namespace std;

#define MAX 100

int arr[MAX], top = -1;

void push(int val)
{
    if (top == MAX - 1)
    {
        cout << "Stack overflow!\n";
        return;
    }

    arr[++top] = val;
    cout << val << " pushed onto the stack.\n";
}

void pop()
{
    if (top == -1)
    {
        cout << "Stack underflow!\n";
        return;
    }

    cout << arr[top--] << " popped from the stack.\n";
}

void display()
{
    if (top == -1)
    {
        cout << "Stack is empty.\n";
        return;
    }

    cout << "Stack elements (top to bottom): ";

    for (int i = top; i >= 0; i--)
    {
        cout << arr[i] << " ";
    }

    cout << endl;
}

int main()
{
    int choice, val;

    do
    {
        cout << "\n--- MENU ---\n";
        cout << "1. Push\n";
        cout << "2. Pop\n";
        cout << "3. Display\n";
        cout << "4. Exit\n";
        cout << "Enter your choice: ";
        cin >> choice;

        switch (choice)
        {
            case 1:
                cout << "Enter value to push: ";
                cin >> val;
                push(val);
                break;

            case 2:
                pop();
                break;

            case 3:
                display();
                break;

            case 4:
                cout << "Exiting program...\n";
                break;

            default:
                cout << "Invalid choice!\n";
        }

    } while (choice != 4);

    return 0;
}
```

---

## Practical 3(b): Infix to Postfix and Prefix Conversion
Infix to Postfix and Prefix Conversion in clean, copy-paste-ready C++.

```cpp
#include <iostream>
#include <stack>
#include <algorithm>
#include <string>
#include <cctype>
using namespace std;

int precedence(char op)
{
    if (op == '+' || op == '-')
        return 1;
    if (op == '*' || op == '/')
        return 2;
    if (op == '^')
        return 3;

    return 0;
}

string infixToPostfix(string infix)
{
    stack<char> st;
    string postfix = "";

    for (char c : infix)
    {
        if (isalnum(c))
        {
            postfix += c;
        }
        else if (c == '(')
        {
            st.push(c);
        }
        else if (c == ')')
        {
            while (!st.empty() && st.top() != '(')
            {
                postfix += st.top();
                st.pop();
            }

            if (!st.empty())
                st.pop();
        }
        else
        {
            while (!st.empty() && st.top() != '(' &&
                   (precedence(st.top()) > precedence(c) ||
                   (precedence(st.top()) == precedence(c) && c != '^')))
            {
                postfix += st.top();
                st.pop();
            }

            st.push(c);
        }
    }

    while (!st.empty())
    {
        postfix += st.top();
        st.pop();
    }

    return postfix;
}

string infixToPrefix(string infix)
{
    reverse(infix.begin(), infix.end());

    for (char &c : infix)
    {
        if (c == '(')
            c = ')';
        else if (c == ')')
            c = '(';
    }

    string prefix = infixToPostfix(infix);

    reverse(prefix.begin(), prefix.end());

    return prefix;
}

int main()
{
    string infix;

    cout << "Enter infix expression: ";
    cin >> infix;

    cout << "Postfix expression: "
         << infixToPostfix(infix) << endl;

    cout << "Prefix expression: "
         << infixToPrefix(infix) << endl;

    return 0;
}
```

---

## Practical 3(c): Tower of Hanoi

```cpp
#include <iostream>
using namespace std;

int moveCount = 0;

void towerOfHanoi(int n, char from, char aux, char to)
{
    if (n == 0)
        return;

    towerOfHanoi(n - 1, from, to, aux);

    cout << "Move disk " << n << " from "
         << from << " to " << to << endl;

    moveCount++;

    towerOfHanoi(n - 1, aux, from, to);
}

int main()
{
    int n;

    cout << "Enter number of disks: ";
    cin >> n;

    if (n <= 0)
    {
        cout << "Please enter a positive number.\n";
        return 0;
    }

    towerOfHanoi(n, 'A', 'B', 'C');

    cout << "Total moves: " << moveCount << endl;

    return 0;
}
```

---

## Practical 4a1. Double-Ended Queue (Deque)

```cpp
#include <iostream>
using namespace std;

#define MAX 5

class Deque {
    int arr[MAX];
    int front, rear;

public:
    Deque() {
        front = -1;
        rear = -1;
    }

    bool isEmpty() {
        return front == -1;
    }

    bool isFull() {
        return (front == 0 && rear == MAX - 1) ||
               (front == rear + 1);
    }

    void insertFront(int value) {
        if (isFull()) {
            cout << "Deque Overflow!\n";
            return;
        }

        if (isEmpty()) {
            front = rear = 0;
        }
        else if (front == 0) {
            front = MAX - 1;
        }
        else {
            front--;
        }

        arr[front] = value;
        cout << value << " inserted at front.\n";
    }

    void insertRear(int value) {
        if (isFull()) {
            cout << "Deque Overflow!\n";
            return;
        }

        if (isEmpty()) {
            front = rear = 0;
        }
        else if (rear == MAX - 1) {
            rear = 0;
        }
        else {
            rear++;
        }

        arr[rear] = value;
        cout << value << " inserted at rear.\n";
    }

    void deleteFront() {
        if (isEmpty()) {
            cout << "Deque Underflow!\n";
            return;
        }

        cout << arr[front] << " deleted from front.\n";

        if (front == rear) {
            front = rear = -1;
        }
        else if (front == MAX - 1) {
            front = 0;
        }
        else {
            front++;
        }
    }

    void deleteRear() {
        if (isEmpty()) {
            cout << "Deque Underflow!\n";
            return;
        }

        cout << arr[rear] << " deleted from rear.\n";

        if (front == rear) {
            front = rear = -1;
        }
        else if (rear == 0) {
            rear = MAX - 1;
        }
        else {
            rear--;
        }
    }

    void display() {
        if (isEmpty()) {
            cout << "Deque is empty.\n";
            return;
        }

        cout << "Deque: ";
        int i = front;

        while (true) {
            cout << arr[i] << " ";

            if (i == rear)
                break;

            i = (i + 1) % MAX;
        }

        cout << endl;
    }
};

int main() {
    Deque d;
    int choice, value;

    do {
        cout << "\n--- DEQUE MENU ---\n";
        cout << "1. Insert Front\n";
        cout << "2. Insert Rear\n";
        cout << "3. Delete Front\n";
        cout << "4. Delete Rear\n";
        cout << "5. Display\n";
        cout << "6. Exit\n";
        cout << "Enter choice: ";
        cin >> choice;

        switch (choice) {
            case 1:
                cout << "Enter value: ";
                cin >> value;
                d.insertFront(value);
                break;

            case 2:
                cout << "Enter value: ";
                cin >> value;
                d.insertRear(value);
                break;

            case 3:
                d.deleteFront();
                break;

            case 4:
                d.deleteRear();
                break;

            case 5:
                d.display();
                break;

            case 6:
                cout << "Exiting...\n";
                break;

            default:
                cout << "Invalid choice!\n";
        }

    } while (choice != 6);

    return 0;
}
```

---

## practical 4b2. Circular Queue

```cpp
#include <iostream>
using namespace std;

#define MAX 5

class CircularQueue {
    int arr[MAX];
    int front, rear;

public:
    CircularQueue() {
        front = -1;
        rear = -1;
    }

    bool isEmpty() {
        return front == -1;
    }

    bool isFull() {
        return (rear + 1) % MAX == front;
    }

    void insert(int value) {
        if (isFull()) {
            cout << "Queue Overflow!\n";
            return;
        }

        if (isEmpty()) {
            front = rear = 0;
        }
        else {
            rear = (rear + 1) % MAX;
        }

        arr[rear] = value;
        cout << value << " inserted.\n";
    }

    void deleteElement() {
        if (isEmpty()) {
            cout << "Queue Underflow!\n";
            return;
        }

        cout << arr[front] << " deleted.\n";

        if (front == rear) {
            front = rear = -1;
        }
        else {
            front = (front + 1) % MAX;
        }
    }

    void display() {
        if (isEmpty()) {
            cout << "Queue is empty.\n";
            return;
        }

        cout << "Queue: ";

        int i = front;

        while (true) {
            cout << arr[i] << " ";

            if (i == rear)
                break;

            i = (i + 1) % MAX;
        }

        cout << endl;
    }
};

int main() {
    CircularQueue q;
    int choice, value;

    do {
        cout << "\n--- CIRCULAR QUEUE MENU ---\n";
        cout << "1. Insert\n";
        cout << "2. Delete\n";
        cout << "3. Display\n";
        cout << "4. Exit\n";
        cout << "Enter choice: ";
        cin >> choice;

        switch (choice) {
            case 1:
                cout << "Enter value: ";
                cin >> value;
                q.insert(value);
                break;

            case 2:
                q.deleteElement();
                break;

            case 3:
                q.display();
                break;

            case 4:
                cout << "Exiting...\n";
                break;

            default:
                cout << "Invalid choice!\n";
        }

    } while (choice != 4);

    return 0;
}
```

---

## practical 4c3. Linear Queue

```cpp
#include <iostream>
using namespace std;

#define MAX 5

class Queue {
    int arr[MAX];
    int front, rear;

public:
    Queue() {
        front = -1;
        rear = -1;
    }

    bool isEmpty() {
        return front == -1;
    }

    bool isFull() {
        return rear == MAX - 1;
    }

    void insert(int value) {
        if (isFull()) {
            cout << "Queue Overflow!\n";
            return;
        }

        if (isEmpty()) {
            front = 0;
        }

        rear++;
        arr[rear] = value;

        cout << value << " inserted.\n";
    }

    void deleteElement() {
        if (isEmpty()) {
            cout << "Queue Underflow!\n";
            return;
        }

        cout << arr[front] << " deleted.\n";

        if (front == rear) {
            front = rear = -1;
        }
        else {
            front++;
        }
    }

    void display() {
        if (isEmpty()) {
            cout << "Queue is empty.\n";
            return;
        }

        cout << "Queue: ";

        for (int i = front; i <= rear; i++) {
            cout << arr[i] << " ";
        }

        cout << endl;
    }
};

int main() {
    Queue q;
    int choice, value;

    do {
        cout << "\n--- LINEAR QUEUE MENU ---\n";
        cout << "1. Insert\n";
        cout << "2. Delete\n";
        cout << "3. Display\n";
        cout << "4. Exit\n";
        cout << "Enter choice: ";
        cin >> choice;

        switch (choice) {
            case 1:
                cout << "Enter value: ";
                cin >> value;
                q.insert(value);
                break;

            case 2:
                q.deleteElement();
                break;

            case 3:
                q.display();
                break;

            case 4:
                cout << "Exiting...\n";
                break;

            default:
                cout << "Invalid choice!\n";
        }

    } while (choice != 4);

    return 0;
}
```

---

## Practical No. 5 — Sorting Techniques in C++

### Q1. WAP to Implement Bubble Sort

```cpp
#include <iostream>
using namespace std;

void bubbleSort(int arr[], int n)
{
    for (int i = 0; i < n - 1; i++)
    {
        for (int j = 0; j < n - i - 1; j++)
        {
            if (arr[j] > arr[j + 1])
            {
                swap(arr[j], arr[j + 1]);
            }
        }
    }
}

int main()
{
    int arr[] = {64, 34, 25, 12, 22, 11, 90};
    int n = sizeof(arr) / sizeof(arr[0]);

    bubbleSort(arr, n);

    cout << "Sorted array using Bubble Sort: ";

    for (int i = 0; i < n; i++)
    {
        cout << arr[i] << " ";
    }

    return 0;
}
```

### Q2. WAP to Implement Quick Sort

```cpp
#include <iostream>
using namespace std;

int partition(int arr[], int low, int high)
{
    int pivot = arr[high];
    int i = low - 1;

    for (int j = low; j < high; j++)
    {
        if (arr[j] < pivot)
        {
            i++;
            swap(arr[i], arr[j]);
        }
    }

    swap(arr[i + 1], arr[high]);

    return i + 1;
}

void quickSort(int arr[], int low, int high)
{
    if (low < high)
    {
        int pi = partition(arr, low, high);

        quickSort(arr, low, pi - 1);
        quickSort(arr, pi + 1, high);
    }
}

int main()
{
    int arr[] = {64, 34, 25, 12, 22, 11, 90};
    int n = sizeof(arr) / sizeof(arr[0]);

    quickSort(arr, 0, n - 1);

    cout << "Sorted array using Quick Sort: ";

    for (int i = 0; i < n; i++)
    {
        cout << arr[i] << " ";
    }

    return 0;
}
```

### Q3. WAP to Implement Insertion Sort

```cpp
#include <iostream>
using namespace std;

void insertionSort(int arr[], int n)
{
    for (int i = 1; i < n; i++)
    {
        int key = arr[i];
        int j = i - 1;

        while (j >= 0 && arr[j] > key)
        {
            arr[j + 1] = arr[j];
            j--;
        }

        arr[j + 1] = key;
    }
}

int main()
{
    int arr[] = {64, 34, 25, 12, 22, 11, 90};
    int n = sizeof(arr) / sizeof(arr[0]);

    insertionSort(arr, n);

    cout << "Sorted array using Insertion Sort: ";

    for (int i = 0; i < n; i++)
    {
        cout << arr[i] << " ";
    }

    return 0;
}
```

---

## Practical No. 6

### Q1. WAP to Implement Linear Search

```cpp
#include <iostream>
#include <vector>
using namespace std;

// Function to perform linear search
int linearSearch(const vector<int>& arr, int target)
{
    for (int i = 0; i < arr.size(); i++)
    {
        if (arr[i] == target)
        {
            return i;
        }
    }

    return -1;
}

int main()
{
    vector<int> numbers = {12, 45, 67, 8, 93, 21};

    int target = 93;

    int result = linearSearch(numbers, target);

    if (result != -1)
    {
        cout << "Element found at index: " << result << endl;
    }
    else
    {
        cout << "Element not found in the array." << endl;
    }

    return 0;
}
```

### Q2. WAP to Implement Binary Search

```cpp
#include <iostream>
using namespace std;

// Function to perform binary search
int binarySearch(int arr[], int n, int target)
{
    int left = 0;
    int right = n - 1;

    while (left <= right)
    {
        int mid = left + (right - left) / 2;

        if (arr[mid] == target)
        {
            return mid;
        }
        else if (arr[mid] < target)
        {
            left = mid + 1;
        }
        else
        {
            right = mid - 1;
        }
    }

    return -1;
}

int main()
{
    int arr[] = {2, 5, 8, 12, 16, 23, 38, 56};

    int n = sizeof(arr) / sizeof(arr[0]);

    int target = 23;

    int result = binarySearch(arr, n, target);

    if (result != -1)
    {
        cout << "Element found at index: " << result << endl;
    }
    else
    {
        cout << "Element not found." << endl;
    }

    return 0;
}
```

---

## Practical No. 7: Binary Tree Traversals

```cpp
#include <iostream>
using namespace std;

// Node structure
struct Node
{
    int data;
    Node* left;
    Node* right;
};

// Creates a new node
Node* CreateNode(int value)
{
    Node* newNode = new Node();

    newNode->data = value;
    newNode->left = NULL;
    newNode->right = NULL;

    return newNode;
}

// Inorder Traversal: Left -> Root -> Right
void inorder(Node* root)
{
    if (root == NULL)
        return;

    inorder(root->left);
    cout << root->data << " ";
    inorder(root->right);
}

// Preorder Traversal: Root -> Left -> Right
void preorder(Node* root)
{
    if (root == NULL)
        return;

    cout << root->data << " ";
    preorder(root->left);
    preorder(root->right);
}

// Postorder Traversal: Left -> Right -> Root
void postorder(Node* root)
{
    if (root == NULL)
        return;

    postorder(root->left);
    postorder(root->right);
    cout << root->data << " ";
}

int main()
{
    // Create a binary tree
    Node* root = CreateNode(1);

    root->left = CreateNode(2);
    root->right = CreateNode(3);

    root->left->left = CreateNode(4);
    root->left->right = CreateNode(5);

    // Display traversals
    cout << "Inorder Traversal: ";
    inorder(root);

    cout << "\nPreorder Traversal: ";
    preorder(root);

    cout << "\nPostorder Traversal: ";
    postorder(root);

    return 0;
}
```

---

## Practical-8

### Q1. C++ Program to Implement Minimum Heap

```cpp
#include <iostream>
using namespace std;

class MinHeap {
private:
    int heap[100];
    int size;

public:
    MinHeap() {
        size = 0;
    }

    // Insert an element into the heap
    void insert(int value) {
        size++;
        int i = size;
        heap[i] = value;

        // Move the element upward
        while (i > 1 && heap[i] < heap[i / 2]) {
            swap(heap[i], heap[i / 2]);
            i = i / 2;
        }
    }

    // Delete the minimum element (root)
    void deletion() {
        if (size == 0) {
            cout << "Heap is empty!" << endl;
            return;
        }

        cout << "Deleted element: " << heap[1] << endl;

        heap[1] = heap[size];
        size--;

        // Move the element downward
        int i = 1;

        while (true) {
            int left = 2 * i;
            int right = 2 * i + 1;
            int smallest = i;

            if (left <= size && heap[left] < heap[smallest]) {
                smallest = left;
            }

            if (right <= size && heap[right] < heap[smallest]) {
                smallest = right;
            }

            if (smallest != i) {
                swap(heap[i], heap[smallest]);
                i = smallest;
            } else {
                break;
            }
        }
    }

    // Display the heap
    void display() {
        cout << "Min Heap: ";

        for (int i = 1; i <= size; i++) {
            cout << heap[i] << " ";
        }

        cout << endl;
    }
};

int main() {
    MinHeap h;

    h.insert(40);
    h.insert(20);
    h.insert(10);
    h.insert(30);
    h.insert(50);

    cout << "After insertion:" << endl;
    h.display();

    h.deletion();

    cout << "After deletion:" << endl;
    h.display();

    return 0;
}
```

### Q2. C++ Program to Implement Maximum Heap

```cpp
#include <iostream>
using namespace std;

class MaxHeap {
private:
    int heap[100];
    int size;

public:
    MaxHeap() {
        size = 0;
    }

    // Insert an element into the heap
    void insert(int value) {
        size++;
        int i = size;
        heap[i] = value;

        // Move the element upward
        while (i > 1 && heap[i] > heap[i / 2]) {
            swap(heap[i], heap[i / 2]);
            i = i / 2;
        }
    }

    // Delete the maximum element (root)
    void deletion() {
        if (size == 0) {
            cout << "Heap is empty!" << endl;
            return;
        }

        cout << "Deleted element: " << heap[1] << endl;

        heap[1] = heap[size];
        size--;

        // Move the element downward
        int i = 1;

        while (true) {
            int left = 2 * i;
            int right = 2 * i + 1;
            int largest = i;

            if (left <= size && heap[left] > heap[largest]) {
                largest = left;
            }

            if (right <= size && heap[right] > heap[largest]) {
                largest = right;
            }

            if (largest != i) {
                swap(heap[i], heap[largest]);
                i = largest;
            } else {
                break;
            }
        }
    }

    // Display the heap
    void display() {
        cout << "Max Heap: ";

        for (int i = 1; i <= size; i++) {
            cout << heap[i] << " ";
        }

        cout << endl;
    }
};

int main() {
    MaxHeap h;

    h.insert(40);
    h.insert(20);
    h.insert(10);
    h.insert(30);
    h.insert(50);

    cout << "After insertion:" << endl;
    h.display();

    h.deletion();

    cout << "After deletion:" << endl;
    h.display();

    return 0;
}
```

---

## Practical-9

### 1. Collision Resolution Using Chaining

```cpp
#include <iostream>
#include <list>
using namespace std;

class HashTable {
    int size;
    list<int>* table;

public:
    HashTable(int s) {
        size = s;
        table = new list<int>[size];
    }

    int hashFunction(int key) {
        return key % size;
    }

    void insert(int key) {
        int index = hashFunction(key);
        table[index].push_back(key);

        cout << "Inserted " << key << " at index "
             << index << endl;
    }

    void remove(int key) {
        int index = hashFunction(key);
        table[index].remove(key);
    }

    void search(int key) {
        int index = hashFunction(key);

        for (int value : table[index]) {
            if (value == key) {
                cout << key << " found at index "
                     << index << endl;
                return;
            }
        }

        cout << key << " not found" << endl;
    }

    void display() {
        cout << "\nHash Table (Chaining):\n";

        for (int i = 0; i < size; i++) {
            cout << "Index " << i << ": ";

            for (int value : table[i]) {
                cout << value << " -> ";
            }

            cout << "NULL" << endl;
        }
    }

    ~HashTable() {
        delete[] table;
    }
};

int main() {
    HashTable ht(7);

    int keys[] = {10, 20, 15, 7, 25, 30};
    int n = sizeof(keys) / sizeof(keys[0]);

    for (int i = 0; i < n; i++) {
        ht.insert(keys[i]);
    }

    ht.display();

    ht.search(15);
    ht.search(99);

    return 0;
}
```

### 2. Collision Resolution Using Linear Probing

```cpp
#include <iostream>
using namespace std;

class HashTable {
    int size;
    int* table;

public:
    HashTable(int s) {
        size = s;
        table = new int[size];

        for (int i = 0; i < size; i++) {
            table[i] = -1;
        }
    }

    int hashFunction(int key) {
        return key % size;
    }

    void insert(int key) {
        int index = hashFunction(key);
        int start = index;

        while (table[index] != -1) {
            index = (index + 1) % size;

            if (index == start) {
                cout << "Hash table is full!" << endl;
                return;
            }
        }

        table[index] = key;

        cout << "Inserted " << key << " at index "
             << index << endl;
    }

    void search(int key) {
        int index = hashFunction(key);
        int start = index;

        while (table[index] != -1) {
            if (table[index] == key) {
                cout << key << " found at index "
                     << index << endl;
                return;
            }

            index = (index + 1) % size;

            if (index == start) {
                break;
            }
        }

        cout << key << " not found" << endl;
    }

    void display() {
        cout << "\nHash Table (Linear Probing):\n";

        for (int i = 0; i < size; i++) {
            cout << "Index " << i << ": ";

            if (table[i] == -1) {
                cout << "Empty";
            } else {
                cout << table[i];
            }

            cout << endl;
        }
    }

    ~HashTable() {
        delete[] table;
    }
};

int main() {
    HashTable ht(7);

    int keys[] = {10, 20, 15, 7, 25, 30};
    int n = sizeof(keys) / sizeof(keys[0]);

    for (int i = 0; i < n; i++) {
        ht.insert(keys[i]);
    }

    ht.display();

    ht.search(15);
    ht.search(99);

    return 0;
}
```
