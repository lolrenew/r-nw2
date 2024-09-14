
# Tài Liệu Về Quy Hoạch Động, Dữ Liệu Cây, Và Kiến Thức Nâng Cao Về C++

## Mục Lục
- [1. Quy Hoạch Động (Dynamic Programming)](#1-quy-hoạch-động-dynamic-programming)
  - [1.1 Khái Niệm](#11-khái-niệm)
  - [1.2 Đặc Điểm](#12-đặc-điểm)
  - [1.3 Ví Dụ Cơ Bản](#13-ví-dụ-cơ-bản)
  - [1.4 Các Bài Toán Khác](#14-các-bài-toán-khác)
- [2. Dữ Liệu Cây (Tree Data Structures)](#2-dữ-liệu-cây-tree-data-structures)
  - [2.1 Khái Niệm](#21-khái-niệm)
  - [2.2 Các Loại Cây](#22-các-loại-cây)
  - [2.3 Ví Dụ Chi Tiết](#23-ví-dụ-chi-tiết)
- [3. Kiến Thức Nâng Cao Về C++](#3-kiến-thức-nâng-cao-về-cpp)
  - [3.1 Kỹ Thuật Tối Ưu](#31-kỹ-thuật-tối-ưu)
  - [3.2 Ví Dụ Chi Tiết](#32-ví-dụ-chi-tiết)

---

## 1. Quy Hoạch Động (Dynamic Programming)

### 1.1 Khái Niệm
Quy hoạch động (Dynamic Programming - DP) là kỹ thuật giải quyết bài toán bằng cách chia nhỏ bài toán thành các bài toán con nhỏ hơn và lưu trữ kết quả của chúng. Các bài toán con này thường có tính lặp lại, và DP giúp tránh tính toán lại, nhờ đó tối ưu hóa thời gian xử lý.

### 1.2 Đặc Điểm
- **Tối ưu hóa chồng chéo (Overlapping Subproblems)**: Các bài toán con xuất hiện lặp lại nhiều lần.
- **Nguyên lý con tối ưu (Optimal Substructure)**: Lời giải của bài toán lớn được xây dựng dựa trên lời giải của các bài toán con.

### 1.3 Ví Dụ Cơ Bản

#### Ví Dụ: Dãy Con Tăng Dài Nhất (Longest Increasing Subsequence - LIS)
Cho một dãy số, tìm độ dài của dãy con tăng dài nhất.

```cpp
#include <iostream>
#include <vector>
using namespace std;

int LIS(vector<int>& arr) {
    int n = arr.size();
    vector<int> dp(n, 1);

    for (int i = 1; i < n; i++) {
        for (int j = 0; j < i; j++) {
            if (arr[i] > arr[j]) {
                dp[i] = max(dp[i], dp[j] + 1);
            }
        }
    }

    return *max_element(dp.begin(), dp.end());
}

int main() {
    vector<int> arr = {10, 22, 9, 33, 21, 50, 41, 60};
    cout << "Độ dài dãy con tăng dài nhất là: " << LIS(arr) << endl;
    return 0;
}
```

### 1.4 Các Bài Toán Khác
- **Knapsack Problem**: Tối ưu hóa giá trị của các món đồ được chọn vào túi mà không vượt quá trọng lượng tối đa.
- **Bài toán đổi tiền**: Tìm số lượng đồng tiền ít nhất để đổi được một số tiền `n` cho trước.

---

## 2. Dữ Liệu Cây (Tree Data Structures)

### 2.1 Khái Niệm
Cây là một cấu trúc dữ liệu phi tuyến, bao gồm các nút (node) được liên kết với nhau bằng các cạnh (edge). Một cây có một nút gốc (root) và mỗi nút có thể có các nút con.

### 2.2 Các Loại Cây
- **Cây nhị phân (Binary Tree)**: Mỗi nút có tối đa hai con.
- **Cây nhị phân tìm kiếm (Binary Search Tree - BST)**: Một dạng cây nhị phân, nơi tất cả các giá trị của nút con bên trái nhỏ hơn nút cha, và nút con bên phải lớn hơn.

### 2.3 Ví Dụ Chi Tiết

#### Ví Dụ: Cây Nhị Phân Tìm Kiếm

```cpp
#include <iostream>
using namespace std;

struct Node {
    int data;
    Node* left;
    Node* right;
    Node(int val) : data(val), left(NULL), right(NULL) {}
};

Node* insert(Node* root, int key) {
    if (!root) return new Node(key);
    if (key < root->data) root->left = insert(root->left, key);
    else root->right = insert(root->right, key);
    return root;
}

void inorder(Node* root) {
    if (!root) return;
    inorder(root->left);
    cout << root->data << " ";
    inorder(root->right);
}

int main() {
    Node* root = NULL;
    root = insert(root, 50);
    insert(root, 30);
    insert(root, 20);
    insert(root, 40);
    insert(root, 70);
    insert(root, 60);
    insert(root, 80);

    cout << "Inorder traversal: ";
    inorder(root);
    return 0;
}
```

---

## 3. Kiến Thức Nâng Cao Về C++

### 3.1 Kỹ Thuật Tối Ưu
- **Sử dụng `inline` functions**: Giảm thời gian gọi hàm.
- **Sử dụng `constexpr`**: Đánh giá hằng số thời gian biên dịch, giúp tối ưu hiệu năng.
- **Tránh sử dụng `std::endl` nếu không cần thiết**: `endl` sẽ làm chậm chương trình do yêu cầu làm trống bộ đệm sau mỗi lần in.

### 3.2 Ví Dụ Chi Tiết

```cpp
#include <iostream>
using namespace std;

inline int square(int x) {
    return x * x;
}

int main() {
    int a = 5;
    cout << "Bình phương của " << a << " là " << square(a) << endl;
    return 0;
}
```
