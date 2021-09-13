# i2cget-dump.sh
因为i2cdump总是报错 i2cdump: block read failed，但是i2cget正常，所以使用i2cget来实现i2cdump格式的输出
## 命令格式
i2cget-dump.sh i2c-id i2c-address

i2c-id 是i2c总线编号，i2c-address是i2c设备地址

例子:
```shell
i2cget-dump.sh 0 0x5b
```
# i2ctransfer-dump-96716F.sh
使用i2ctransfer命令获取96716K芯片的所有寄存器信息(96716K是16bit寄存器地址)，实现i2cdump格式的输出
## 命令格式
i2ctransfer-dump-96716F.sh i2c-id i2c-address

i2c-id 是i2c总线编号，i2c-address是i2c设备地址

例子:
```shell
i2ctransfer-dump-96716F.sh 0 0x5b
```

# 显示输出格式
## 8bit输出 i2cget-dump.sh
```shell
     0  1  2  3  4  5  6  7  8  9  a  b  c  d  e  f
00: 00 a0 00 00 00 00 00 ff 00 00 00 ff 00 00 00 6d
10: 00 00 00 00 00 00 00 00 83 01 00 00 00 00 00 00
20: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
30: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
40: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
50: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
60: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
70: 00 00 00 00 00 00 00 00 XX 00 00 00 00 00 00 00
80: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
90: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
a0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
b0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
c0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
d0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
e0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
f0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
```
## 16bit输出 i2ctransfer-dump-96716F.sh
```shell
       0  1  2  3  4  5  6  7  8  9  a  b  c  d  e  f
0000: 00 a0 00 00 00 00 00 ff 00 00 00 ff 00 00 00 6d
0010: 00 00 00 00 00 00 00 00 83 01 00 00 00 00 00 00
0020: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
0030: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
0040: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
0050: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
0060: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
0070: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
0080: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
0090: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00a0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00b0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00c0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00d0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00e0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
00f0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
01f0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
...
fff0: 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00 00
```
## 读取错误时，显示XX

# i2c-tools使用方法
i2c-tools是一系列的命令i2cdetect, i2cdump, i2cget, i2cset，用于调试i2c的工具。
## i2cdetect检测i2c总线
```shell
# i2cdetect -l
i2c-0   i2c             i2c.0                                   I2C adapter
i2c-1   i2c             i2c.1                                   I2C adapter
i2c-2   i2c             i2c.2                                   I2C adapter
i2c-3   i2c             i2c.3                                   I2C adapter
i2c-4   i2c             16340000.i2c                            I2C adapter
```
## i2cdetect检测挂载在i2c总线上设备
检测总线0上的设备
```shell
# i2cdetect -r -y 0
     0  1  2  3  4  5  6  7  8  9  a  b  c  d  e  f
00:          -- -- -- -- -- -- -- -- -- -- -- -- --
10: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
20: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
30: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
40: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
50: -- -- -- -- -- -- -- -- -- -- UU 5b -- -- -- --
60: -- -- -- -- -- -- -- -- -- -- -- -- -- -- -- --
```
## i2cdump查看器件所有寄存器的值
查看总线0，地址0x5b所有寄存器的值
```shell
i2cdump -f -y 0 0x5b
```
## i2cget 看单个寄存器的值
查看总线0，地址0x5b，寄存器0x10的值
```shell
i2cget -f -y 0 0x5b 0x10
```
## i2cset 设置寄存器的值
将总线0，地址0x5b，寄存器0x10的值设置为0xff
```shell
i2cset -f -y 0 0x5b 0x10 0xff 
```
## i2ctransfer
i2cdump、i2cget、i2cset只适用于读写8位的寄存器地址, 功能完全可由i2ctransfer代替。
对于16位地址的寄存器，或者更高位的，使用i2ctransfer命令。

### 读
```shell
i2ctransfer -f -y 4 w2@0x28 0x00 0x00 r4
```
4代表i2c地址总线id, w2代表写两个字节，这里的两个字节是i2c设备地址
0x28为I2C设备的地址, 0x00 0x00 为要读的寄存器地址, r4为连续读4Byte

### 写
```shell
i2ctransfer -f -y 4 w3@0x28 0x00 0x00 0xaa
```
4代表i2c地址总线id, w3代表写两个字节，其中前两个字节是i2c设备地址，最后一个字节是要写入的数据
0x28为I2C设备的地址, 0x00 0x00 为要写的寄存器地址

## i2ctransfer读写96716k
96716k是一款视频解码芯片，并输出mipi接口的视频信号。
为了为 ADAS 应用提供额外的功能安全性，MAX96716A/MAX96716K 支持向 I2C 事务添加循环冗余校验 (CRC)。 使能时，主控 uC 必须在每个数据字节后计算并发送一个 CRC 字节。
### 读
1. 单字节读取: CNT-MSB CNT-LSB Data CRC
2. 多字节读取: CNT-MSB CNT-LSB Data CRC Data CRC ... Data CRC
### 写
1. 单字节写: CNT-MSB CNT-LSB Data CRC
2. 多字节写: CNT-MSB CNT-LSB Data CRC Data CRC ... Data CRC

