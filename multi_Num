def multi_plus(n1, n2):  # 多项式加法
    return n1 ^ n2


def multi_multiplication(n1, n2):  # 多项式乘法
    temp = bin(n2)[2:]
    s = 0
    while len(temp) > 0:
        if int(temp[0]) > 0:
            s ^= n1 << len(temp) - 1
        temp = temp[1:]
    return s, multi_division(s, 283)[1]


def multi_division(n1, n2, q=0):  # 多项式除法运算
    if n1 < n2:
        return 0, n1
    elif n2 == 0:
        return 0
    else:
        delta = len(bin(n1)) - len(bin(n2))
        q += 1 << delta
        r = (n2 << delta) ^ n1
        if r >= n2:
            return multi_division(r, n2, q)
        else:
            return q, r


def multi_gcd(n1, n2):  # 多项式求最大公因式(欧几里得算法)
    if n1 == 0:
        return n2
    elif n2 == 0:
        return n1
    if n1 - n2 >= 0:
        n1 = multi_division(n1, n2)[1]
        return multi_gcd(n1, n2)
    else:  # s1比s2小，则将s1，s2互换，继续运算
        n1, n2 = n2, n1
        return multi_gcd(n1, n2)


def multi_niyuan(n1, n2, v1=1, v2=0, w1=0, w2=1):  # GF(2^8)域求乘法逆元，原理和整数的扩展欧几里得算法几乎一致，但是必须先定义多项式的模运算、加法运算和乘法运算
    s1, s2 = n1, n2
    if n2 == 0:
        return 0
    if multi_gcd(s1, s2) != 1:
        return "没有逆元"
    else:
        rx = multi_division(n1, n2)[1]  # multi_rx返回的是一个列表，装载着余数和商
        qx = multi_division(n1, n2)[0]
        n1, n2 = n2, rx
        v1, v2 = v2, multi_plus(v1, multi_multiplication(v2, qx)[1])
        w1, w2 = w2, multi_plus(w1, multi_multiplication(w2, qx)[1])
        if rx != 0:
            return multi_niyuan(n1, n2, v1, v2, w1, w2)
        else:
            return w1


def menu():
    n1 = int(input("请输入n1\n"))
    n2 = int(input("请输入n2\n"))
    choose = input("请选择功能：\n"
                   "1.ax+bx\n"
                   "2.ax·bx\n"
                   "3.ax/bx\n"
                   "4.求ax mod(bx)的逆元\n"
                   "5.gcd(ax,bx)\n")
    if choose == '1':
        print('和是：', multi_plus(n1, n2))
    elif choose == '2':
        print('GF(2)上乘积是：', multi_multiplication(n1, n2)[0], " GF(2^8)上乘积是：", multi_multiplication(n1, n2)[1])
    elif choose == '3':
        print('商是:', multi_division(n1, n2)[0], ' 余数是：', multi_division(n1, n2)[1])
    elif choose == '4':
        print('逆元是：', multi_niyuan(n1, n2))
    elif choose == '5':
        print('gcd是：', multi_gcd(n1, n2))
    else:
        print("输入有误，请重试！")


if __name__ == '__main__':
    while True:
        menu()
