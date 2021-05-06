![在这里插入图片描述](https://pic.leetcode-cn.com/143b40666eebb8992b1ed7e6c35d4d5f3b93c6f20ab436e5c9ffa54032c392c0.png)




1. 新建临时节点，令该节点为 root；

2. 如果当前节点的左子节点为空，将当前节点加入答案，并遍历当前节点的右子节点；

3. 如果当前节点的左子节点不为空，在当前节点的左子树中找到当前节点在中序遍历下的前驱节点：
   1. 如果前驱节点的右子节点为空，将前驱节点的右子节点设置为当前节点。然后将当前节点加入答案，并将前驱节点的右子节点更新为当前节点。
   2. 如果前驱节点的右子节点为当前节点，将它的右子节点重新设为空。当前节点更新为当前节点的右子节点。

4. 重复步骤 2 和步骤 3，直到遍历结束。




- 

  - 指针cur: 指向当前遍历位置上的节点
  - 指针pre: 指向cur在中序遍历中的前驱节点

> Java代码实现 morris算法实现线序遍历

``` java
public class Solution {
    
  private List<Integer> res = new ArrayList<>();

  public void morris(TreeNode root) {
    TreeNode pre;
    TreeNode cur = root;
    while (cur != null) {
      if (cur.left == null) {
        res.add(cur.val);
        cur = cur.right;
      } else {
        pre = cur.left;
        // 寻找前驱节点
        while (pre.right != cur && pre.right != null) {
          pre = pre.right;
        }
        if (pre.right == null) {
          res.add(cur.val);
          pre.right = cur;
          cur = pre.right;
          cur = cur.left;
        } else {
          pre.right = null;
          cur = cur.right;
        }
      }
    }
  }    
}
```

