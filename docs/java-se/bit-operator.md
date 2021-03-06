## 位运算符

**1. 按位与运算符（&）**  
&的意思是参加运算的两个数据，按二进制位进行“与”运算
运算规则：只有两个数的二进制同时为1，结果才为1，否则为0。

“与运算”的特殊用途：
（1）清零。如果想将一个单元清零，即使其全部二进制位为0，只要与一个各位都为零的数值相与，结果为零。
（2）取一个数中指定位
方法：找一个数，对应X要取的位，该数的对应位为1，其余位为零，此数与X进行“与运算”可以得到X中的指定位。
例：设X=10101110，
    取X的低4位，用 X & 0000 1111 = 0000 1110 即可得到；
    还可用来取X的2、4、6位。

**2.按位或运算符（|）**  
参加运算的两个对象，按二进制位进行“或”运算。
运算规则：参加运算的两个数的二进制只要有一个为1，其值为1。

“或运算”特殊作用：
（1）常用来对一个数据的某些位置1。
方法：找到一个数，对应X要置1的位，该数的对应位为1，其余位为零。此数与X相或可使X中的某些位置1。
例：将X=10100000的低4位置1 ，用 X | 0000 1111 = 1010 1111即可得到。

**3.异或运算符（^）**  
^的意思是参加运算的两个数据，按二进制位进行“异或”运算
运算规则：参加运算的两个数的二进制，如果两个相应位为“异”（值不同），则该位结果为1，否则为0。  

“异或运算”的特殊作用：
（1）使特定位翻转 找一个数，对应X要翻转的各位，该数的对应位为1，其余位为零，此数与X对应位异或即可。
例：X=10101110，使X低4位翻转，用X ^ 0000 1111 = 1010 0001即可得到。
（2）与0相异或，保留原值 ，X ^ 0000 0000 = 1010 1110。

