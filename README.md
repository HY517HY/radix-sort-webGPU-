# 基数排序并行--->以webGPU为例
基数排序被称为最稳定的排序方法，且由于基于每次的每次迭代所以元素都会被遍历，因此基数排序非常适合做并行。
# 基数排序GPU的两大核心要点：  
1.GPU实现前缀和；  
2.计算基组偏移量实现索引分配。
# webGPU计算的基础知识
1.工作组（工作组id：workgroup_id）：一个工作组由workgroup_size（可指定）个线程（工作项）进行的。同一工作组的所有工作项可以访问共享内存var<workgroup>定义的遍历，且并行运行，可以利用workgroupBarrier()同步工作组中的工作项操作。  
2.工作项：具体全局唯一ID：global_invocation_id和某个工作组中的局部ID：local_invocation_id。  
GPU的运行机制是根绝GPU的线程数和workgroup_size来评估需要多少个工作组，但线程不够分配时只能串行执行。
