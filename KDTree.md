# k维树

k维树是有序二叉树在N维空间的推广，有序二叉树存储的是一维元素。节点N的左子节点的所有元素总小于N，
右子节点的所有元素都大于N，建树和搜索的过程都是递归进行的。

##定义 
* $T_l$ 表示第$l$层子节点， 当前维度dim = l mod n
* $N_i$ 表示N节点第i维值  
* $N^L$ 表示N的左子节点，$N^R$ 表示N的右子节点。 
* Nearest 表示当前搜到的最近点, Min_Distance是搜到的最短距离。

##建树和搜索过程
按照同有序二叉树同样的方式，k维树的建立过程轮番在n维空间的各个维度进行。
$$T_l: N_{dim}^L < N_{dim} < N_{dim}^R $$ 
在每个维度，都从当前维度里选择中位数点作为N节点，把当前的所有节点一分为二。其实随机选一个点应该也可
以，尽量将当前维度均衡划分开。k维树的搜索过程同二叉树也很类似。$T_l$记录当前节点同目标节点的距离，
保留更优的结果（这里如果需要找到k个最近点，可以维护一个有限队列）。然后在左右子节点的当前维度中找离
目标节点更近的那一侧（当然是递归的使用k维树搜索算法），搜索进行到下$T_{l+1}$，一直进行到空叶子节点。
当算法开始回退的时候，**如果$abs(Nearest_{dim} - Target_{dim}) < Min_Distance$，那么我们需要搜索离
目标节点更远的那一侧节点。如果条件不成立，我们就直接向上回退就好。**这相当于在为搜索过程进行剪枝：
如果中间节点都不在Target节点圈定的超球体中， 那么更远侧的所有节点都不可能在其中。

具体的实现代码，可以参见`示例代码`。比较有趣的一点是，k维树可以应用在一种叫KNN的分类算法中，这种分类
算法思路很简单，就是规定一种距离的计算方式，在数据样本中找到同目标节点最近的k个节点，这些节点中属于
哪种节点更多，目标节点就属于那个类。


##代码示例

题目链接： http://acm.hdu.edu.cn/showproblem.php?pid=4347

```{.cpp .numberLines}
    #include <algorithm>
    #include <memory>
    #include <iostream>
    #include <cstring>
    #include <vector>
    #define square(x) (x)*(x)
    int n, dimensions;
    size_t k = 0;
    int target[6];
    int memory[60003][6]; //points value
    size_t data[60003];   //index to points
    int kdtree[200003];
    void init_tree() {
        memset(kdtree, 0xff, sizeof(kdtree));
    }
    void build_tree(int index, int d, int begin, int end) {
        if (begin >= end) return;
        int mid = (begin + end) / 2;
        std::nth_element(data + begin, data + mid, data + end, 
                         [d](int a, int b) { return memory[a][d] < memory[b][d]; });
        kdtree[index] = data[mid];
        int dim = (d + 1) % dimensions;
        build_tree(2 * index + 1, dim, begin, mid);
        build_tree(2 * index + 2, dim, mid + 1, end);
    }
    struct Distance {
        size_t index = 0;
        size_t dis = 0;
    };
    bool operator<(const Distance& dis1, const Distance& dis2) {
        return dis1.dis < dis2.dis;
    }
    size_t compute(int i1[], int i2[]) {
        size_t sum = 0;
        for (int d = 0; d < dimensions; d++) {
            sum += square(i1[d] - i2[d]);
        }
        return sum;
    }
    void output(Distance* closest_list, size_t size) {
        std::cout << "the closest " << size << " points are:" << std::endl;
        std::sort_heap(closest_list, closest_list + size);
        for (int i = 0; i != size; i++) {
            for (int j = 0; j < dimensions; j++) {
                std::cout << memory[closest_list[i].index][j];
                if (j != dimensions - 1) {
                    std::cout << " ";
                }
            }
            std::cout << std::endl;
        }
    }
    void search(int index, int d, Distance* closest_list, size_t* size) {
        if (kdtree[index] < 0) return;
        size_t dis = compute(target, memory[kdtree[index]]);
        closest_list[*size].index = kdtree[index];
        closest_list[*size].dis = dis;
        ++ (*size);
        std::push_heap(closest_list, closest_list+(*size));
        if (*size > k) {
            std::pop_heap(closest_list, closest_list+(*size));
            -- (*size);
        }
        int near_region_index = 0;
        int far_region_index = 0;
        if (memory[kdtree[index]][d] > target[d]) {
            near_region_index = index * 2 + 1;
            far_region_index = index * 2 + 2;
        } else {
            near_region_index = index * 2 + 2;
            far_region_index = index * 2 + 1;
        }
        search(near_region_index, (d+1) % dimensions, closest_list, size);
        //when the closest list is not full, max-dis may not be exact.
        if (*size < k || square(memory[kdtree[index]][d] - target[d]) < closest_list[0].dis) {
            search(far_region_index, (d+1) % dimensions, closest_list, size);
        } 
    }
    int main() {
        while(EOF != scanf("%d%d", &n, &dimensions)) {
        //read data
        for (size_t i = 0; i < n; i++) {
            for (size_t d = 0; d < dimensions; d++) {
                std::cin >> memory[i][d];
            }
            data[i] = i;
        }
        init_tree();
        build_tree(0, 0, 0, n);
        //read queries
        int query = 0;
        std::cin >> query;
        for (size_t i = 0; i < query; i++) {
            for (size_t d = 0; d < dimensions; d++) {
                std::cin >> target[d];
            }
            std::cin >> k; 
            Distance closest_list[20];
            size_t closest_list_size = 0;
            search(0, 0, closest_list, &closest_list_size);
            output(closest_list, closest_list_size);
        }
        }
        return 0;
    }
```


[^1]:《统计学习方法》李航 第三章 KNN分类
[^2]: << an Introductory tutorial on kd-trees>> Andrew W. Moore 



