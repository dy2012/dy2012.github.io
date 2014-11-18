---

layout: post

title:  Spark基础-Mesos框架

tags: [Spark学习]

---

&emsp;&emsp;在同一硬件环境下同时运行多个并行框架，不仅能节省搭建维护集群的成本，而且可以提高集群的使用率。多个框架同时运行产生的首要问题是计算资源的分配。集群的CPU和内存资源有限，只有在多个框架之间使用算法对资源进行统一的管理和分配，才能使所有的框架都正常运行，使资源得到最充分的利用。

&emsp;&emsp;第一代Spark是基于Mesos框架实现的，Mesos是AmpLab为了解决在同一硬件集群环境中同时运行多套不同的并行计算框架（包括MPI，MapReduce，Dryad以及Pregal等）而提出的一个方案。部署Spark和Mesos的优势包括：

* 动态划分Spark和其他的frameworks。

* 在多个不同的Spark实例中实现扩展。


![](http://dy2012.github.io/graphics/mesos.jpeg)












