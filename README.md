#硬件api接口
##说明
####传输协议
采用 HTTP 标准的 POST 协议。
####数据格式
提交和返回数据都为 JSON 格式
####字符编码
统一采用 UTF-8 字符编码
####串口
波特率：115200
数据位：8
奇偶校验：无
停止位：1
数据流控：无

##固件
模块标准为esp8266 12E或者12F（Flash 32M）
<p align="center"><img src="http://wiki.aithinker.com/_media/esp8266/esp8266_module_list.png
"></p>

固件文件分别为0x00000.bin，0x10000.bin，0x80000-32mb.img

烧录位置<br>
0x00000.bin->0x00000<br>
0x10000.bin->0x10000<br>
0x80000-32mb.img->0x80000<br>

##设备心跳
####模块每5秒向mcu发送心跳
{"action":"ping","status":"1001"}
####status码
1001 设备没有联网<br>
1002 设备已联网<br>
1003 设备已经连接mqtt<br>

##设备联网
####mcu串口发送
{"action":"config","type":"0"}
####type类型
0  esptouch配网<br>
1  airkiss配网<br>
2  AP路由配网<br>

##查询产品信息
####模块向mcu发送
{"action":"product"}
####mcu串口回复
{"action":"product","id":"xxx","ver":"01"}
####说明
product_id和ver版本号有管理后台维护，mcu固件写入指定product_id和ver版本号

##获取系统时间
####mcu串口发送
{"action":"time"}
####模块回复
{"active":"time","data":"190224162357"}
####日期格式
年月日时分秒


##MQTT通讯
####mcu接收（data部分源协议）
{"action":"mqtt","data":"0x550000020000000"}
####mcu发送（源协议）
0x550000020000000


##升级检测
####mcu串口发送
{"action":"ckup"}
####模块回复
{"active":"ckup","data":"04"}
####data说明
00：不支持升级<br>
01：模块未就绪<br>
02：云端升级信息查询失败<br>
03：无需升级（云端无更新）<br>
04：需升级，等待发起升级操作<br>

##产测模式
####mcu串口发送
{"action":"test"}
####模块回复
{"active":"test"}
