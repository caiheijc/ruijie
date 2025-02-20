# 锐捷设备命令自学笔记
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
```
(config-if-接口)#switchport access vlan 100 //指接口的配置为access口，并且属于vlan100
```
**说明**
交换机如果没有配置，所有的端口默认都是access。如果端口被配置为trunk,需要改成access口的话，先需要在接口下使用switchpor mode access 命令切换成access,否则不生效。
查看配置`#show vlan`
```
(config-if-接口)#switchport mode trunk //将交换机端口配置为trunk口
```
查看配置`#show interfaces trunk`



