# tiaFunction 
## 1. 4Byte2Str
## 2. 8Byte2Str
## 3. ISODate
## 4. PtpPolling
### 编辑环境
TIA v15.1 
#### 功能介绍
转换整数或实数为指定格式的字符串

4Byte2Str.scl 适用于S7-1200 v4.2 和 S7-1500 v2.6及以上系列PLC

8Byte2Str.scl 适用于S7-1500 v2.6 及以上系列PLC

ISODate.scl 利用4Byte2Str FC 将DTL格式时间转换为ISO格式时间字符串

#### 	参数描述：
 in：支持以下数据类型
 
| TYPE | 4Byte2Str |8Byte2Str  |
| --- | --- | --- |
| SINT | Y | Y |
| USINT | Y | Y |
| INT | Y | Y |
| UINT | Y | Y |
| DINT| Y |Y  |
| SDINT | Y | Y |
| LINT | N | Y |
| ULINT | N | Y |
| REAL | Y |Y  |
| LREAL |N  |Y  |
    
Format：格式['s'][width]['.'prec]
    s：带符号，大小写均可；
    width：整数部分长度
    prec：小数部分长度 

Error：1表示故障

返回值：转换后的字符串；Error=1时返回故障原因   

### 说明
in为负数时，转换字符串总是带'-'号                                                             
width小于实际整数长度时按实际整数长度转换字符串                                             
width大于实际整数长度时，左侧填'0'                                                          
prec=0时，不显示小数部分
prec > 0 时，小数部分采用四舍六入五取偶

	例如对下列数据保留3位有效数字：
	9.8249=9.82, 9.82671=9.83
	9.8350=9.84, 9.83501=9.84
	9.8250=9.82, 9.82501=9.83

4Byte2Str 如果数值大于 4.294968E+9 或小于 -4.294968E+9 ，返回字符串将按浮点格式显示输出。
8Byte2Str 如果数值大于 1.84467440737095E+19 或小于 -1.84467440737095E+19 ，返回字符串将按浮点格式显示输出。
### 示例
	in=15.2
	Format='',        4Byte2Str='15.2'
	Format='s3.5'，   4Byte2Str='+015.20000'
    
	in=-312
	Format='2.5',     4Byte2Str='-312.00000'
    
	in=2.991
	Format='',          4Byte2Str='1'
	Format='s2.3',      4Byte2Str='+02.991'
	
	in=4.294968E+09
	Format='',          4Byte2Str='4.294968E+9'
	Format='s2.3',      4Byte2Str='+4.294968E+9'

