# Data Structure

## 1. Linked list 

크게는 singly Linked List, Doubly Linked List와 Circular Linked List가 있고, 

차이점은 single은 한방향으로만 다른 Node를 가리키고 Double은 양방향으로, Circular는 순환적으로

가리킨다. 이를 구현해 볼 때에는 Next를 고려해서 구현해야 한다.

![Linked List](https://eeenthusiast.com//wp-content/uploads/2017/05/link-listmycomputerscience.net_.png)

- 주목할 만한 점은 (JavaScript는 예외지만 다른 언어의 일반적인 Array라고 생각한다면) 

  Array에 메모리가 저장될 때에는 연속적으로 메모리 블럭이 생성되지만, Object에 메모리가 저장될 때에는 

  연속적이지 않고 dynamic하게 효율적으로 메모리가 저장된다는 점이다. 이 점을 고려하면서 Data Structure를 

  구현해야 할 것 같다.

- Complexity를 생각을 해보면,

  search 할 때는 한 방향으로 찾아봐야 하므로 O(n)이고, insert할 때는 특정 지점에 insert하고 방향만 연결해주면 

  되므로 O(1)이다. 또 delete할 때도 특정지점의 값만 빼고 연결해주면 되므로 O(1)이다.

## 2. Tree

 일반적인 Tree는 정렬된 상태가 아니지만 BST(Binary Search Tree)는 다르다.

BST는 기준이 되는 Node보다 크기가 크면 오른쪽 작으면 왼쪽에 배치한다. 또 BST의 경우 search할 때에 두가지 경우가

있는데 첫번째로는 Breadth First Search, 이 검색 방법은 같은 층에 있는 Node들에 대해 검색을 하고 그 밑에 층에 있는 

자식 Node들에 대해 검색을 하는 방법이다. 이와는 다르게 두번째 방법인 Depth First Search는 한 쪽 방향으로 간 후에 

그 방향의 자식 Node를 다 검색하고 없으면 옆으로 가는 아래쪽으로 먼저 검사를 하는 방법이다. 

![Breadth First Search, Depth First Search](http://mishadoff.com/images/dfs/binary_tree_search.png)

또 Tree의 시작 Node를 root, 자식이 없는 Node를 leaf라고 부르기도 한다.

![Tree](https://koenig-media.raywenderlich.com/uploads/2016/07/BinaryTree.png)

- Complexity는 search할 때의 값이 독특한데 BST를 기준으로 생각해보면 검색을 할때 숫자의 크기로 검색을 하다보면 찾을 수 있는 확률이 2배씩 늘어나기 때문에 O(log n)이다.  

## 3. Graph

Graph는 Linked List의 확장버전 같은 느낌인데, 이차원적인 형태로 Node가 연결되어 있는 Data Structure이다.

이때 Node가 서로를 가리키고 있는지 혹은 한 방향으로만 가리키고 있는지도 다른데, 가장 적절한 예로는 Facebook은

친구가 되면 양방향으로 가리키는 경우이지만 Twitter는 팔로우기능이므로 한 방향으로만 가리키는 경우이다.

또한 이외에도 쓰이는 경우는 지도에도 적용을 할 수가 있다.  두 Node를 놓고 이를 서로 연결하면 지도 상에서는 

이를 길로 표현할 수 있다. 또 서로를 이어주는 연결고리를 Edge라고 하는데 이에 대해 가중치를 적용하는 경우도 있다. 

이에 대한 예로는 지도에서 거리를 나타낼 수 있는 부분이 이 경우이다. 

![Graph Weighted Edges](http://somethingk.com/main/wp-content/uploads/2017/06/CPT-Graphs-directed-weighted-ex1.svg_.png)

