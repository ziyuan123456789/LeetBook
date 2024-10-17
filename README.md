# 自用刷题笔记
## 自述:
垃圾学习垃圾专业垃圾就业形势,不刷点题不行

## 贪心
局部最优解我觉得就是整体最优解,前一阵看有个什么贝叶斯思维,觉得跟这个很像
### 445:分发饼干
题目描述:
假设你是一位很棒的家长，想要给你的孩子们一些小饼干。但是，每个孩子最多只能给一块饼干。
对每个孩子 i，都有一个胃口值 g[i]，这是能让孩子们满足胃口的饼干的最小尺寸；并且每块饼干 j，都有一个尺寸 s[j] 。如果 s[j] >= g[i]，我们可以将这个饼干 j 分配给孩子 i ，这个孩子会得到满足。你的目标是满足尽可能多的孩子，并输出这个最大数值。
我的思路:
我们把数组进行排列,小的在前大的在后,因为饼干总数量有限,所以我们以饼干数组为for循环基准点
无非只有三种情况,饼干正好为孩子胃口,饼干大于孩子胃口,饼干小于孩子胃口
1. 饼干正好为孩子胃口:这种情况是最好的,根本没浪费,因为我们采用饼干数组当作for循环基点所以我们需要让孩子数组步进一位,累加值+1
2. 饼干大于孩子胃口:可以喂饱这个孩子,孩子数组步进一位,累加值+1,因为你的目标是小饼干喂饱小胃口 所以不需要做后续处理了
3. 饼干小于孩子胃口:那么意味着你无法喂饱这个孩子 你只能寄托下一个饼干
```java
public int findContentChildren(int[] g, int[] s) {
    Arrays.sort(g);
    Arrays.sort(s);
    int start = 0;
    int count = 0;
    for(int i=0;i<s.length && start < g.length;i++){
        if(s[i]==g[start]){
            count++;
        }
        if(s[i] > g[start]){
            count++;
        }
        if(!(s[i] < g[start])){
            start++;
        }

    }
    return count;
}
```

## 二叉树
### 226. 翻转二叉树
递归处理只需要处理好一个节点就可以自动应用到整棵树上,后续遍历可以拿到之前的数据因此功能应该是最强大的,所以默认就选择了后续遍历
但是想想前序也是可以的
```java
public TreeNode invertTree(TreeNode root) {
    fx(root);
    return root;

}

public void fx(TreeNode root) {
    if (root == null) {
        return;
    }
    fx(root.left);
    fx(root.right);
    TreeNode temp = root.left;
    root.left = root.right;
    root.right = temp;
}
```
