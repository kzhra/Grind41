# 4th
おださんのコメントを受けて
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

            if (current) {
                swap(current->left, current->right);
                unvisited.push(current->left);
                unvisited.push(current->right);
            }
        }
        return root;
    }
};
```
