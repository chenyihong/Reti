# Reti

---check bit---

正常的传输(数据包为正确的)     A为发送方     B为接收方
```
	A				B
[01101001]		→		[01101001]

	A		←ACK		B

[01101001]	← 	1的数量为双数,那么结尾添加0 	成为[01101001]0
```
1.此方法仅可得知是否存在错误的bit,但不能纠正错误
2.如果有两个bit错误
3.如果数据包包含错误,则丢弃此数据包,请求重新发送数据包
4.如果数据包的错误数量过多,可能会被当成正确的数据包从而接收此数据包

```
Ppe = probabilita di pacchetto errato
Ppg = probabilita di pacchetto giusto = (1-Ppe)^n
```

0110101000011001	
两个1则为0，一个1则为1
```        
	   n
	0 1 1 0		0
n	1 0 1 0		0
	0 0 0 1		1
	1 0 0 1		0

	0 1 0 0
```
	2n/n^2 = 2/n lim(n→∞) → 0

0110101000011001 →	0110101000011001 0100 0010

此方法可以用于找出错误的bit,并且纠正错误的bit

```
	   n
            +-+
	0 1 |1| 0		0
n	1 0 |1| 0		0
       +----+-+--+			
       |0 0 |X| 1|		1
       +----+-+--+
	1 0 |0| 1		0
	    +-+

	0 1  0  0
```
X 处为错误的bit:	如果X的bit为0则为正确
		    如果X的bit为1则为错误,则接收方会利用多出的bit[0100 0010]纠正错别的bit


```
XOR(异或表)
A	B	|	XOR
----------------+-----------
0	0	|	0
0	1	|	1
1	0	|	1
1	1	|	0
```
例子:

```

	0 1 1 0		|	0
	1 0 1 0		|	0
	0 0 0 1		|	1
	1 0 0 1		|	0
------------------------+------------
	0 1 0 0		|

```

如果有3个错误的bit:

```
	0 1 1 0		|	0
	1 X O 0		|	0
	0 X X 1		|	1
	1 0 0 1		|	0
------------------------+------------
	0 1 0 0		|
```

改变正确的O即可纠正错误的X数据	→	将O处的1改成0即可纠正其他三个错误的bit

```
如果接受到包含错误的数据包(两种处理方式):
	1.重新请求发生数据包
	2.利用bit di parita / CRC 纠正错误的bit字节
```
