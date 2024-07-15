# 1st
後から見返すとコードが全然整理されていないと自覚する  
2段階目では整理できた
```cpp
class Solution {
public:
    TreeNode* invertTree(TreeNode* root) {
        // bfs, QUEUE　
        if(!root) {
            return nullptr;
        }

        queue<TreeNode*> node_queue;
        node_queue.push(root);  

        while(!node_queue.empty()) {
            TreeNode* current_node = node_queue.front();  
            node_queue.pop(); 
            if(current_node->left && current_node->right) {
                TreeNode* temp = current_node->left; 
                current_node->left = current_node->right;
                current_node->right = temp;
                node_queue.push(current_node->left);    
                node_queue.push(current_node->right);
            } else if (current_node->left) {
                current_node->right = current_node->left;
                current_node->left = nullptr;
                node_queue.push(current_node->right); 
            } else if (current_node->right) {
                current_node->left = current_node->right;
                current_node->right = nullptr;
                node_queue.push(current_node->left); 
            } else {
                continue;
            }
        }
        return root;
    }
}
```
