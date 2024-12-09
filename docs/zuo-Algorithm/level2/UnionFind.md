# 岛问题和并查集

> 参考文章[Harry Blog]([My ultimate data structure and algorithm guide | Harry Blog](https://harryqu1229.github.io/2022/06/12/算法终极指南/#并查集))

## 岛问题

### 题目

​	一个矩阵中只有0和1两种值，每个位置都可以和自己的上、下、左、右 四个位置相连，如果有一片1连在一起，这个部分叫做一个岛，求一个矩阵中有多少个岛?

* 举例

001010

111010

100100

000000

这个矩阵中有三个岛

### 解法

* 岛的数据结构是一个二维数组，维度为M和N
* 我们遍历整个数组，如果当前值为1，就把当前位置传入到一个infect函数
* infect函数会把当前位置设置为2，并且递归访问当前位置的上下左右，然后返回
* 因此这个函数会把所有连通的岛都修改为2
* 此时我们让count++，表示找到一个岛
* 访问完当前位置后就继续遍历接下来的位置，直到找到当前位置为1的点
* 最终的count为岛的数量

```java
package 基础提升.class01;

/**
 * 该类用于计算二维矩阵中的岛屿数量。
 * 岛屿是由相邻的 1（陆地）组成的区域，相邻是指水平或垂直方向上的相邻。
 * 0 表示水域。
 */
public class Code03_Islands {

	/**
	 * 计算二维矩阵中的岛屿数量。
	 *
	 * @param m 二维矩阵，0 表示水域，1 表示陆地。
	 * @return 岛屿的数量。
	 */
	public static int countIslands(int[][] m) {
		if (m == null || m[0] == null) {
			return 0; // 如果输入矩阵为空，返回 0
		}
		int N = m.length; // 矩阵的行数
		int M = m[0].length; // 矩阵的列数
		int res = 0; // 用于记录岛屿的数量

		// 遍历整个矩阵
		for (int i = 0; i < N; i++) {
			for (int j = 0; j < M; j++) {
				if (m[i][j] == 1) { // 如果当前元素是陆地
					res++; // 发现一个新的岛屿
					infect(m, i, j, N, M); // 将当前岛屿的所有部分标记为已访问
				}
			}
		}
		return res; // 返回岛屿的数量
	}

	/**
	 * 使用深度优先搜索（DFS）将当前岛屿的所有部分标记为已访问。
	 *
	 * @param m 二维矩阵
	 * @param i 当前元素的行索引
	 * @param j 当前元素的列索引
	 * @param N 矩阵的行数
	 * @param M 矩阵的列数
	 */
	public static void infect(int[][] m, int i, int j, int N, int M) {
		// 边界条件检查
		if (i < 0 || i >= N || j < 0 || j >= M || m[i][j] != 1) {
			return; // 如果超出边界或当前元素不是陆地，返回
		}
		m[i][j] = 2; // 将当前元素标记为已访问（2 表示已访问）

		// 递归调用，处理四个方向的相邻元素
		infect(m, i + 1, j, N, M); // 下方
		infect(m, i - 1, j, N, M); // 上方
		infect(m, i, j + 1, N, M); // 右方
		infect(m, i, j - 1, N, M); // 左方
	}

	/**
	 * 主方法，用于测试计算岛屿数量的功能。
	 *
	 * @param args 命令行参数
	 */
	public static void main(String[] args) {
		int[][] m1 = {
				{ 0, 0, 0, 0, 0, 0, 0, 0, 0 },
				{ 0, 1, 1, 1, 0, 1, 1, 1, 0 },
				{ 0, 1, 1, 1, 0, 0, 0, 1, 0 },
				{ 0, 1, 1, 0, 0, 0, 0, 0, 0 },
				{ 0, 0, 0, 0, 0, 1, 1, 0, 0 },
				{ 0, 0, 0, 0, 1, 1, 1, 0, 0 },
				{ 0, 0, 0, 0, 0, 0, 0, 0, 0 },
		};
		System.out.println(countIslands(m1)); // 输出岛屿数量

		int[][] m2 = {
				{ 0, 0, 0, 0, 0, 0, 0, 0, 0 },
				{ 0, 1, 1, 1, 1, 1, 1, 1, 0 },
				{ 0, 1, 1, 1, 0, 0, 0, 1, 0 },
				{ 0, 1, 1, 0, 0, 0, 1, 1, 0 },
				{ 0, 0, 0, 0, 0, 1, 1, 0, 0 },
				{ 0, 0, 0, 0, 1, 1, 1, 0, 0 },
				{ 0, 0, 0, 0, 0, 0, 0, 0, 0 },
		};
		System.out.println(countIslands(m2)); // 输出岛屿数量
	}
}

```

> **这整个的时间复杂度是$O(N*M)$,N 代表 number of rows, M 代表 number of columns **
>
> 遍历整个二维数组会碰每一个元素一次
>
> 而infect过程中，所有的位置只会被他上下左右四个位置所访问，所以最多被访问四次
>
> 因此每一个点的最高访问次数为5，因此时间复杂度就是二维数组的规模$O(N*M)$

## 并查集

支持集合快速合并以及查找的结构

有两个操作：

1. 检查两个集合是否为同一个集合
2. 把两个集合变成一个集合

使用经典的数据结构无法在$O(1)$的时间复杂度内同时实现这两个操作。

**并查集可以在$O(1)$的时间复杂度内实现这两个操作**

并查集的重要思想在于，**用集合中的一个元素代表集合**。我曾看过一个有趣的比喻，把集合比喻成**帮派**，而代表元素则是**帮主**。接下来我们利用这个比喻，看看并查集是如何运作的。

![](/media/UnionFind-1.png)

最开始，所有大侠各自为战。他们各自的帮主自然就是自己。*（对于只有一个元素的集合，代表元素自然是唯一的那个元素）*

现在 1 号和 3 号比武，假设 1 号赢了（这里具体谁赢暂时不重要），那么 3 号就认 1 号作帮主 *（合并 1 号和 3 号所在的集合，1 号为代表元素）*。

![](/media/UnionFind-2.png)

现在 2 号想和 3 号比武 *（合并 3 号和 2 号所在的集合）*，但 3 号表示，别跟我打，让我帮主来收拾你*（合并代表元素）*。不妨设这次又是 1 号赢了，那么 2 号也认 1 号做帮主。

![](/media/UnionFind-3.jpg)

现在我们假设 4、5、6 号也进行了一番帮派合并，江湖局势变成下面这样：

![](/media/UnionFind-4.jpg)

现在假设 2 号想与 6 号比，跟刚刚说的一样，喊帮主 1 号和 4 号出来打一架（帮主真辛苦啊）。1 号胜利后，4 号认 1 号为帮主，当然他的手下也都是跟着投降了。

![](/media/UnionFind-5.png)

好了，比喻结束了。如果你有一点图论基础，相信你已经觉察到，这是一个**树**状的结构，要寻找集合的代表元素，只需要一层一层往上访问**父节点**（图中箭头所指的圆），直达树的**根节点**（图中橙色的圆）即可。根节点的父节点是它自己。我们可以直接把它画成一棵树：

![](/media/UnionFind-6.jpg)

### 路径压缩

最简单的并查集效率是比较低的。例如，来看下面这个场景：

![](/media/UnionFind-7.jpg)

现在我们要 merge (2,3)，于是从 2 找到 1，fa [1]=3，于是变成了这样：

![](/media/UnionFind-8.jpg)

然后我们又找来一个元素 4，并需要执行 merge (2,4)：

![](/media/UnionFind-9.png)

从 2 找到 1，再找到 3，然后 fa [3]=4，于是变成了这样：

大家应该有感觉了，这样可能会形成一条长长的**链**，随着链越来越长，我们想要从底部找到根节点会变得越来越难。

怎么解决呢？我们可以使用**路径压缩**的方法。既然我们只关心一个元素对应的**根节点**，那我们希望每个元素到根节点的路径尽可能短，最好只需要一步，像这样：

![](/media/UnionFind-10.png)

>  其实这说来也很好实现。只要我们在查询的过程中，**把沿途的每个节点的父节点都设为根节点**即可。***下一次再查询时，我们就可以省很多事***。

![](/media/UnionFind-code1.png)

这个就代表我们那个圈，就是不管什么类型进来我们就先让变成一个集合 (像是), 相当于给他包装一层就是这个 element 类

![](/media/UnionFind-code2.png)

> 并查集使用的前提就是初始化的时候把所有数据给我们了，这样我们才可以挨个包装成 Element 然后你接着可以做检查是不是同一集合，以及把两个不是同一个集合的合并成一个集合这种操作。注意这里面数据只是针对于你一开始初始化的，不能使用别的数据

![](/media/UnionFind-code3.png)

![](/media/UnionFind-code4.png)

![](/media/UnionFind-code5.png)

> 所以我们只需要调用并查集的构造函数把所有数据传进去
>
> **之后我们就可以对这些数据调用 isSameSet 和 Union 方法，然后时间复杂度很低 $O (1)$**
>
> 尽管这两个方法都调用了 findHead 方法， **其实只要方法被调用够多次数 (O (n) 次)(他内部那个扁平化优化), 其实调用他的时间复杂度是非常非常接近于 $O (1)$**—>(他的证明很难很难，花了 20 多年才证明出来)

```java
package 基础提升.class01;

import java.util.HashMap;
import java.util.List;
import java.util.Stack;

/**
 * 并查集（Union-Find Set）的实现。
 * 并查集是一种数据结构，用于处理一些不相交集合的合并及查询问题。
 * 主要支持两种操作：查找（find）和合并（union）。
 */
public class Code04_UnionFind {

	/**
	 * 元素类，用于存储集合中的元素。
	 *
	 * @param <V> 元素的类型
	 */
	public static class Element<V> {
		public V value;

		public Element(V value) {
			this.value = value;
		}
	}

	/**
	 * 并查集类，包含并查集的主要操作。
	 *
	 * @param <V> 元素的类型
	 */
	public static class UnionFindSet<V> {
		public HashMap<V, Element<V>> elementMap; // 存储值到元素的映射
		public HashMap<Element<V>, Element<V>> fatherMap; // 存储每个元素的父元素
		public HashMap<Element<V>, Integer> rankMap; // 存储每个元素的秩（树的高度）

		/**
		 * 构造函数，初始化并查集。
		 *
		 * @param list 初始元素列表
		 */
		public UnionFindSet(List<V> list) {
			elementMap = new HashMap<>();
			fatherMap = new HashMap<>();
			rankMap = new HashMap<>();
			for (V value : list) {
				Element<V> element = new Element<>(value);
				elementMap.put(value, element);
				fatherMap.put(element, element); // 每个元素的初始父元素是它自己
				rankMap.put(element, 1); // 每个元素的初始秩为1
			}
		}

		/**
		 * 查找元素的根节点，并进行路径压缩。
		 *
		 * @param element 要查找的元素
		 * @return 元素的根节点
		 */
		private Element<V> findHead(Element<V> element) {
			Stack<Element<V>> path = new Stack<>();
			while (element != fatherMap.get(element)) {
				path.push(element);
				element = fatherMap.get(element);
			}
			while (!path.isEmpty()) {
				fatherMap.put(path.pop(), element); // 路径压缩
			}
			return element;
		}

		/**
		 * 判断两个元素是否属于同一个集合。
		 *
		 * @param a 第一个元素
		 * @param b 第二个元素
		 * @return 如果两个元素属于同一个集合，返回 true；否则返回 false
		 */
		public boolean isSameSet(V a, V b) {
			if (elementMap.containsKey(a) && elementMap.containsKey(b)) {
				return findHead(elementMap.get(a)) == findHead(elementMap.get(b));
			}
			return false;
		}

		/**
		 * 合并两个元素所在的集合。
		 *
		 * @param a 第一个元素
		 * @param b 第二个元素
		 */
		public void union(V a, V b) {
			if (elementMap.containsKey(a) && elementMap.containsKey(b)) {
				Element<V> aF = findHead(elementMap.get(a));
				Element<V> bF = findHead(elementMap.get(b));
				if (aF != bF) {
					Element<V> big = rankMap.get(aF) >= rankMap.get(bF) ? aF : bF;
					Element<V> small = big == aF ? bF : aF;
					fatherMap.put(small, big); // 将秩较小的树的根节点指向秩较大的树的根节点
					rankMap.put(big, rankMap.get(aF) + rankMap.get(bF)); // 更新秩
					rankMap.remove(small); // 秩较小的树的根节点不再作为根节点
				}
			}
		}
	}
}

```



## 使用并查集解决岛问题

比如说岛问题给的二维数组特别特别大，那么我们之前那种方法只用一个 CPU 就会非常非常耗时间

首先，使用两个 CPU:

![img](/media/UnionFind-11.png)

其实我们整个来看就一个岛，但是

- 处理左边的 CPU 找到两个岛
- 处理右边的 CPU 也会找到两个岛

这是不对的，所以我们两个 CPU 需要想一个合并逻辑去求出一个正确的岛的数量

我们合并逻辑

- 首先记录我们从哪个点开始感染每一块岛
- 对于每个感染到的在边缘 (**分割的边缘**), 我们给他们做个记号 (记号就是我们开始感染的那个点)

比如说处理我们左边的 CPU 的数据

![img](/media/UnionFind-12.png)

右边同理:

![img](/media/UnionFind-13.png)

做合并:

一开始有多少 (从哪开始的) 感染点–> 四个，ABCD, 所以相当于传进去给并查集的构造函数形成四个集合

然后左边右边 CPU 分割算出 2 个岛，也就是一共 4 个岛

- **我们对于 (分割的) 边缘那块连在一起的集合 (如果他们不是同一个集合) 让他们连在一起**，然后让总共岛数 - 1

![](/media/UnionFind-14.png)

此时集合是 {A,C} {B}

- 接着看，此时 B 所在的岛和 C 所在的岛 **(他们代表的集合不是同一个，而且还在边缘除相连接，所以就合并！)** 合并在一起，总数 - 1

此时集合是 {A,C,B}

- 同理 B 和 D 代表的集合不是同一个，而且还在边缘除相连接，所以就合并，总数 - 1

此时集合是

- 然后 A 和 D 检查，现在是一同一个集合了！！！所以不用 - 1 (而且因为之后也没有其他集合要检查了，如果有的话就继续看然后合并等等等), 也就是现在岛数就是 1, 也就是正确答案

> 这样就做到了两个 CPU 分别处理一半，然后最后合并等等操作还是正确答案，当然比一个 CPU 处理整块快

多个 CPU:

![img](/media/UnionFind-15.png)

> **同理，分成好多块，然后让每一个 CPU 收集四边 (四边都要！) 的信息，然后就可以之后合并就跟四边都要合并一下**，最后合并成一大块，速度当然非常快