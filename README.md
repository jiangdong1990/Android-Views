# 数据结构及算法
## Android常见数据结构&优缺点
### 数组
数组在内存中是一个连续的存储单元，我们在声明一个数组的时候必须声明其长度，这样就导致了我们在数组中插入或者删除一个元素的时候其他元素都要相应的向后移动或者向前移动，但是在知道查询时如果知道角标i则能够直接通过角标快速找到该元素时间复杂度为O(1) 如果不知道角标则时间复杂度为O(n)
### 堆栈
堆栈提供的是后进先出的存储方式
### 队列
队列提供的是先进先出的存储方式
### 链表
链表有别于数组，它是离散式存储方式，不需要一块连续的存储方式，每个数据之间通过指针链接，数据元素包括数据域和指针域，数据域存储数据，指针域指向下一个数据元素（针对单向链表）
双向链表包括数据域和前后指针，前后指针分别指向上一个数据元素和下一个数据元素
链表针对查询元素的话则需要循环遍历，时间复杂度为O(n)，插入和删除的则速度较快，因为只需要针对前后元素进行操作就行，不要前后移动其他元素，不要造成内存碎片化
简单总结起来就是：链表增删效率高，查找效率低。每一个数据项与数组相比更耗内存。不需要整块内存块，不会造成碎片化
引申：Linklist ArrayList Vector的区别
ArrayList和Vector是基于存储元素的数组来实现的，因此允许带角标查询，带角标的查询时间复杂度为O(1)。只是ArrayList是线程不安全而Vector是线程安全的，Vector多数方法是synchronize同步了的
LinkList是基于双向链表来实现的，因此它的增删效率快，查询效率要慢些
### 哈希表
哈希表其实就是以键值对key-value的方式进行存储的，只要有对应的key就能很快速的查找出对应元素  
哈希表能同时兼备数组和链表的优点，它能在插入和查找时都具备良好的性能。

## 算法
### 插入算法
 //插入算法
    private int[] insertSort(int[] args){
       if (args==null||args.length<2){
           return args;
       }
       for (int i = 1;i<args.length;i++){
           //将i号元素和前面的元素比较
           for (int j = i-1;j>=0&&args[j]>args[j+1];j--){
                int temp =args[j];
                args[j] = args[j+1];
                args[j+1] =temp;
           }
       }
       return args;
    }


    //折半插入算法
    private int[] halfInsertSort(int[] args){
        if (args==null||args.length<2){
            return args;
        }
        for (int i =1;i<args.length;i++){
            int temp = args[i];  //待插入元素
            
            //二分法  将0到i-1号元素进行二分比较
            int L = 0;
            int R = i-1;
            while (L<R){
                int mid = i+(i-1)/2;
                if (temp<args[mid]){  //继续二分 L到mid+1号元素
                    R = mid+1;
                }else {
                    L = mid-1;    //继续二分 mid-1到R号元素
                }
            }
            
            //找到元素该放的位置角标L后，将后面的元素依次移动位置
            for (int j =i ;j>L;j--){
                args[j]= args[j-1];
            }
            //将待插入元素放入角标L的位置
            args[L] = temp;
        }
        return  args;
    }
