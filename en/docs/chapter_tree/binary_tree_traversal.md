---
comments: true
---

# 7.2 &nbsp; Binary tree traversal

From the perspective of physical structure, a tree is a data structure based on linked lists, hence its traversal method involves accessing nodes one by one through pointers. However, a tree is a non-linear data structure, which makes traversing a tree more complex than traversing a linked list, requiring the assistance of search algorithms to achieve.

Common traversal methods for binary trees include level-order traversal, preorder traversal, inorder traversal, and postorder traversal, among others.

## 7.2.1 &nbsp; Level-order traversal

As shown in the Figure 7-9 , "level-order traversal" traverses the binary tree from top to bottom, layer by layer, and accesses nodes in each layer in a left-to-right order.

Level-order traversal essentially belongs to "breadth-first traversal", also known as "breadth-first search (BFS)", which embodies a "circumferentially outward expanding" layer-by-layer traversal method.

![Level-order traversal of a binary tree](binary_tree_traversal.assets/binary_tree_bfs.png){ class="animation-figure" }

<p align="center"> Figure 7-9 &nbsp; Level-order traversal of a binary tree </p>

### 1. &nbsp; Code implementation

Breadth-first traversal is usually implemented with the help of a "queue". The queue follows the "first in, first out" rule, while breadth-first traversal follows the "layer-by-layer progression" rule, the underlying ideas of the two are consistent. The implementation code is as follows:

=== "Python"

    ```python title="binary_tree_bfs.py"
    def level_order(root: TreeNode | None) -> list[int]:
        """层序遍历"""
        # 初始化队列，加入根节点
        queue: deque[TreeNode] = deque()
        queue.append(root)
        # 初始化一个列表，用于保存遍历序列
        res = []
        while queue:
            node: TreeNode = queue.popleft()  # 队列出队
            res.append(node.val)  # 保存节点值
            if node.left is not None:
                queue.append(node.left)  # 左子节点入队
            if node.right is not None:
                queue.append(node.right)  # 右子节点入队
        return res
    ```

=== "C++"

    ```cpp title="binary_tree_bfs.cpp"
    /* 层序遍历 */
    vector<int> levelOrder(TreeNode *root) {
        // 初始化队列，加入根节点
        queue<TreeNode *> queue;
        queue.push(root);
        // 初始化一个列表，用于保存遍历序列
        vector<int> vec;
        while (!queue.empty()) {
            TreeNode *node = queue.front();
            queue.pop();              // 队列出队
            vec.push_back(node->val); // 保存节点值
            if (node->left != nullptr)
                queue.push(node->left); // 左子节点入队
            if (node->right != nullptr)
                queue.push(node->right); // 右子节点入队
        }
        return vec;
    }
    ```

=== "Java"

    ```java title="binary_tree_bfs.java"
    /* 层序遍历 */
    List<Integer> levelOrder(TreeNode root) {
        // 初始化队列，加入根节点
        Queue<TreeNode> queue = new LinkedList<>();
        queue.add(root);
        // 初始化一个列表，用于保存遍历序列
        List<Integer> list = new ArrayList<>();
        while (!queue.isEmpty()) {
            TreeNode node = queue.poll(); // 队列出队
            list.add(node.val);           // 保存节点值
            if (node.left != null)
                queue.offer(node.left);   // 左子节点入队
            if (node.right != null)
                queue.offer(node.right);  // 右子节点入队
        }
        return list;
    }
    ```

=== "C#"

    ```csharp title="binary_tree_bfs.cs"
    /* 层序遍历 */
    List<int> LevelOrder(TreeNode root) {
        // 初始化队列，加入根节点
        Queue<TreeNode> queue = new();
        queue.Enqueue(root);
        // 初始化一个列表，用于保存遍历序列
        List<int> list = [];
        while (queue.Count != 0) {
            TreeNode node = queue.Dequeue(); // 队列出队
            list.Add(node.val!.Value);       // 保存节点值
            if (node.left != null)
                queue.Enqueue(node.left);    // 左子节点入队
            if (node.right != null)
                queue.Enqueue(node.right);   // 右子节点入队
        }
        return list;
    }
    ```

=== "Go"

    ```go title="binary_tree_bfs.go"
    /* 层序遍历 */
    func levelOrder(root *TreeNode) []any {
        // 初始化队列，加入根节点
        queue := list.New()
        queue.PushBack(root)
        // 初始化一个切片，用于保存遍历序列
        nums := make([]any, 0)
        for queue.Len() > 0 {
            // 队列出队
            node := queue.Remove(queue.Front()).(*TreeNode)
            // 保存节点值
            nums = append(nums, node.Val)
            if node.Left != nil {
                // 左子节点入队
                queue.PushBack(node.Left)
            }
            if node.Right != nil {
                // 右子节点入队
                queue.PushBack(node.Right)
            }
        }
        return nums
    }
    ```

=== "Swift"

    ```swift title="binary_tree_bfs.swift"
    /* 层序遍历 */
    func levelOrder(root: TreeNode) -> [Int] {
        // 初始化队列，加入根节点
        var queue: [TreeNode] = [root]
        // 初始化一个列表，用于保存遍历序列
        var list: [Int] = []
        while !queue.isEmpty {
            let node = queue.removeFirst() // 队列出队
            list.append(node.val) // 保存节点值
            if let left = node.left {
                queue.append(left) // 左子节点入队
            }
            if let right = node.right {
                queue.append(right) // 右子节点入队
            }
        }
        return list
    }
    ```

=== "JS"

    ```javascript title="binary_tree_bfs.js"
    /* 层序遍历 */
    function levelOrder(root) {
        // 初始化队列，加入根节点
        const queue = [root];
        // 初始化一个列表，用于保存遍历序列
        const list = [];
        while (queue.length) {
            let node = queue.shift(); // 队列出队
            list.push(node.val); // 保存节点值
            if (node.left) queue.push(node.left); // 左子节点入队
            if (node.right) queue.push(node.right); // 右子节点入队
        }
        return list;
    }
    ```

=== "TS"

    ```typescript title="binary_tree_bfs.ts"
    /* 层序遍历 */
    function levelOrder(root: TreeNode | null): number[] {
        // 初始化队列，加入根节点
        const queue = [root];
        // 初始化一个列表，用于保存遍历序列
        const list: number[] = [];
        while (queue.length) {
            let node = queue.shift() as TreeNode; // 队列出队
            list.push(node.val); // 保存节点值
            if (node.left) {
                queue.push(node.left); // 左子节点入队
            }
            if (node.right) {
                queue.push(node.right); // 右子节点入队
            }
        }
        return list;
    }
    ```

=== "Dart"

    ```dart title="binary_tree_bfs.dart"
    /* 层序遍历 */
    List<int> levelOrder(TreeNode? root) {
      // 初始化队列，加入根节点
      Queue<TreeNode?> queue = Queue();
      queue.add(root);
      // 初始化一个列表，用于保存遍历序列
      List<int> res = [];
      while (queue.isNotEmpty) {
        TreeNode? node = queue.removeFirst(); // 队列出队
        res.add(node!.val); // 保存节点值
        if (node.left != null) queue.add(node.left); // 左子节点入队
        if (node.right != null) queue.add(node.right); // 右子节点入队
      }
      return res;
    }
    ```

=== "Rust"

    ```rust title="binary_tree_bfs.rs"
    /* 层序遍历 */
    fn level_order(root: &Rc<RefCell<TreeNode>>) -> Vec<i32> {
        // 初始化队列，加入根节点
        let mut que = VecDeque::new();
        que.push_back(root.clone());
        // 初始化一个列表，用于保存遍历序列
        let mut vec = Vec::new();

        while let Some(node) = que.pop_front() {
            // 队列出队
            vec.push(node.borrow().val); // 保存节点值
            if let Some(left) = node.borrow().left.as_ref() {
                que.push_back(left.clone()); // 左子节点入队
            }
            if let Some(right) = node.borrow().right.as_ref() {
                que.push_back(right.clone()); // 右子节点入队
            };
        }
        vec
    }
    ```

=== "C"

    ```c title="binary_tree_bfs.c"
    /* 层序遍历 */
    int *levelOrder(TreeNode *root, int *size) {
        /* 辅助队列 */
        int front, rear;
        int index, *arr;
        TreeNode *node;
        TreeNode **queue;

        /* 辅助队列 */
        queue = (TreeNode **)malloc(sizeof(TreeNode *) * MAX_SIZE);
        // 队列指针
        front = 0, rear = 0;
        // 加入根节点
        queue[rear++] = root;
        // 初始化一个列表，用于保存遍历序列
        /* 辅助数组 */
        arr = (int *)malloc(sizeof(int) * MAX_SIZE);
        // 数组指针
        index = 0;
        while (front < rear) {
            // 队列出队
            node = queue[front++];
            // 保存节点值
            arr[index++] = node->val;
            if (node->left != NULL) {
                // 左子节点入队
                queue[rear++] = node->left;
            }
            if (node->right != NULL) {
                // 右子节点入队
                queue[rear++] = node->right;
            }
        }
        // 更新数组长度的值
        *size = index;
        arr = realloc(arr, sizeof(int) * (*size));

        // 释放辅助数组空间
        free(queue);
        return arr;
    }
    ```

=== "Kotlin"

    ```kotlin title="binary_tree_bfs.kt"
    /* 层序遍历 */
    fun levelOrder(root: TreeNode?): MutableList<Int> {
        // 初始化队列，加入根节点
        val queue = LinkedList<TreeNode?>()
        queue.add(root)
        // 初始化一个列表，用于保存遍历序列
        val list = mutableListOf<Int>()
        while (queue.isNotEmpty()) {
            val node = queue.poll()      // 队列出队
            list.add(node?._val!!)      // 保存节点值
            if (node.left != null)
                queue.offer(node.left)   // 左子节点入队
            if (node.right != null)
                queue.offer(node.right)  // 右子节点入队
        }
        return list
    }
    ```

=== "Ruby"

    ```ruby title="binary_tree_bfs.rb"
    [class]{}-[func]{level_order}
    ```

=== "Zig"

    ```zig title="binary_tree_bfs.zig"
    // 层序遍历
    fn levelOrder(comptime T: type, mem_allocator: std.mem.Allocator, root: *inc.TreeNode(T)) !std.ArrayList(T) {
        // 初始化队列，加入根节点
        const L = std.TailQueue(*inc.TreeNode(T));
        var queue = L{};
        var root_node = try mem_allocator.create(L.Node);
        root_node.data = root;
        queue.append(root_node); 
        // 初始化一个列表，用于保存遍历序列
        var list = std.ArrayList(T).init(std.heap.page_allocator);
        while (queue.len > 0) {
            var queue_node = queue.popFirst().?;    // 队列出队
            var node = queue_node.data;
            try list.append(node.val);              // 保存节点值
            if (node.left != null) {
                var tmp_node = try mem_allocator.create(L.Node);
                tmp_node.data = node.left.?;
                queue.append(tmp_node);             // 左子节点入队
            }
            if (node.right != null) {
                var tmp_node = try mem_allocator.create(L.Node);
                tmp_node.data = node.right.?;
                queue.append(tmp_node);             // 右子节点入队
            }        
        }
        return list;
    }
    ```

??? pythontutor "Code Visualization"

    <div style="height: 549px; width: 100%;"><iframe class="pythontutor-iframe" src="https://pythontutor.com/iframe-embed.html#code=from%20collections%20import%20deque%0A%0Aclass%20TreeNode%3A%0A%20%20%20%20%22%22%22%E4%BA%8C%E5%8F%89%E6%A0%91%E8%8A%82%E7%82%B9%E7%B1%BB%22%22%22%0A%20%20%20%20def%20__init__%28self,%20val%3A%20int%29%3A%0A%20%20%20%20%20%20%20%20self.val%3A%20int%20%3D%20val%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20%E8%8A%82%E7%82%B9%E5%80%BC%0A%20%20%20%20%20%20%20%20self.left%3A%20TreeNode%20%7C%20None%20%3D%20None%20%20%23%20%E5%B7%A6%E5%AD%90%E8%8A%82%E7%82%B9%E5%BC%95%E7%94%A8%0A%20%20%20%20%20%20%20%20self.right%3A%20TreeNode%20%7C%20None%20%3D%20None%20%23%20%E5%8F%B3%E5%AD%90%E8%8A%82%E7%82%B9%E5%BC%95%E7%94%A8%0A%0Adef%20list_to_tree_dfs%28arr%3A%20list%5Bint%5D,%20i%3A%20int%29%20-%3E%20TreeNode%20%7C%20None%3A%0A%20%20%20%20%22%22%22%E5%B0%86%E5%88%97%E8%A1%A8%E5%8F%8D%E5%BA%8F%E5%88%97%E5%8C%96%E4%B8%BA%E4%BA%8C%E5%8F%89%E6%A0%91%EF%BC%9A%E9%80%92%E5%BD%92%22%22%22%0A%20%20%20%20%23%20%E5%A6%82%E6%9E%9C%E7%B4%A2%E5%BC%95%E8%B6%85%E5%87%BA%E6%95%B0%E7%BB%84%E9%95%BF%E5%BA%A6%EF%BC%8C%E6%88%96%E8%80%85%E5%AF%B9%E5%BA%94%E7%9A%84%E5%85%83%E7%B4%A0%E4%B8%BA%20None%20%EF%BC%8C%E5%88%99%E8%BF%94%E5%9B%9E%20None%0A%20%20%20%20if%20i%20%3C%200%20or%20i%20%3E%3D%20len%28arr%29%20or%20arr%5Bi%5D%20is%20None%3A%0A%20%20%20%20%20%20%20%20return%20None%0A%20%20%20%20%23%20%E6%9E%84%E5%BB%BA%E5%BD%93%E5%89%8D%E8%8A%82%E7%82%B9%0A%20%20%20%20root%20%3D%20TreeNode%28arr%5Bi%5D%29%0A%20%20%20%20%23%20%E9%80%92%E5%BD%92%E6%9E%84%E5%BB%BA%E5%B7%A6%E5%8F%B3%E5%AD%90%E6%A0%91%0A%20%20%20%20root.left%20%3D%20list_to_tree_dfs%28arr,%202%20*%20i%20%2B%201%29%0A%20%20%20%20root.right%20%3D%20list_to_tree_dfs%28arr,%202%20*%20i%20%2B%202%29%0A%20%20%20%20return%20root%0A%0Adef%20list_to_tree%28arr%3A%20list%5Bint%5D%29%20-%3E%20TreeNode%20%7C%20None%3A%0A%20%20%20%20%22%22%22%E5%B0%86%E5%88%97%E8%A1%A8%E5%8F%8D%E5%BA%8F%E5%88%97%E5%8C%96%E4%B8%BA%E4%BA%8C%E5%8F%89%E6%A0%91%22%22%22%0A%20%20%20%20return%20list_to_tree_dfs%28arr,%200%29%0A%0A%0Adef%20level_order%28root%3A%20TreeNode%20%7C%20None%29%20-%3E%20list%5Bint%5D%3A%0A%20%20%20%20%22%22%22%E5%B1%82%E5%BA%8F%E9%81%8D%E5%8E%86%22%22%22%0A%20%20%20%20%23%20%E5%88%9D%E5%A7%8B%E5%8C%96%E9%98%9F%E5%88%97%EF%BC%8C%E5%8A%A0%E5%85%A5%E6%A0%B9%E8%8A%82%E7%82%B9%0A%20%20%20%20queue%3A%20deque%5BTreeNode%5D%20%3D%20deque%28%29%0A%20%20%20%20queue.append%28root%29%0A%20%20%20%20%23%20%E5%88%9D%E5%A7%8B%E5%8C%96%E4%B8%80%E4%B8%AA%E5%88%97%E8%A1%A8%EF%BC%8C%E7%94%A8%E4%BA%8E%E4%BF%9D%E5%AD%98%E9%81%8D%E5%8E%86%E5%BA%8F%E5%88%97%0A%20%20%20%20res%20%3D%20%5B%5D%0A%20%20%20%20while%20queue%3A%0A%20%20%20%20%20%20%20%20node%3A%20TreeNode%20%3D%20queue.popleft%28%29%20%20%23%20%E9%98%9F%E5%88%97%E5%87%BA%E9%98%9F%0A%20%20%20%20%20%20%20%20res.append%28node.val%29%20%20%23%20%E4%BF%9D%E5%AD%98%E8%8A%82%E7%82%B9%E5%80%BC%0A%20%20%20%20%20%20%20%20if%20node.left%20is%20not%20None%3A%0A%20%20%20%20%20%20%20%20%20%20%20%20queue.append%28node.left%29%20%20%23%20%E5%B7%A6%E5%AD%90%E8%8A%82%E7%82%B9%E5%85%A5%E9%98%9F%0A%20%20%20%20%20%20%20%20if%20node.right%20is%20not%20None%3A%0A%20%20%20%20%20%20%20%20%20%20%20%20queue.append%28node.right%29%20%20%23%20%E5%8F%B3%E5%AD%90%E8%8A%82%E7%82%B9%E5%85%A5%E9%98%9F%0A%20%20%20%20return%20res%0A%0A%22%22%22Driver%20Code%22%22%22%0Aif%20__name__%20%3D%3D%20%22__main__%22%3A%0A%20%20%20%20%23%20%E5%88%9D%E5%A7%8B%E5%8C%96%E4%BA%8C%E5%8F%89%E6%A0%91%0A%20%20%20%20%23%20%E8%BF%99%E9%87%8C%E5%80%9F%E5%8A%A9%E4%BA%86%E4%B8%80%E4%B8%AA%E4%BB%8E%E6%95%B0%E7%BB%84%E7%9B%B4%E6%8E%A5%E7%94%9F%E6%88%90%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E5%87%BD%E6%95%B0%0A%20%20%20%20root%20%3D%20list_to_tree%28arr%3D%5B1,%202,%203,%204,%205,%206,%207%5D%29%0A%0A%20%20%20%20%23%20%E5%B1%82%E5%BA%8F%E9%81%8D%E5%8E%86%0A%20%20%20%20res%20%3D%20level_order%28root%29%0A%20%20%20%20print%28%22%5Cn%E5%B1%82%E5%BA%8F%E9%81%8D%E5%8E%86%E7%9A%84%E8%8A%82%E7%82%B9%E6%89%93%E5%8D%B0%E5%BA%8F%E5%88%97%20%3D%20%22,%20res%29&codeDivHeight=472&codeDivWidth=350&cumulative=false&curInstr=127&heapPrimitives=nevernest&origin=opt-frontend.js&py=311&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe></div>
    <div style="margin-top: 5px;"><a href="https://pythontutor.com/iframe-embed.html#code=from%20collections%20import%20deque%0A%0Aclass%20TreeNode%3A%0A%20%20%20%20%22%22%22%E4%BA%8C%E5%8F%89%E6%A0%91%E8%8A%82%E7%82%B9%E7%B1%BB%22%22%22%0A%20%20%20%20def%20__init__%28self,%20val%3A%20int%29%3A%0A%20%20%20%20%20%20%20%20self.val%3A%20int%20%3D%20val%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20%E8%8A%82%E7%82%B9%E5%80%BC%0A%20%20%20%20%20%20%20%20self.left%3A%20TreeNode%20%7C%20None%20%3D%20None%20%20%23%20%E5%B7%A6%E5%AD%90%E8%8A%82%E7%82%B9%E5%BC%95%E7%94%A8%0A%20%20%20%20%20%20%20%20self.right%3A%20TreeNode%20%7C%20None%20%3D%20None%20%23%20%E5%8F%B3%E5%AD%90%E8%8A%82%E7%82%B9%E5%BC%95%E7%94%A8%0A%0Adef%20list_to_tree_dfs%28arr%3A%20list%5Bint%5D,%20i%3A%20int%29%20-%3E%20TreeNode%20%7C%20None%3A%0A%20%20%20%20%22%22%22%E5%B0%86%E5%88%97%E8%A1%A8%E5%8F%8D%E5%BA%8F%E5%88%97%E5%8C%96%E4%B8%BA%E4%BA%8C%E5%8F%89%E6%A0%91%EF%BC%9A%E9%80%92%E5%BD%92%22%22%22%0A%20%20%20%20%23%20%E5%A6%82%E6%9E%9C%E7%B4%A2%E5%BC%95%E8%B6%85%E5%87%BA%E6%95%B0%E7%BB%84%E9%95%BF%E5%BA%A6%EF%BC%8C%E6%88%96%E8%80%85%E5%AF%B9%E5%BA%94%E7%9A%84%E5%85%83%E7%B4%A0%E4%B8%BA%20None%20%EF%BC%8C%E5%88%99%E8%BF%94%E5%9B%9E%20None%0A%20%20%20%20if%20i%20%3C%200%20or%20i%20%3E%3D%20len%28arr%29%20or%20arr%5Bi%5D%20is%20None%3A%0A%20%20%20%20%20%20%20%20return%20None%0A%20%20%20%20%23%20%E6%9E%84%E5%BB%BA%E5%BD%93%E5%89%8D%E8%8A%82%E7%82%B9%0A%20%20%20%20root%20%3D%20TreeNode%28arr%5Bi%5D%29%0A%20%20%20%20%23%20%E9%80%92%E5%BD%92%E6%9E%84%E5%BB%BA%E5%B7%A6%E5%8F%B3%E5%AD%90%E6%A0%91%0A%20%20%20%20root.left%20%3D%20list_to_tree_dfs%28arr,%202%20*%20i%20%2B%201%29%0A%20%20%20%20root.right%20%3D%20list_to_tree_dfs%28arr,%202%20*%20i%20%2B%202%29%0A%20%20%20%20return%20root%0A%0Adef%20list_to_tree%28arr%3A%20list%5Bint%5D%29%20-%3E%20TreeNode%20%7C%20None%3A%0A%20%20%20%20%22%22%22%E5%B0%86%E5%88%97%E8%A1%A8%E5%8F%8D%E5%BA%8F%E5%88%97%E5%8C%96%E4%B8%BA%E4%BA%8C%E5%8F%89%E6%A0%91%22%22%22%0A%20%20%20%20return%20list_to_tree_dfs%28arr,%200%29%0A%0A%0Adef%20level_order%28root%3A%20TreeNode%20%7C%20None%29%20-%3E%20list%5Bint%5D%3A%0A%20%20%20%20%22%22%22%E5%B1%82%E5%BA%8F%E9%81%8D%E5%8E%86%22%22%22%0A%20%20%20%20%23%20%E5%88%9D%E5%A7%8B%E5%8C%96%E9%98%9F%E5%88%97%EF%BC%8C%E5%8A%A0%E5%85%A5%E6%A0%B9%E8%8A%82%E7%82%B9%0A%20%20%20%20queue%3A%20deque%5BTreeNode%5D%20%3D%20deque%28%29%0A%20%20%20%20queue.append%28root%29%0A%20%20%20%20%23%20%E5%88%9D%E5%A7%8B%E5%8C%96%E4%B8%80%E4%B8%AA%E5%88%97%E8%A1%A8%EF%BC%8C%E7%94%A8%E4%BA%8E%E4%BF%9D%E5%AD%98%E9%81%8D%E5%8E%86%E5%BA%8F%E5%88%97%0A%20%20%20%20res%20%3D%20%5B%5D%0A%20%20%20%20while%20queue%3A%0A%20%20%20%20%20%20%20%20node%3A%20TreeNode%20%3D%20queue.popleft%28%29%20%20%23%20%E9%98%9F%E5%88%97%E5%87%BA%E9%98%9F%0A%20%20%20%20%20%20%20%20res.append%28node.val%29%20%20%23%20%E4%BF%9D%E5%AD%98%E8%8A%82%E7%82%B9%E5%80%BC%0A%20%20%20%20%20%20%20%20if%20node.left%20is%20not%20None%3A%0A%20%20%20%20%20%20%20%20%20%20%20%20queue.append%28node.left%29%20%20%23%20%E5%B7%A6%E5%AD%90%E8%8A%82%E7%82%B9%E5%85%A5%E9%98%9F%0A%20%20%20%20%20%20%20%20if%20node.right%20is%20not%20None%3A%0A%20%20%20%20%20%20%20%20%20%20%20%20queue.append%28node.right%29%20%20%23%20%E5%8F%B3%E5%AD%90%E8%8A%82%E7%82%B9%E5%85%A5%E9%98%9F%0A%20%20%20%20return%20res%0A%0A%22%22%22Driver%20Code%22%22%22%0Aif%20__name__%20%3D%3D%20%22__main__%22%3A%0A%20%20%20%20%23%20%E5%88%9D%E5%A7%8B%E5%8C%96%E4%BA%8C%E5%8F%89%E6%A0%91%0A%20%20%20%20%23%20%E8%BF%99%E9%87%8C%E5%80%9F%E5%8A%A9%E4%BA%86%E4%B8%80%E4%B8%AA%E4%BB%8E%E6%95%B0%E7%BB%84%E7%9B%B4%E6%8E%A5%E7%94%9F%E6%88%90%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E5%87%BD%E6%95%B0%0A%20%20%20%20root%20%3D%20list_to_tree%28arr%3D%5B1,%202,%203,%204,%205,%206,%207%5D%29%0A%0A%20%20%20%20%23%20%E5%B1%82%E5%BA%8F%E9%81%8D%E5%8E%86%0A%20%20%20%20res%20%3D%20level_order%28root%29%0A%20%20%20%20print%28%22%5Cn%E5%B1%82%E5%BA%8F%E9%81%8D%E5%8E%86%E7%9A%84%E8%8A%82%E7%82%B9%E6%89%93%E5%8D%B0%E5%BA%8F%E5%88%97%20%3D%20%22,%20res%29&codeDivHeight=800&codeDivWidth=600&cumulative=false&curInstr=127&heapPrimitives=nevernest&origin=opt-frontend.js&py=311&rawInputLstJSON=%5B%5D&textReferences=false" target="_blank" rel="noopener noreferrer">Full Screen ></a></div>

### 2. &nbsp; Complexity analysis

- **Time complexity is $O(n)$**: All nodes are visited once, using $O(n)$ time, where $n$ is the number of nodes.
- **Space complexity is $O(n)$**: In the worst case, i.e., a full binary tree, before traversing to the lowest level, the queue can contain at most $(n + 1) / 2$ nodes at the same time, occupying $O(n)$ space.

## 7.2.2 &nbsp; Preorder, inorder, and postorder traversal

Correspondingly, preorder, inorder, and postorder traversal all belong to "depth-first traversal", also known as "depth-first search (DFS)", which embodies a "proceed to the end first, then backtrack and continue" traversal method.

The Figure 7-10  shows the working principle of performing a depth-first traversal on a binary tree. **Depth-first traversal is like walking around the perimeter of the entire binary tree**, encountering three positions at each node, corresponding to preorder traversal, inorder traversal, and postorder traversal.

![Preorder, inorder, and postorder traversal of a binary search tree](binary_tree_traversal.assets/binary_tree_dfs.png){ class="animation-figure" }

<p align="center"> Figure 7-10 &nbsp; Preorder, inorder, and postorder traversal of a binary search tree </p>

### 1. &nbsp; Code implementation

Depth-first search is usually implemented based on recursion:

=== "Python"

    ```python title="binary_tree_dfs.py"
    def pre_order(root: TreeNode | None):
        """前序遍历"""
        if root is None:
            return
        # 访问优先级：根节点 -> 左子树 -> 右子树
        res.append(root.val)
        pre_order(root=root.left)
        pre_order(root=root.right)

    def in_order(root: TreeNode | None):
        """中序遍历"""
        if root is None:
            return
        # 访问优先级：左子树 -> 根节点 -> 右子树
        in_order(root=root.left)
        res.append(root.val)
        in_order(root=root.right)

    def post_order(root: TreeNode | None):
        """后序遍历"""
        if root is None:
            return
        # 访问优先级：左子树 -> 右子树 -> 根节点
        post_order(root=root.left)
        post_order(root=root.right)
        res.append(root.val)
    ```

=== "C++"

    ```cpp title="binary_tree_dfs.cpp"
    /* 前序遍历 */
    void preOrder(TreeNode *root) {
        if (root == nullptr)
            return;
        // 访问优先级：根节点 -> 左子树 -> 右子树
        vec.push_back(root->val);
        preOrder(root->left);
        preOrder(root->right);
    }

    /* 中序遍历 */
    void inOrder(TreeNode *root) {
        if (root == nullptr)
            return;
        // 访问优先级：左子树 -> 根节点 -> 右子树
        inOrder(root->left);
        vec.push_back(root->val);
        inOrder(root->right);
    }

    /* 后序遍历 */
    void postOrder(TreeNode *root) {
        if (root == nullptr)
            return;
        // 访问优先级：左子树 -> 右子树 -> 根节点
        postOrder(root->left);
        postOrder(root->right);
        vec.push_back(root->val);
    }
    ```

=== "Java"

    ```java title="binary_tree_dfs.java"
    /* 前序遍历 */
    void preOrder(TreeNode root) {
        if (root == null)
            return;
        // 访问优先级：根节点 -> 左子树 -> 右子树
        list.add(root.val);
        preOrder(root.left);
        preOrder(root.right);
    }

    /* 中序遍历 */
    void inOrder(TreeNode root) {
        if (root == null)
            return;
        // 访问优先级：左子树 -> 根节点 -> 右子树
        inOrder(root.left);
        list.add(root.val);
        inOrder(root.right);
    }

    /* 后序遍历 */
    void postOrder(TreeNode root) {
        if (root == null)
            return;
        // 访问优先级：左子树 -> 右子树 -> 根节点
        postOrder(root.left);
        postOrder(root.right);
        list.add(root.val);
    }
    ```

=== "C#"

    ```csharp title="binary_tree_dfs.cs"
    /* 前序遍历 */
    void PreOrder(TreeNode? root) {
        if (root == null) return;
        // 访问优先级：根节点 -> 左子树 -> 右子树
        list.Add(root.val!.Value);
        PreOrder(root.left);
        PreOrder(root.right);
    }

    /* 中序遍历 */
    void InOrder(TreeNode? root) {
        if (root == null) return;
        // 访问优先级：左子树 -> 根节点 -> 右子树
        InOrder(root.left);
        list.Add(root.val!.Value);
        InOrder(root.right);
    }

    /* 后序遍历 */
    void PostOrder(TreeNode? root) {
        if (root == null) return;
        // 访问优先级：左子树 -> 右子树 -> 根节点
        PostOrder(root.left);
        PostOrder(root.right);
        list.Add(root.val!.Value);
    }
    ```

=== "Go"

    ```go title="binary_tree_dfs.go"
    /* 前序遍历 */
    func preOrder(node *TreeNode) {
        if node == nil {
            return
        }
        // 访问优先级：根节点 -> 左子树 -> 右子树
        nums = append(nums, node.Val)
        preOrder(node.Left)
        preOrder(node.Right)
    }

    /* 中序遍历 */
    func inOrder(node *TreeNode) {
        if node == nil {
            return
        }
        // 访问优先级：左子树 -> 根节点 -> 右子树
        inOrder(node.Left)
        nums = append(nums, node.Val)
        inOrder(node.Right)
    }

    /* 后序遍历 */
    func postOrder(node *TreeNode) {
        if node == nil {
            return
        }
        // 访问优先级：左子树 -> 右子树 -> 根节点
        postOrder(node.Left)
        postOrder(node.Right)
        nums = append(nums, node.Val)
    }
    ```

=== "Swift"

    ```swift title="binary_tree_dfs.swift"
    /* 前序遍历 */
    func preOrder(root: TreeNode?) {
        guard let root = root else {
            return
        }
        // 访问优先级：根节点 -> 左子树 -> 右子树
        list.append(root.val)
        preOrder(root: root.left)
        preOrder(root: root.right)
    }

    /* 中序遍历 */
    func inOrder(root: TreeNode?) {
        guard let root = root else {
            return
        }
        // 访问优先级：左子树 -> 根节点 -> 右子树
        inOrder(root: root.left)
        list.append(root.val)
        inOrder(root: root.right)
    }

    /* 后序遍历 */
    func postOrder(root: TreeNode?) {
        guard let root = root else {
            return
        }
        // 访问优先级：左子树 -> 右子树 -> 根节点
        postOrder(root: root.left)
        postOrder(root: root.right)
        list.append(root.val)
    }
    ```

=== "JS"

    ```javascript title="binary_tree_dfs.js"
    /* 前序遍历 */
    function preOrder(root) {
        if (root === null) return;
        // 访问优先级：根节点 -> 左子树 -> 右子树
        list.push(root.val);
        preOrder(root.left);
        preOrder(root.right);
    }

    /* 中序遍历 */
    function inOrder(root) {
        if (root === null) return;
        // 访问优先级：左子树 -> 根节点 -> 右子树
        inOrder(root.left);
        list.push(root.val);
        inOrder(root.right);
    }

    /* 后序遍历 */
    function postOrder(root) {
        if (root === null) return;
        // 访问优先级：左子树 -> 右子树 -> 根节点
        postOrder(root.left);
        postOrder(root.right);
        list.push(root.val);
    }
    ```

=== "TS"

    ```typescript title="binary_tree_dfs.ts"
    /* 前序遍历 */
    function preOrder(root: TreeNode | null): void {
        if (root === null) {
            return;
        }
        // 访问优先级：根节点 -> 左子树 -> 右子树
        list.push(root.val);
        preOrder(root.left);
        preOrder(root.right);
    }

    /* 中序遍历 */
    function inOrder(root: TreeNode | null): void {
        if (root === null) {
            return;
        }
        // 访问优先级：左子树 -> 根节点 -> 右子树
        inOrder(root.left);
        list.push(root.val);
        inOrder(root.right);
    }

    /* 后序遍历 */
    function postOrder(root: TreeNode | null): void {
        if (root === null) {
            return;
        }
        // 访问优先级：左子树 -> 右子树 -> 根节点
        postOrder(root.left);
        postOrder(root.right);
        list.push(root.val);
    }
    ```

=== "Dart"

    ```dart title="binary_tree_dfs.dart"
    /* 前序遍历 */
    void preOrder(TreeNode? node) {
      if (node == null) return;
      // 访问优先级：根节点 -> 左子树 -> 右子树
      list.add(node.val);
      preOrder(node.left);
      preOrder(node.right);
    }

    /* 中序遍历 */
    void inOrder(TreeNode? node) {
      if (node == null) return;
      // 访问优先级：左子树 -> 根节点 -> 右子树
      inOrder(node.left);
      list.add(node.val);
      inOrder(node.right);
    }

    /* 后序遍历 */
    void postOrder(TreeNode? node) {
      if (node == null) return;
      // 访问优先级：左子树 -> 右子树 -> 根节点
      postOrder(node.left);
      postOrder(node.right);
      list.add(node.val);
    }
    ```

=== "Rust"

    ```rust title="binary_tree_dfs.rs"
    /* 前序遍历 */
    fn pre_order(root: Option<&Rc<RefCell<TreeNode>>>) -> Vec<i32> {
        let mut result = vec![];

        if let Some(node) = root {
            // 访问优先级：根节点 -> 左子树 -> 右子树
            result.push(node.borrow().val);
            result.extend(pre_order(node.borrow().left.as_ref()));
            result.extend(pre_order(node.borrow().right.as_ref()));
        }
        result
    }

    /* 中序遍历 */
    fn in_order(root: Option<&Rc<RefCell<TreeNode>>>) -> Vec<i32> {
        let mut result = vec![];

        if let Some(node) = root {
            // 访问优先级：左子树 -> 根节点 -> 右子树
            result.extend(in_order(node.borrow().left.as_ref()));
            result.push(node.borrow().val);
            result.extend(in_order(node.borrow().right.as_ref()));
        }
        result
    }

    /* 后序遍历 */
    fn post_order(root: Option<&Rc<RefCell<TreeNode>>>) -> Vec<i32> {
        let mut result = vec![];

        if let Some(node) = root {
            // 访问优先级：左子树 -> 右子树 -> 根节点
            result.extend(post_order(node.borrow().left.as_ref()));
            result.extend(post_order(node.borrow().right.as_ref()));
            result.push(node.borrow().val);
        }
        result
    }
    ```

=== "C"

    ```c title="binary_tree_dfs.c"
    /* 前序遍历 */
    void preOrder(TreeNode *root, int *size) {
        if (root == NULL)
            return;
        // 访问优先级：根节点 -> 左子树 -> 右子树
        arr[(*size)++] = root->val;
        preOrder(root->left, size);
        preOrder(root->right, size);
    }

    /* 中序遍历 */
    void inOrder(TreeNode *root, int *size) {
        if (root == NULL)
            return;
        // 访问优先级：左子树 -> 根节点 -> 右子树
        inOrder(root->left, size);
        arr[(*size)++] = root->val;
        inOrder(root->right, size);
    }

    /* 后序遍历 */
    void postOrder(TreeNode *root, int *size) {
        if (root == NULL)
            return;
        // 访问优先级：左子树 -> 右子树 -> 根节点
        postOrder(root->left, size);
        postOrder(root->right, size);
        arr[(*size)++] = root->val;
    }
    ```

=== "Kotlin"

    ```kotlin title="binary_tree_dfs.kt"
    /* 前序遍历 */
    fun preOrder(root: TreeNode?) {
        if (root == null) return
        // 访问优先级：根节点 -> 左子树 -> 右子树
        list.add(root._val)
        preOrder(root.left)
        preOrder(root.right)
    }

    /* 中序遍历 */
    fun inOrder(root: TreeNode?) {
        if (root == null) return
        // 访问优先级：左子树 -> 根节点 -> 右子树
        inOrder(root.left)
        list.add(root._val)
        inOrder(root.right)
    }

    /* 后序遍历 */
    fun postOrder(root: TreeNode?) {
        if (root == null) return
        // 访问优先级：左子树 -> 右子树 -> 根节点
        postOrder(root.left)
        postOrder(root.right)
        list.add(root._val)
    }
    ```

=== "Ruby"

    ```ruby title="binary_tree_dfs.rb"
    [class]{}-[func]{pre_order}

    [class]{}-[func]{in_order}

    [class]{}-[func]{post_order}
    ```

=== "Zig"

    ```zig title="binary_tree_dfs.zig"
    // 前序遍历
    fn preOrder(comptime T: type, root: ?*inc.TreeNode(T)) !void {
        if (root == null) return;
        // 访问优先级：根节点 -> 左子树 -> 右子树
        try list.append(root.?.val);
        try preOrder(T, root.?.left);
        try preOrder(T, root.?.right);
    }

    // 中序遍历
    fn inOrder(comptime T: type, root: ?*inc.TreeNode(T)) !void {
        if (root == null) return;
        // 访问优先级：左子树 -> 根节点 -> 右子树
        try inOrder(T, root.?.left);
        try list.append(root.?.val);
        try inOrder(T, root.?.right);
    }

    // 后序遍历
    fn postOrder(comptime T: type, root: ?*inc.TreeNode(T)) !void {
        if (root == null) return;
        // 访问优先级：左子树 -> 右子树 -> 根节点
        try postOrder(T, root.?.left);
        try postOrder(T, root.?.right);
        try list.append(root.?.val);
    }
    ```

??? pythontutor "Code Visualization"

    <div style="height: 549px; width: 100%;"><iframe class="pythontutor-iframe" src="https://pythontutor.com/iframe-embed.html#code=class%20TreeNode%3A%0A%20%20%20%20%22%22%22%E4%BA%8C%E5%8F%89%E6%A0%91%E8%8A%82%E7%82%B9%E7%B1%BB%22%22%22%0A%20%20%20%20def%20__init__%28self,%20val%3A%20int%29%3A%0A%20%20%20%20%20%20%20%20self.val%3A%20int%20%3D%20val%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20%E8%8A%82%E7%82%B9%E5%80%BC%0A%20%20%20%20%20%20%20%20self.left%3A%20TreeNode%20%7C%20None%20%3D%20None%20%20%23%20%E5%B7%A6%E5%AD%90%E8%8A%82%E7%82%B9%E5%BC%95%E7%94%A8%0A%20%20%20%20%20%20%20%20self.right%3A%20TreeNode%20%7C%20None%20%3D%20None%20%23%20%E5%8F%B3%E5%AD%90%E8%8A%82%E7%82%B9%E5%BC%95%E7%94%A8%0A%0Adef%20list_to_tree_dfs%28arr%3A%20list%5Bint%5D,%20i%3A%20int%29%20-%3E%20TreeNode%20%7C%20None%3A%0A%20%20%20%20%22%22%22%E5%B0%86%E5%88%97%E8%A1%A8%E5%8F%8D%E5%BA%8F%E5%88%97%E5%8C%96%E4%B8%BA%E4%BA%8C%E5%8F%89%E6%A0%91%EF%BC%9A%E9%80%92%E5%BD%92%22%22%22%0A%20%20%20%20%23%20%E5%A6%82%E6%9E%9C%E7%B4%A2%E5%BC%95%E8%B6%85%E5%87%BA%E6%95%B0%E7%BB%84%E9%95%BF%E5%BA%A6%EF%BC%8C%E6%88%96%E8%80%85%E5%AF%B9%E5%BA%94%E7%9A%84%E5%85%83%E7%B4%A0%E4%B8%BA%20None%20%EF%BC%8C%E5%88%99%E8%BF%94%E5%9B%9E%20None%0A%20%20%20%20if%20i%20%3C%200%20or%20i%20%3E%3D%20len%28arr%29%20or%20arr%5Bi%5D%20is%20None%3A%0A%20%20%20%20%20%20%20%20return%20None%0A%20%20%20%20%23%20%E6%9E%84%E5%BB%BA%E5%BD%93%E5%89%8D%E8%8A%82%E7%82%B9%0A%20%20%20%20root%20%3D%20TreeNode%28arr%5Bi%5D%29%0A%20%20%20%20%23%20%E9%80%92%E5%BD%92%E6%9E%84%E5%BB%BA%E5%B7%A6%E5%8F%B3%E5%AD%90%E6%A0%91%0A%20%20%20%20root.left%20%3D%20list_to_tree_dfs%28arr,%202%20*%20i%20%2B%201%29%0A%20%20%20%20root.right%20%3D%20list_to_tree_dfs%28arr,%202%20*%20i%20%2B%202%29%0A%20%20%20%20return%20root%0A%0Adef%20list_to_tree%28arr%3A%20list%5Bint%5D%29%20-%3E%20TreeNode%20%7C%20None%3A%0A%20%20%20%20%22%22%22%E5%B0%86%E5%88%97%E8%A1%A8%E5%8F%8D%E5%BA%8F%E5%88%97%E5%8C%96%E4%B8%BA%E4%BA%8C%E5%8F%89%E6%A0%91%22%22%22%0A%20%20%20%20return%20list_to_tree_dfs%28arr,%200%29%0A%0A%0Adef%20pre_order%28root%3A%20TreeNode%20%7C%20None%29%3A%0A%20%20%20%20%22%22%22%E5%89%8D%E5%BA%8F%E9%81%8D%E5%8E%86%22%22%22%0A%20%20%20%20if%20root%20is%20None%3A%0A%20%20%20%20%20%20%20%20return%0A%20%20%20%20%23%20%E8%AE%BF%E9%97%AE%E4%BC%98%E5%85%88%E7%BA%A7%EF%BC%9A%E6%A0%B9%E8%8A%82%E7%82%B9%20-%3E%20%E5%B7%A6%E5%AD%90%E6%A0%91%20-%3E%20%E5%8F%B3%E5%AD%90%E6%A0%91%0A%20%20%20%20res.append%28root.val%29%0A%20%20%20%20pre_order%28root%3Droot.left%29%0A%20%20%20%20pre_order%28root%3Droot.right%29%0A%0Adef%20in_order%28root%3A%20TreeNode%20%7C%20None%29%3A%0A%20%20%20%20%22%22%22%E4%B8%AD%E5%BA%8F%E9%81%8D%E5%8E%86%22%22%22%0A%20%20%20%20if%20root%20is%20None%3A%0A%20%20%20%20%20%20%20%20return%0A%20%20%20%20%23%20%E8%AE%BF%E9%97%AE%E4%BC%98%E5%85%88%E7%BA%A7%EF%BC%9A%E5%B7%A6%E5%AD%90%E6%A0%91%20-%3E%20%E6%A0%B9%E8%8A%82%E7%82%B9%20-%3E%20%E5%8F%B3%E5%AD%90%E6%A0%91%0A%20%20%20%20in_order%28root%3Droot.left%29%0A%20%20%20%20res.append%28root.val%29%0A%20%20%20%20in_order%28root%3Droot.right%29%0A%0Adef%20post_order%28root%3A%20TreeNode%20%7C%20None%29%3A%0A%20%20%20%20%22%22%22%E5%90%8E%E5%BA%8F%E9%81%8D%E5%8E%86%22%22%22%0A%20%20%20%20if%20root%20is%20None%3A%0A%20%20%20%20%20%20%20%20return%0A%20%20%20%20%23%20%E8%AE%BF%E9%97%AE%E4%BC%98%E5%85%88%E7%BA%A7%EF%BC%9A%E5%B7%A6%E5%AD%90%E6%A0%91%20-%3E%20%E5%8F%B3%E5%AD%90%E6%A0%91%20-%3E%20%E6%A0%B9%E8%8A%82%E7%82%B9%0A%20%20%20%20post_order%28root%3Droot.left%29%0A%20%20%20%20post_order%28root%3Droot.right%29%0A%20%20%20%20res.append%28root.val%29%0A%0A%22%22%22Driver%20Code%22%22%22%0Aif%20__name__%20%3D%3D%20%22__main__%22%3A%0A%20%20%20%20%23%20%E5%88%9D%E5%A7%8B%E5%8C%96%E4%BA%8C%E5%8F%89%E6%A0%91%0A%20%20%20%20%23%20%E8%BF%99%E9%87%8C%E5%80%9F%E5%8A%A9%E4%BA%86%E4%B8%80%E4%B8%AA%E4%BB%8E%E6%95%B0%E7%BB%84%E7%9B%B4%E6%8E%A5%E7%94%9F%E6%88%90%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E5%87%BD%E6%95%B0%0A%20%20%20%20root%20%3D%20list_to_tree%28arr%3D%5B1,%202,%203,%204,%205,%206,%207%5D%29%0A%0A%20%20%20%20%23%20%E5%89%8D%E5%BA%8F%E9%81%8D%E5%8E%86%0A%20%20%20%20res%20%3D%20%5B%5D%0A%20%20%20%20pre_order%28root%29%0A%20%20%20%20print%28%22%5Cn%E5%89%8D%E5%BA%8F%E9%81%8D%E5%8E%86%E7%9A%84%E8%8A%82%E7%82%B9%E6%89%93%E5%8D%B0%E5%BA%8F%E5%88%97%20%3D%20%22,%20res%29%0A%0A%20%20%20%20%23%20%E4%B8%AD%E5%BA%8F%E9%81%8D%E5%8E%86%0A%20%20%20%20res.clear%28%29%0A%20%20%20%20in_order%28root%29%0A%20%20%20%20print%28%22%5Cn%E4%B8%AD%E5%BA%8F%E9%81%8D%E5%8E%86%E7%9A%84%E8%8A%82%E7%82%B9%E6%89%93%E5%8D%B0%E5%BA%8F%E5%88%97%20%3D%20%22,%20res%29%0A%0A%20%20%20%20%23%20%E5%90%8E%E5%BA%8F%E9%81%8D%E5%8E%86%0A%20%20%20%20res.clear%28%29%0A%20%20%20%20post_order%28root%29%0A%20%20%20%20print%28%22%5Cn%E5%90%8E%E5%BA%8F%E9%81%8D%E5%8E%86%E7%9A%84%E8%8A%82%E7%82%B9%E6%89%93%E5%8D%B0%E5%BA%8F%E5%88%97%20%3D%20%22,%20res%29&codeDivHeight=472&codeDivWidth=350&cumulative=false&curInstr=129&heapPrimitives=nevernest&origin=opt-frontend.js&py=311&rawInputLstJSON=%5B%5D&textReferences=false"> </iframe></div>
    <div style="margin-top: 5px;"><a href="https://pythontutor.com/iframe-embed.html#code=class%20TreeNode%3A%0A%20%20%20%20%22%22%22%E4%BA%8C%E5%8F%89%E6%A0%91%E8%8A%82%E7%82%B9%E7%B1%BB%22%22%22%0A%20%20%20%20def%20__init__%28self,%20val%3A%20int%29%3A%0A%20%20%20%20%20%20%20%20self.val%3A%20int%20%3D%20val%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%20%23%20%E8%8A%82%E7%82%B9%E5%80%BC%0A%20%20%20%20%20%20%20%20self.left%3A%20TreeNode%20%7C%20None%20%3D%20None%20%20%23%20%E5%B7%A6%E5%AD%90%E8%8A%82%E7%82%B9%E5%BC%95%E7%94%A8%0A%20%20%20%20%20%20%20%20self.right%3A%20TreeNode%20%7C%20None%20%3D%20None%20%23%20%E5%8F%B3%E5%AD%90%E8%8A%82%E7%82%B9%E5%BC%95%E7%94%A8%0A%0Adef%20list_to_tree_dfs%28arr%3A%20list%5Bint%5D,%20i%3A%20int%29%20-%3E%20TreeNode%20%7C%20None%3A%0A%20%20%20%20%22%22%22%E5%B0%86%E5%88%97%E8%A1%A8%E5%8F%8D%E5%BA%8F%E5%88%97%E5%8C%96%E4%B8%BA%E4%BA%8C%E5%8F%89%E6%A0%91%EF%BC%9A%E9%80%92%E5%BD%92%22%22%22%0A%20%20%20%20%23%20%E5%A6%82%E6%9E%9C%E7%B4%A2%E5%BC%95%E8%B6%85%E5%87%BA%E6%95%B0%E7%BB%84%E9%95%BF%E5%BA%A6%EF%BC%8C%E6%88%96%E8%80%85%E5%AF%B9%E5%BA%94%E7%9A%84%E5%85%83%E7%B4%A0%E4%B8%BA%20None%20%EF%BC%8C%E5%88%99%E8%BF%94%E5%9B%9E%20None%0A%20%20%20%20if%20i%20%3C%200%20or%20i%20%3E%3D%20len%28arr%29%20or%20arr%5Bi%5D%20is%20None%3A%0A%20%20%20%20%20%20%20%20return%20None%0A%20%20%20%20%23%20%E6%9E%84%E5%BB%BA%E5%BD%93%E5%89%8D%E8%8A%82%E7%82%B9%0A%20%20%20%20root%20%3D%20TreeNode%28arr%5Bi%5D%29%0A%20%20%20%20%23%20%E9%80%92%E5%BD%92%E6%9E%84%E5%BB%BA%E5%B7%A6%E5%8F%B3%E5%AD%90%E6%A0%91%0A%20%20%20%20root.left%20%3D%20list_to_tree_dfs%28arr,%202%20*%20i%20%2B%201%29%0A%20%20%20%20root.right%20%3D%20list_to_tree_dfs%28arr,%202%20*%20i%20%2B%202%29%0A%20%20%20%20return%20root%0A%0Adef%20list_to_tree%28arr%3A%20list%5Bint%5D%29%20-%3E%20TreeNode%20%7C%20None%3A%0A%20%20%20%20%22%22%22%E5%B0%86%E5%88%97%E8%A1%A8%E5%8F%8D%E5%BA%8F%E5%88%97%E5%8C%96%E4%B8%BA%E4%BA%8C%E5%8F%89%E6%A0%91%22%22%22%0A%20%20%20%20return%20list_to_tree_dfs%28arr,%200%29%0A%0A%0Adef%20pre_order%28root%3A%20TreeNode%20%7C%20None%29%3A%0A%20%20%20%20%22%22%22%E5%89%8D%E5%BA%8F%E9%81%8D%E5%8E%86%22%22%22%0A%20%20%20%20if%20root%20is%20None%3A%0A%20%20%20%20%20%20%20%20return%0A%20%20%20%20%23%20%E8%AE%BF%E9%97%AE%E4%BC%98%E5%85%88%E7%BA%A7%EF%BC%9A%E6%A0%B9%E8%8A%82%E7%82%B9%20-%3E%20%E5%B7%A6%E5%AD%90%E6%A0%91%20-%3E%20%E5%8F%B3%E5%AD%90%E6%A0%91%0A%20%20%20%20res.append%28root.val%29%0A%20%20%20%20pre_order%28root%3Droot.left%29%0A%20%20%20%20pre_order%28root%3Droot.right%29%0A%0Adef%20in_order%28root%3A%20TreeNode%20%7C%20None%29%3A%0A%20%20%20%20%22%22%22%E4%B8%AD%E5%BA%8F%E9%81%8D%E5%8E%86%22%22%22%0A%20%20%20%20if%20root%20is%20None%3A%0A%20%20%20%20%20%20%20%20return%0A%20%20%20%20%23%20%E8%AE%BF%E9%97%AE%E4%BC%98%E5%85%88%E7%BA%A7%EF%BC%9A%E5%B7%A6%E5%AD%90%E6%A0%91%20-%3E%20%E6%A0%B9%E8%8A%82%E7%82%B9%20-%3E%20%E5%8F%B3%E5%AD%90%E6%A0%91%0A%20%20%20%20in_order%28root%3Droot.left%29%0A%20%20%20%20res.append%28root.val%29%0A%20%20%20%20in_order%28root%3Droot.right%29%0A%0Adef%20post_order%28root%3A%20TreeNode%20%7C%20None%29%3A%0A%20%20%20%20%22%22%22%E5%90%8E%E5%BA%8F%E9%81%8D%E5%8E%86%22%22%22%0A%20%20%20%20if%20root%20is%20None%3A%0A%20%20%20%20%20%20%20%20return%0A%20%20%20%20%23%20%E8%AE%BF%E9%97%AE%E4%BC%98%E5%85%88%E7%BA%A7%EF%BC%9A%E5%B7%A6%E5%AD%90%E6%A0%91%20-%3E%20%E5%8F%B3%E5%AD%90%E6%A0%91%20-%3E%20%E6%A0%B9%E8%8A%82%E7%82%B9%0A%20%20%20%20post_order%28root%3Droot.left%29%0A%20%20%20%20post_order%28root%3Droot.right%29%0A%20%20%20%20res.append%28root.val%29%0A%0A%22%22%22Driver%20Code%22%22%22%0Aif%20__name__%20%3D%3D%20%22__main__%22%3A%0A%20%20%20%20%23%20%E5%88%9D%E5%A7%8B%E5%8C%96%E4%BA%8C%E5%8F%89%E6%A0%91%0A%20%20%20%20%23%20%E8%BF%99%E9%87%8C%E5%80%9F%E5%8A%A9%E4%BA%86%E4%B8%80%E4%B8%AA%E4%BB%8E%E6%95%B0%E7%BB%84%E7%9B%B4%E6%8E%A5%E7%94%9F%E6%88%90%E4%BA%8C%E5%8F%89%E6%A0%91%E7%9A%84%E5%87%BD%E6%95%B0%0A%20%20%20%20root%20%3D%20list_to_tree%28arr%3D%5B1,%202,%203,%204,%205,%206,%207%5D%29%0A%0A%20%20%20%20%23%20%E5%89%8D%E5%BA%8F%E9%81%8D%E5%8E%86%0A%20%20%20%20res%20%3D%20%5B%5D%0A%20%20%20%20pre_order%28root%29%0A%20%20%20%20print%28%22%5Cn%E5%89%8D%E5%BA%8F%E9%81%8D%E5%8E%86%E7%9A%84%E8%8A%82%E7%82%B9%E6%89%93%E5%8D%B0%E5%BA%8F%E5%88%97%20%3D%20%22,%20res%29%0A%0A%20%20%20%20%23%20%E4%B8%AD%E5%BA%8F%E9%81%8D%E5%8E%86%0A%20%20%20%20res.clear%28%29%0A%20%20%20%20in_order%28root%29%0A%20%20%20%20print%28%22%5Cn%E4%B8%AD%E5%BA%8F%E9%81%8D%E5%8E%86%E7%9A%84%E8%8A%82%E7%82%B9%E6%89%93%E5%8D%B0%E5%BA%8F%E5%88%97%20%3D%20%22,%20res%29%0A%0A%20%20%20%20%23%20%E5%90%8E%E5%BA%8F%E9%81%8D%E5%8E%86%0A%20%20%20%20res.clear%28%29%0A%20%20%20%20post_order%28root%29%0A%20%20%20%20print%28%22%5Cn%E5%90%8E%E5%BA%8F%E9%81%8D%E5%8E%86%E7%9A%84%E8%8A%82%E7%82%B9%E6%89%93%E5%8D%B0%E5%BA%8F%E5%88%97%20%3D%20%22,%20res%29&codeDivHeight=800&codeDivWidth=600&cumulative=false&curInstr=129&heapPrimitives=nevernest&origin=opt-frontend.js&py=311&rawInputLstJSON=%5B%5D&textReferences=false" target="_blank" rel="noopener noreferrer">Full Screen ></a></div>

!!! tip

    Depth-first search can also be implemented based on iteration, interested readers can study this on their own.

The Figure 7-11  shows the recursive process of preorder traversal of a binary tree, which can be divided into two opposite parts: "recursion" and "return".

1. "Recursion" means starting a new method, the program accesses the next node in this process.
2. "Return" means the function returns, indicating the current node has been fully accessed.

=== "<1>"
    ![The recursive process of preorder traversal](binary_tree_traversal.assets/preorder_step1.png){ class="animation-figure" }

=== "<2>"
    ![preorder_step2](binary_tree_traversal.assets/preorder_step2.png){ class="animation-figure" }

=== "<3>"
    ![preorder_step3](binary_tree_traversal.assets/preorder_step3.png){ class="animation-figure" }

=== "<4>"
    ![preorder_step4](binary_tree_traversal.assets/preorder_step4.png){ class="animation-figure" }

=== "<5>"
    ![preorder_step5](binary_tree_traversal.assets/preorder_step5.png){ class="animation-figure" }

=== "<6>"
    ![preorder_step6](binary_tree_traversal.assets/preorder_step6.png){ class="animation-figure" }

=== "<7>"
    ![preorder_step7](binary_tree_traversal.assets/preorder_step7.png){ class="animation-figure" }

=== "<8>"
    ![preorder_step8](binary_tree_traversal.assets/preorder_step8.png){ class="animation-figure" }

=== "<9>"
    ![preorder_step9](binary_tree_traversal.assets/preorder_step9.png){ class="animation-figure" }

=== "<10>"
    ![preorder_step10](binary_tree_traversal.assets/preorder_step10.png){ class="animation-figure" }

=== "<11>"
    ![preorder_step11](binary_tree_traversal.assets/preorder_step11.png){ class="animation-figure" }

<p align="center"> Figure 7-11 &nbsp; The recursive process of preorder traversal </p>

### 2. &nbsp; Complexity analysis

- **Time complexity is $O(n)$**: All nodes are visited once, using $O(n)$ time.
- **Space complexity is $O(n)$**: In the worst case, i.e., the tree degrades into a linked list, the recursion depth reaches $n$, the system occupies $O(n)$ stack frame space.