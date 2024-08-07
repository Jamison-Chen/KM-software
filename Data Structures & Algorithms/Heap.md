# 定義

- Heap 是一種特殊的 tree，每個 node 最多只能有兩個 child nodes（heap 是一種 binary tree）
- 完全填滿一層後，才可以往下一層塞資料（heap 是一種 self-balanced tree）
- 最多只會有一個「只有一個 child node 的 internal node」，且該 node：
    - 必定是缺少 right child
    - 必定是同 level 中最右邊的 internal node
- 分為 **min heap** 與 **max heap**
    - Min heap 的每個 node 的值必定「小於等於」自己的兩個 child nodes 的值
    - Max heap 的每個 node 的值必定「大於等於」自己的兩個 child nodes 的值

# 建構 Heap 的方式

建構 heap 的方式分為 top-down 與 bottom-up 兩種，top-down 比較直覺（好實作），bottom-up 則比較有效率：

### Top-Down Construction

（假設要實作 max heap）從 root node 開始建立，當新建立的 node 有 parent 時，比較 parent 的值與新 node 的值，如果 parent 的值比較小，就將新 node 的值與 parent 的值對調；只要有對調，拿到新值的 parent node 就須要再與他的 parent 比較，一直比到沒有 swap 發生或抵達 root node 為止。

![](<https://raw.githubusercontent.com/Jamison-Chen/KM-software/master/img/heap-top-down-construction.png>)

Time complexity: $O(n \cdot \log n)$

### Bottom-Up Construction

（以 max heap 為例）由於 heap 的規則嚴謹，所以在給定元素個數時就可以知道 heap 的形狀了，因此可以先建立好一個所有 nodes 都沒有值的空 heap，並依下列規則填入值：

- 從「最底層最左邊」的 node 開始填入值
- 如果要填入值的 node 沒有 child node 則可直接繼續填下一個 node
- 若要填入值的 node 有 child node(s)，則先拿 child node(s) 中較大的值與剛填入的值比較，若剛填入的值較小，則將該值與 larger child 的值對調，反之則直接填入
- 若有因前向規則而發生對調，則拿到新值的 child node 要再與他的 larger child 比較，一直比到沒有對調發生或抵達 leaf node 為止

![](<https://raw.githubusercontent.com/Jamison-Chen/KM-software/master/img/heap-bottom-up-construction.png>)

Time complexity: $O(n)$

>[!Note]
>Time complexity 之所以是 $O(n)$ 不是 $O(n \cdot \log n)$，是因為整個 bottom-up construction 過程中，總對調次數不會超過 2n 次。

# Base

可以先實作 `Node` 資料結構，再將 nodes 串起來，也可以直接使用 array，以 max heap 為例：

![](<https://raw.githubusercontent.com/Jamison-Chen/KM-software/master/img/heap-tree-array.png>)

### Node-Based

每個 node 須要有 `value`、`parent`、`left_child`、`right_child`、`next` 五個 properties。

比起 node，array 輕量許多，所以簡單的 heap 通常不會用 node 實作。

# 實作

以 Python 實作：

- Bottom-up construction
- Array-based
- Pop method
- Push method

```Python
class MinHeap:
    def __init__(self, nums: list[int]) -> None:
        self.__h = self.__construct(list(nums))

    @property
    def size(self) -> int:
        return len(self.__h)

    def __construct(self, nums: list[int]) -> list[int]:
        """
        Using the bottom-up approach.
        """
        import math

        result: list = [None] * len(nums)
        depth = math.floor(math.log2(len(nums)))
        while nums:
            for idx in range(2**depth - 1, len(nums)):
                result[idx] = nums.pop()
                self.__downheap(result, idx)
            depth -= 1
        return result

    @staticmethod
    def __downheap(heap: list[int], idx: int) -> None:
        while (l := idx * 2 + 1) < len(heap):
            if (r := idx * 2 + 2) < len(heap):
                if heap[l] < heap[r] and heap[l] < heap[idx]:
                    heap[idx], heap[l] = heap[l], heap[idx]
                    idx = l
                elif heap[r] < heap[idx]:
                    heap[idx], heap[r] = heap[r], heap[idx]
                    idx = r
                else:
                    break
            elif heap[l] < heap[idx]:
                heap[idx], heap[l] = heap[l], heap[idx]
                idx = l
            else:
                break

    @staticmethod
    def __upheap(heap: list[int], idx: int) -> None:
        while idx > 0:
            parent_idx = (idx - (1 if idx % 2 else 2)) // 2
            if heap[idx] < heap[parent_idx]:
                heap[idx], heap[parent_idx] = heap[parent_idx], heap[idx]
                idx = parent_idx
            else:
                break

    def pop(self) -> int:
        if len(self.__h) == 1:
            return self.__h.pop()
        result = self.__h[0]
        self.__h[0] = self.__h.pop()
        self.__downheap(self.__h, 0)
        return result

    def push(self, num: int) -> None:
        self.__h.append(num)
        self.__upheap(self.__h, len(self.__h) - 1)
```

使用方法如下：

```Python
h = MinHeap([4, 1, 2, 5, 3, 6])
h.pop()  # 1
h.push(3)
```

>[!Note]
>其實 Python 有內建 [heapq](https://docs.python.org/3/library/heapq.html) library，不須要自己實作。

# 應用

### Priority Queue

Priority queue 的定義：「不論 enqueue 元素的順序為何，每次 dequeue 都會將 queue 中優先序最高的元素拿出」，heap 可以用 $O(\log n)$ 的時間複雜度做到 dequeue。

### Heap Sort

將所有元素放進 heap，然後再逐一 pop 出來。Heap sort 具有 $O(n \cdot \log n)$ 的時間複雜度，詳見 [Sorting Algorithms](</Data Structures & Algorithms/Sorting Algorithms.canvas>)。
