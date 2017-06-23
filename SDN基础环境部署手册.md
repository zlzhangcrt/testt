# 部署手册
## 一.安装ubuntu虚拟机
### 软件环境如下：
| 终端类别及用途|操作系统 | 相关应用软件 |
|--------|--------|
|   WEB服务器    |  Ubuntu 14.04.5 LTS    |Openvswitch 2.3.1 mininet
|      客户端  | Windows 10 	  |PuTTY 远程登录
### 硬件如下
| 终端类别及用途|机器配置 |IPv6地址|
|--------|--------|
|   WEB服务器    |  CPU： Intel(R) Xeon(R) CPU E5-2403 0 @ 1.80GHz  内存：4GB  硬盘：80GB|2001:da8:20d:21::131
|      客户端  |intel(R)_Core(TM)_i5-6200U_CPU_@_2.30GHz  内存：4GB  硬盘：250GB|2001:250:2800:20c3:a57f:8518:154c:81d9
## 二.安装java配置环境，需要需要Java7.0以上版本。
## 三.安装openvswitch 2.3.1
###1.安装好操作系统
```
lsb_release -a
```
###2.安装依赖包
```
apt-get install -y build-essential fakeroot debhelper \
                autoconf automake bzip2 libssl-dev \
                openssl graphviz python-all procps \
                python-qt4 python-zopeinterface \
                python-twisted-conch libtool
                ```
###3.下载openvswitch，并解压进入目录
```
wget http://openvswitch.org/releases/openvswitch-2.3.1.tar.gz
tar –zxvf  openvswitch-2.3.1.tar.gz
cd  openvswitch-2.3.1/
```
### 4.可以用# dpkg-checkbuilddeps检查下是否依赖包已经安装完毕
构建安装包
```
DEB_BUILD_OPTIONS='parallel=8 nocheck' fakeroot debian/rules binary
```
查看已经构建完成的包`ls`
### 5.安装openvswitch 2.3.1
```
dpkg -i openvswitch-common_2.3.1-1_amd64.deb  openvswitch-switch_2.3.1-1_amd64.deb
```
### 6.查看内核模块是 否加载
```
lsmod | grep openb
```
###	7.查看openvswitch版本
`ovs-vsctl -V`
### 8.查看OVS进程是否启动
```ps -ef | grep ovs | grep -v grep```
###9．查看 OVS 支持的 OpenFlow 协议的版本
`ovs-ofctl –version`
###10.openvswitch 启动
`service openvswitch-switch start`
##四.安装opendaylight
###	1.下载
`distribution-karaf-0.6.x-Carbon.zip`
###2.上传至服务器上
###3.解压
`unzip distribution-karaf-0.6.x-Carbon.zip`
###4．进入ODL目录
`cd bin`
`./karaf` #执行./karaf
### 5.出现上面界面完成安装
###	6．功能组件安装
```
opendaylight-user@root>feature:install odl-restconf
opendaylight-user@root>feature:install odl-l2switch-switch-ui
opendaylight-user@root>feature:install odl-openflowplugin-flow-services-ui
opendaylight-user@root>feature:install odl-mdsal-apidocs
opendaylight-user@root>feature:install odl-dlux-core
opendaylight-user@root>feature:install odl-dlux-node
opendaylight-user@root>feature:install odl-dlux-yangui
```
###7．登陆管理WEB UI
http://202.205.7.131:8181/index.html

提示：用户名和密码都是admin
