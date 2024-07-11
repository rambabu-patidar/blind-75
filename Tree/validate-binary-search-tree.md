# [Validate Binary Search Tree](https://leetcode.com/problems/validate-binary-search-tree/description/)

`Medium` `Tree` `BST`

## Wrong Intution

- If you try to that at every node you check its left is lesser than root and its right is greater than root, this will be wrong

                            5
                          1   8
                        0  2 4  9  (see this tree)

## Approaches

### 1. The inorder traversal of BST is sorted

Time Complexity: O(N)
Space Complexity: O(N) {Stack Space + inorder traversal array}

```c++
class Solution {
public:
    void inorder(TreeNode* root, vector<int>&inorderTraversal) {
        if (root == nullptr) {
            return;
        }

        inorder(root->left, inorderTraversal);

        inorderTraversal.push_back(root->val);

        inorder(root->right, inorderTraversal);
    }

    bool isValidBST(TreeNode* root) {
        vector<int> inorderTraversal;
        inorder(root, inorderTraversal);

        // if the array is sorted it is BST

        for (int i = 1; i < inorderTraversal.size(); i++) {
            if (inorderTraversal[i - 1] >= inorderTraversal[i]) {
                return false;
            }
        }
        return true;
    }
};
```

### 2. Do the iterative Inorder Traversal

Time Complexity: O(N)
Space Complexity: O(H) {Height of the tree, in wrost case N}

```c++

class Solution {
public:
    bool isValidBST(TreeNode* root) {
        stack<TreeNode*> st;
        TreeNode* curr = root;

        long long prevValue = LLONG_MIN;
        while (!st.empty() || curr != nullptr) {
            while (curr != nullptr) {
                st.push(curr);
                curr = curr->left;
            }

            curr = st.top();

            if (curr->val <= prevValue) {
                return false;
            }

            st.pop();
            prevValue = curr->val;
            curr = curr->right;
        }

        return true;
    }
};
```

### 3. Recursive Top Down approach

Time complexity: O(N)
Space complexity: O(H) {stack space}

```c++
class Solution {
public:

    bool isValidBSTUtil(TreeNode* root, long long min, long long max) {
        if (!root) {
            return true;
        }

        if (root->val < min || root->val > max) {
            return false;
        }

        return isValidBSTUtil(root->left, min, (long long)root->val - 1) &&
                isValidBSTUtil(root->right, (long long)root->val + 1, max);
    }

    bool isValidBST(TreeNode* root) {
        return isValidBSTUtil(root, LLONG_MIN, LLONG_MAX);
    }
};

```

### 4. See the Bottom Up approach really awesome
