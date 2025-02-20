# 锐捷交换机命令自学笔记
## 进入全局命令
`
#configure terminal
`
## 在config(全局)模式下
### 进入接口 
`
(config)#interface interface-id
(config-if)#
`
### 例如： 批量化接口配置 vlan/其他接口
`
#interface range vlan 1-10  //一次对十个vlan端口进行配置
`
### 重置接口的命令
```
#default 接口名称 //可以重置接口
```
### 关闭/打开接口
```
(config-if-接口)#shutdown //关闭接口
(config-if-接口)#no shutown //打开接口,默认端口处于no shoutdown状态
```
### 接口速率配置
```
(config-if-接口)#speed 100 //接口速率设置为100M
(config-if-接口)#end
(config-if-接口)#duplex full //接口设置为全双工
(config-if-接口)#end

(config-if-接口)#flowcontrol off //关闭交换机流接口控配置
#show interfaces status
```
### 交换机光电口复用
```
(config-if-接口)#medium-type fiber //将电口转换为光口
(config-if-接口)#medium-type copper //将光口转换为电口
```
1. 可用`#show interface status` //查看是否修改成功
2. 可用`#show interfaces ` //端口名称 transceiver`查看光模块的信息

### 交换机access口和trunk口配置与裁剪
1. 对交换机access口配置
```
(config-if-接口)#switchport access vlan 100 //指接口的配置为access口，并且属于vlan100
```
**说明:**
交换机如果没有配置，所有的端口默认都是access。如果端口被配置为trunk,需要改成access口的话，先需要在接口下使用switchpor mode access 命令切换成access,否则不生效。
查看配置`#show vlan`

2. 对交换机trunk口配置
```
(config-if-接口)#switchport mode trunk //将交换机端口配置为trunk口
```
查看配置`#show interfaces trunk`

3. 对trunk口和vlan的裁剪(必配)

**对trunk口指定vlan允许通过,不允许其他vlan通过.**
比如,允许vlan5,vlan10,vlan20-30通过
```
(config-if-接口)#switchport mode trunk //配置为trunk口
(config-if-接口)#switchport mode allowed vlan remove 1-4,6-9,11-19,31-4094 //交换机默认允许所有的本地已创建vlan通过,因为只允许指定的vlan通过，所以把不需要通过的vlan给裁剪掉。
(config-if-接口)#switchport mode allowed vlan 5;10;20-30 //也可以直接指定vlan通过
```
### 三层接口配置(SVI或Switchport接口)
#### 配置SVI接口，并配置ip地址：
```
(config)#vlan 10 //在配置vlan接口时应要先再config模式下创建vlan再去vlan配置IP地址否则不会生效
(config-vlan)#exit 
(config)#interface vlan 10 //进入vlan10
(config-if-VLAN 1)#ip address 192.1.1 255.255.255.0 //配置ip
```
查看配置可以`#show ip int brief` 

#### 配置No Switchport接口,并配置IP地址：
```
(config)#int 接口
(config-if-接口)#no switchport //先将端口设置为三层口，配置IP地址之前必须要变为三层口，否则无法完成ip的配置
(config-if-接口)#ip add 192.168.16.1 255.255.255.0 //配置ip地址
```
### 端口保护
适用于同一台交换机下的用户，在同一个vlan内用的用户不能互相访问，使其完全隔离。
在所需要隔离的端口输入
```
(config-if-接口)#switchport protected //开启端口保护
(config-if-接口)#exit
(config)#protected-ports route-deny //全局开启隔离功能，让配置了端口保护的端口之间不能访问
```
查看端口后可以看见protected那一栏时enable的
端口之间是无法ping通的


