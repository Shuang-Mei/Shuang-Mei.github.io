---
layout: post
title: "---Ubuntu 14.04下配置caffe---"
description: "在一台没有安装任何软件的机器上重新搭建caffe的环境，具体过程参见本文。"
category: 'configure'
---

**1.从github上下载源码**

	git clone https://github.com/BVLC/caffe.git

**2.安装BLAS库**

<font size="3">	选择安装mkl，在官网上下载学生版，解压到存放目录。先对解压后的文件授权</font>

	chmod a+x parallel_studio_xe_2015 -R

<font size="3">然后用root权限执行</font>

	sudo ./install.sh（一般都选择默认的选项）
	sudo vim /etc/ld.so.conf.d/intel_mkl.conf

<font size="3">配置环境，加入下面内容</font>

	/opt/intel/lib/intel64
	/opt/intel/mkl/lib/intel64

**3.安装python依赖包**

<font size="3">先安装python-pip</font>

	sudo apt-get install python-pip

<font size="3">然后进入caffe下的python文件夹，执行</font>

	for req in $(cat requirements.txt); do pip install $req; done

**4.安装cmake**

	sudo add-apt-repository ppa:george-edison55/cmake-3.x
	sudo apt-get update
	sudo apt-get install cmake

**5.安装glog**

<font size="3">https://github.com/google/glog.git(这个地址的安装包会报错，下载</font><font size="3" color="#FA8072">0.3.3</font><font size="3">的)</font>

<font size="3">进入文件夹，执行</font>

	sudo ./configure
	sudo make 
	sudo make install

**6.可以用apt-get安装的**

<font size="3">sudo apt-get install libboost-all-dev libprotobuf-dev libsnappy-dev libleveldb-dev libhdf5-serial-dev libgflags-dev libgoogle-glog-dev liblmdb-dev protobuf-compiler libopencv-dev</font>

**7.安装cudnn**

<font size="3">从官网上下载，然后解压</font>

	sudo cp cudnn.h /usr/local/include
	sudo cp libcudnn.* /usr/local/lib

<font size="3">复制过去之后，软连接就不见了，要自己再链接一次</font>

	sudo ln -sf libcudnn.so.7.0.64 libcudnn.so.7.0
	sudo ln -sf libcudnn.so.7.0 libcudnn.so
	sudo ldconfig 

**8.安装caffe**

<font size="3">执行cp Makefile.config.example Makefile.config，修改部分内容</font>

	BLAS := mkl
	USE_CUDNN := 1前面注释去掉
	DEBUG := 1 //便于后面调试

<font size="3">编译</font>

	make all -j8
	make test -j8
	make runtest -j8

错误：

1./bin/bash: aclocal-1.14: command not found

	sudo apt-get install autotools-dev
	sudo apt-get install automake

2.src/demangle.h:80:27: error: expected initializer before 'Demangle'.换成版本0.3.3就好了

3./sbin/ldconfig.real: /usr/local/lib/libcudnn.so.7.0 is not a symbolic link.重新建立软链接
