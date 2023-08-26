import pandas as pd
import matplotlib.pyplot as plt

# 将数据转化为DataFrame
data = {
    "类型": ["C2C", "USDT", "卡卡", "其它", "三方钱包", "数字人民币", "淘宝点卡", "云闪付", "支付宝"],
    "2023/8/1": [259600, 274518, 947597, 13650, 4674682, 117710, 11300, 37321, 3307066],
    "2023/8/2": [179700, 311833, 872335, 7500, 4075892, 89296, 27850, 32637, 3171985],
    # ... 添加其他日期的数据 ...
}

df = pd.DataFrame(data)

# 设置“类型”列为索引，方便后续分析
df.set_index("类型", inplace=True)

# 绘制折线图来展示不同类型在每天的交易额变化趋势
df.T.plot(kind="line", figsize=(12, 8))
plt.title("Daily Transaction Amount Trend")
plt.xlabel("Date")
plt.ylabel("Transaction Amount")
plt.legend(title="Type")
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()

# 计算每种类型的总交易额
df["总交易额"] = df.sum(axis=1)

# 找出每种类型的最大和最小交易额及对应日期
df["最大交易额日期"] = df.idxmax(axis=1)
df["最大交易额"] = df.max(axis=1)
df["最小交易额日期"] = df.idxmin(axis=1)
df["最小交易额"] = df.min(axis=1)

# 输出全面分析结果
print(df)

# 绘制柱状图来展示每种类型的总交易额
df["总交易额"].plot(kind="bar", figsize=(10, 6))
plt.title("Total Transaction Amount by Type")
plt.xlabel("Type")
plt.ylabel("Total Transaction Amount")
plt.xticks(rotation=45)
plt.tight_layout()
plt.show()
