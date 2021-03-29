# proj28-3RMM

## 3RMM
A Reliable, Robust, Real-time Memory Manager

### 【项目描述】
在工业控制、航天航空等严苛的应用环境中，计算机硬件通常会受到高低温、潮湿、电磁辐射、宇宙射线等恶劣因素的影响。为了实现高可靠的计算机系统，传统上多采用硬件的升级改造，或者定制操作系统/内核，其成本异常昂贵。

内存在计算机系统中的重要性仅次于CPU，在恶劣环境下会出现单粒子翻转等问题，进而导致程序或系统崩溃。如果能通过软件的解决方案，实现一个针对严苛场景下的内存管理器，有助于节省硬件成本。

3RMM项目的目标是，实现一个可靠的、健壮的、实时的内存管理器，在Linux系统下以一个库的形式对外发布，运行在用户态。建议使用C语言开发，以便将来更易于移植到Linux内核或别的操作系统中。

- Reliable 可靠  
实现基本的内存管理功能，包括内存池等，在重负载、高并发、长期运行的情况，系统都能正常使用。

- Robust 健壮  
在内存出现单粒子翻转等异常情况下，依然能够正常运行。

- Real-time 实时  
使用高效的内存分配算法以及其他技术手段，加快内存分配和读写的速度。


### 【所属赛道】
2021全国大学生操作系统比赛的“OS功能设计”赛道

### 【参赛要求】
- 以小组为单位参赛，最多三人一个小组，且小组成员是来自同一所高校的本科生（2021年春季学期或之后本科毕业的大一~大四的学生）
- 如学生参加了多个项目，参赛学生选择一个自己参加的项目参与评奖
- 请遵循“2021全国大学生操作系统比赛”的章程和技术方案要求

### 【项目导师】
刘志立
- github https://github.com/liuzhili-ya
- email zhili.liu@ucas.com.cn

### 【难度】
中等

### 【特征】
- 具备内存分配器的常用功能，包括但不限于：分配、释放、扩充等
- 支持多线程和并发
- 支持内存池的功能
- 抗单粒子翻转，即1个bit出现错误的情况，系统还能够正常工作
- 支持Linux 4.4以上的系统

### 【License】
MIT license (LICENSE-MIT or http://opensource.org/licenses/MIT)  

## 【预期目标】
### 第一题：简单的内存分配器
- 实现一个内存分配器（allocator），并具备基本的功能;
- 支持的接口至少包括malloc、calloc、realloc、free;
- 具体实现可参考glibc/Ptmalloc2、[_mimalloc_](https://github.com/microsoft/mimalloc) 、[_tcmalloc_](https://github.com/gperftools/gperftools)、[_jemalloc_](https://github.com/jemalloc/jemalloc)。

### 第二题：支持多线程的高效内存分配器
- 在第一题的基础上，支持多线程和并发 （利用锁机制保护相关操作的临界区）;
- 通过benchmark测试，benchmark的参考实现为[_mimalloc-bench_](https://github.com/daanx/mimalloc-bench);
- 根据benchmark测试的性能数据，以及测试中占用的物理内存，综合评估方案，目标平台x86_64。

### 第三题：支持内存池的内存分配器
- 内存池是一个块预分配的内存区域，基于内存池的内存分配和释放都在内存池中完成;
- 支持基于处理器核心亲和度的内存池管理（以提高访存性能）;
- 支持的接口至少包括pool_create、pool_clear、pool_destroy、palloc、pcalloc;
- 参考实现为[_apr_pool_](https://github.com/apache/apr)，以及Linux的NUMA机制。

### 第四题：高可靠的内存管理器
- 在第一题的基础上，实现一个高可靠的内存管理器;
- 可以采用校验、备份、三模冗余、纠删码等各种方式，实现抗单粒子翻转的功能;
- 已分配内存的1个bit值出现错误的情况，依然能够读取正确的值;
- 对有异常的内存，能够自动修复;
- 上述处理层的加入，内存无法直接读取，需要内存的读写接口，实现内存在读写中数据的自动冗余备份、校验和纠错写;
- 本题测试方法：程序运行过程中，外部检测框架修改特定内存来模拟异常，程序内存不会出现读写错误。

### 第五题：3R的内存管理器
- 在第四题的基础上，进一步提高性能和实时性，兼顾3R (Reliable 可靠，Robust 健壮，Real-time 实时）;
- 使用benchmark进行测试，根据性能数据以及测试中占用的物理内存综合评估方案，目标平台为x86_64。
