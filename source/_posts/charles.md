---
title: Charles 安装
category: ubuntu
---

#### 1. 下载java-jre
   https://java.com/zh_CN/download/linux_manual.jsp（官网下载）
   http://pan.baidu.com/s/1o8evbJ0（网盘下载地址）
  （官网下载速度较慢）

#### 2. 将java-jre文件夹移动到一个目录下
   在之前，需要在/home下创建tools文件夹，并且修改分组和用户    
  `sudo mv jre-8u101-linux-x64.tar.gz /home/tools/`

#### 3. 解压&安装java-jre
  `tar -zxvf jre-8u101-linux-x64.tar.gz`

#### 4. 配置环境变量
  `sudo vim /etc/profile`

   在最下面添加：（下方首行路径为解压&安装路径）
    
    JAVA_HOME=/home/tools/jre1.8.0_101
    CLASSPATH=.:$JAVA_HOME/lib.tools.jar  
    PATH=$JAVA_HOME/bin:$PATH
    export JAVA_HOME CLASSPATH PATH

#### 5. 测试是否成功
  `source /etc/profile`    
   输入：   
  `java -version`    
   显示版本号则成功    
   到这里，java-jre安装成功。

#### 6. 下载 Charles：
   https://www.charlesproxy.com/latest-release/download.do
   (选择 **Linux**版本)

#### 7. 到下载目录，移动至自己的目录，并解压：

  `sudo mv charles-proxy-4.0.tar.gz /home/tools/`    
  `cd /home/tools/`    
  `tar -zxvf charles-proxy-4.0.tar.gz`

#### 8. 创建软连接
  `sudo ln -s /home/tools/charles/bin/charles /usr/local/bin/charles`

#### 9. 重启Ubuntu
  `reboot`

#### 10. 启动charles（端口：8888）
  `charles`
