-  代數效應: 讓code可以跳過中間的狀態先處裡後面的工作，再回到前面處裡原本的階段。
## React Fiber
- Fiber並不是計算機術語中的新名詞，他的中文翻譯叫做纖程，與進程（Process）、線程（Thread）、協程（Coroutine）同為程序執行過程。

- 在很多文章中將纖程理解為協程的一種實現。在JS中，協程的實現便是Generator。

- 所以，我們可以將纖程(Fiber)、協程(Generator)理解為代數效應思想在JS中的體現。

- React Fiber可以理解為：
    React內部實現的一套狀態更新機制。支持任務不同優先級，可中斷與恢覆，並且恢覆後可以覆用之前的中間狀態。
- Fiber的含意
    - 作為架構來說，之前React15的Reconciler采用遞歸的方式執行，數據保存在遞歸調用棧中，所以被稱為stack Reconciler。React16的Reconciler基於Fiber節點實現，被稱為Fiber Reconciler。

    - 作為靜態的數據結構來說，每個Fiber節點對應一個React element，保存了該組件的類型（函數組件/類組件/原生組件...）、對應的DOM節點等信息。

    - 作為動態的工作單元來說，每個Fiber節點保存了本次更新中該組件改變的狀態、要執行的工作（需要被刪除/被插入頁面中/被更新...）。
```
function FiberNode(
  tag: WorkTag,
  pendingProps: mixed,
  key: null | string,
  mode: TypeOfMode,
) {
  // 作為靜態數據結構的屬性
  this.tag = tag;
  this.key = key;
  this.elementType = null;
  this.type = null;
  this.stateNode = null;

  // 用於連接其他Fiber節點形成Fiber樹
  this.return = null;
  this.child = null;
  this.sibling = null;
  this.index = 0;

  this.ref = null;

  // 作為動態的工作單元的屬性
  this.pendingProps = pendingProps;
  this.memoizedProps = null;
  this.updateQueue = null;
  this.memoizedState = null;
  this.dependencies = null;

  this.mode = mode;

  this.effectTag = NoEffect;
  this.nextEffect = null;

  this.firstEffect = null;
  this.lastEffect = null;

  // 調度優先級相關
  this.lanes = NoLanes;
  this.childLanes = NoLanes;

  // 指向該fiber在另一次更新時對應的fiber
  this.alternate = null;
}
```



- Reference
    - https://react.iamkasong.com/process/fiber.html#fiber%E7%9A%84%E7%BB%93%E6%9E%84

