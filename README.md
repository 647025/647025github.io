       天天十点半开奖信息网站
# 六加一组合开奖代码生成器
# 用法：python 6+1_code.py 381752 龙

import sys

# 1. 尾数→波色/五行/阴阳 映射表
MAP = {
    '0': ('蓝','土','阴'),
    '1': ('红','水','阳'),
    '2': ('红','火','阳'),
    '3': ('蓝','木','阴'),
    '4': ('蓝','金','阴'),
    '5': ('绿','土','阳'),
    '6': ('绿','水','阴'),
    '7': ('红','火','阴'),
    '8': ('红','木','阳'),
    '9': ('蓝','金','阳'),
}

# 2. 12 生肖→序号
SX2NO = {s: f'{i:02d}' for i, s in enumerate(
        '鼠牛虎兔龙蛇马羊猴鸡狗猪', start=1)}

def make_code(num6: str, shengxiao: str) -> str:
    """
    返回格式：
    波色:蓝红...|五行:木木...|阴阳:阴阳...|生肖:05
    """
    num6 = num6.strip()
    if len(num6) != 6 or not num6.isdigit():
        raise ValueError('6 位基本号必须是 0-9 的数字')
    if shengxiao not in SX2NO:
        raise ValueError('生肖只能是：鼠牛虎兔龙蛇马羊猴鸡狗猪')

    colors, elements, yinyang = [], [], []
    for d in num6:
        c, e, y = MAP[d]
        colors.append(c)
        elements.append(e)
        yinyang.append(y)

    sx_no = SX2NO[shengxiao]
    return (f'波色:{"".join(colors)}|'
            f'五行:{"".join(elements)}|'
            f'阴阳:{"".join(yinyang)}|'
            f'生肖:{sx_no}')

# 3. 命令行入口
if __name__ == '__main__':
    if len(sys.argv) != 3:
        print('用法：python 6+1_code.py <6位基本号> <生肖>')
        sys.exit(1)
    print(make_code(sys.argv[1], sys.argv[2]))
