## 关于树的一些说明

前序遍历二叉树 == 深度优先遍历（DFS）

中序遍历二叉树（按层遍历二叉树） == 广度优先遍历（BFS）

[数据结构中各种树](http://www.cnblogs.com/maybe2030/p/4732377.html#_label1)

## 二叉查找树(BSTree.h)

### 定义

又称为是二叉排序树（Binary Sort Tree）或二叉搜索树。二叉排序树或者是一棵空树，或者是具有下列性质的二叉树：

1. 若左子树不空，则左子树上所有结点的值均小于它的根结点的值；
2. 若右子树不空，则右子树上所有结点的值均大于或等于它的根结点的值；
3. 左、右子树也分别为二叉排序树；
4. 没有键值相等的节点。

### 性质

对二叉查找树进行中序遍历，即可得到有序的数列。
　　
### 时间复杂度

它和二分查找一样，插入和查找的时间复杂度均为O(logn)，但是在最坏的情况下仍然会有O(n)的时间复杂度。原因在于插入和删除元素的时候，树没有保持平衡。我们希望在最坏的情况下仍然有较好的时间复杂度，这就是平衡查找树设计的初衷。二叉查找树的高度决定了二叉查找树的查找效率。

### 插入：

1. 若当前的二叉查找树为空，则插入的元素为根节点;

2. 若插入的元素值小于根节点值，则将元素插入到左子树中;

3. 若插入的元素值不小于根节点值，则将元素插入到右子树中。

### 删除：

将待删除节点命名为z

1. 如果z为叶子节点(没有左子树和没有右子树)，那么就可以直接删除该节点再修改其父节点的指针

2. 如果z为单支节点(只有左子树或者只有右子树), 那么就让z的子树连接z的父节点,再删除z

3. 如果z左右子树均不为空。找到z的后继y(y一定没有左子树),所以可以删除y, 让y的父节点成为y的右子树的父节点，用y代替z

### 前驱与后继

先找到键值相同的节点

#### 前驱：

1. 如果键值最小，则没有前驱

2. 如果该节点有左孩子，则前驱为“以当前节点的左孩子为根的子树的最大节点”。应该是该节点的左孩子的右孩子（如果有的话，否则为根节点）

3. 如果该节点没有左孩子

    1. 如果该节点是一个右孩子，则前驱就为它的父节点

    2. 如果该节点是一个左孩子，则前驱为它父节点的父节点第一个拥有右孩子的节点（需要不断遍历）

#### 后继：

1. 如果键值最大，则没有后继

2. 如果该节点有右孩子，则后继为右孩子中的最小节点

3. 如果该节点没有右孩子

    1. 如果该节点是一个左孩子，则后继就为它的父节点
    
    2. 如果该节点是一个右孩子，则后继为它父节点的父节点第一个拥有左孩子的节点
	        
## 平衡二叉树（AVL）

### 定义

​父节点的左子树和右子树的高度之差不能大于1，也就是说不能高过1层，否则该树就失衡了，此时就要旋转节点，在编码时，我们可以记录当前节点的高度，比如空节点是-1，叶子节点是0，非叶子节点的height往根节点递增。

### 插入

每次插入后需要平衡二叉树

1. 如果插入的数小于当前节点，遍历左边

    1. 如果当前节点的左节点为NULL，则插入到当前节点的左节点中

        2. 如果当前节点的左节点不为NULL，则继续遍历当前节点的左节点

2. 如果插入的数大于当前节点，遍历右边

    1. 如果当前节点的右节点为NULL，则插入到当前节点的右节点中

    2. 如果当前节点的右节点不为NULL，则继续遍历当前节点的右节点

    3. 如果插入的数等于当前节点，则不插入

### 删除

每次删除后需要平衡二叉树

先找到需要删除的节点

1. 需要删除的数大于当前节点，继续遍历左边

2. 需要删除的数小于当前节点，继续遍历右边

3. 需要删除的数等于当前节点，进行删除

删除节点

1. 删除节点有左右子树

    1. 找出左子树中最大的节点，代替删除节点（交换key值）

        1. 如果删除节点的左节点没有右节点，则最大节点就是左子树的根节点。将最大节点（待删除节点的左节点），衔接到当前待删除的节点

	2. 如果删除节点的左节点有右节点，则一直向右节点搜索，直到没有右节点为止（即找到了最大节点的值）。判断最大节点是父节点的左节点还是右节点。

            1. 如果是右节点，就将最大节点的子树接到最大节点的父节点上
            
	    2. 如果是左节点，就说明它已经是叶子节点了，就将这个节点赋值为NULL

2. 删除节点有左子树

    1. 删除节点的左子树的左节点如果存在，就将该节点赋值为待删除节点

    2. 删除节点的左子树的右节点如果存在，就将该节点复制为待删除节点

3. 删除节点有右子树

    同步骤2

4. 删除节点没有子树

    判断删除节点是父节点的左节点还是右节点，直接删除即可
