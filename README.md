0x01 介绍<br>
此项目主要完成数据包的嗅探。<br>
0x02 目的<br>
主要采取学和练的方式熟悉DPDK开发框架。<br>
0x03 编译<br>
（1）编译DPDK环境，利用脚本。<br>
（2）进入源码目录make。<br>
（3）运行：./dpdk_sniffer -l 0-1 -n 1 -- --rx "(1,0,0)" --flow "1"<br>
0x04 版本计划<br>
v1.0.0 主要单网卡、单队列、流管理。 每个版本会持续更新。<br>
  2017.11.27 使用struct rte_ring 将IO线程和流管理线程解耦。<br>
0x05 遇到的问题<br>
(1)编译程序没问题，运行时报内存ops没初始化。<br>
	原因：constructor在main函数运行，有些对应的静态库没连接进来。因为我的makefile没有按照DPDK编程手册的建议编写，<br>
	所以导致某些静态库没连接进来。<br>
(2)流表五元组做key存在将一条流分为了两个不同方向的流，因为五元组顺序不同。<br>