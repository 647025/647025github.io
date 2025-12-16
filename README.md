# parse_kaijiang.py
import re
import pandas as pd
from paddleocr import PaddleOCR

# 1. OCR 识别
ocr = PaddleOCR(use_angle_cls=True, lang='ch')   # 中文模型
img_path = 'kaijiang.jpg'
result = ocr.ocr(img_path, cls=True)

# 把识别到的文字拼成一整串
full_text = ''.join([line[1][0] for line in result[0]])

# 2. 正则提取 7 个开奖号码（2 位数字）
codes = re.findall(r'\b\d{2}\b', full_text)
codes = sorted(set(codes), key=lambda x: int(x))  # 去重 + 按大小排序

# 3. 提取 7 个生肖（汉字）
shengxiao_list = ['鼠','牛','虎','兔','龙','蛇','马','羊','猴','鸡','狗','猪']
pattern = '[' + ''.join(shengxiao_list) + ']'
animals = re.findall(pattern, full_text)
animals = sorted(set(animals), key=lambda x: shengxiao_list.index(x))

# 4. 整理成表格
df = pd.DataFrame({
    '序号': list(range(1, 8)),
    '开奖号码': codes,
    '生肖': animals
})

# 5. 保存结果
df.to_csv('result.csv', index=False, encoding='utf-8-sig')
print('已提取完成，结果写入 result.csv：')
print(df)

