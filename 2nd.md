# 2nd

```cpp
class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        if (!root) {
            return nullptr;
        }
        queue<TreeNode*> unvisited;
        unvisited.push(root);

        while (!unvisited.empty()) {
            TreeNode* current = unvisited.front();
            unvisited.pop();    
            swap(current->left, current->right);
            if (current->left) {
                unvisited.push(current->left);
            }
            if (current->right) {
                unvisited.push(current->right);
            }
        }
        return root;
    }
};
```

# 2-2
再帰
```cpp
class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        if (!root) {
            return nullptr;
        }  

        swap(root->left, root->right);
        if (root->left) {
            invertTree(root->left);
        }
        if (root->right) {
            invertTree(root->right);
        }
        
        return root;
    }
};
```
