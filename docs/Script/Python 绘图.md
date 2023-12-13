# Python 绘图

## 散点图

- python 3.9
- `pip install matplotlib numpy pandas`

```py
import matplotlib
import matplotlib.pyplot as plt
import numpy as np
import pandas as pd
import math

# df_log10 = pd.DataFrame({"4": [1, 2, 3], "8": [4, 5, 6], "16": [7, 8, 9]})
# sel_df = df_log10.loc[:, ["4", "8", "16"]]

# data:8/16/20/24
data = [
    [0.0034, 0.0094, 0.0248, 0.0417, 0.0633, 0.0772, 0.0745, 0.2725, 0.1852],
    [
        1.0013,
        0.3085,
        0.1992,
        0.0973,
        0.0868,
        0.0778,
        0.0855,
        0.1026,
        0.1395,
        0.1823,
        0.3132,
        0.3601,
        0.5106,
        0.6534,
        0.5629,
        2.9645,
        2.6379,
    ],
    [
        23.1435,
        6.3223,
        1.9782,
        0.8193,
        0.6535,
        0.2713,
        0.1770,
        0.1313,
        0.1279,
        0.1442,
        0.1523,
        0.2160,
        0.2530,
        0.4235,
        0.6378,
        0.8669,
        1.0260,
        1.3802,
        1.3010,
        5.9628,
        6.3742,
    ],
    [
        55.2993,
        78.4492,
        26.4270,
        14.9658,
        6.8339,
        3.6449,
        1.2573,
        0.7458,
        0.4680,
        0.2775,
        0.2233,
        0.2195,
        0.2060,
        0.2241,
        0.2602,
        0.3589,
        0.4181,
        0.8348,
        1.0976,
        1.7496,
        1.9596,
        2.7690,
        2.2817,
        12.6460,
        12.0313,
    ],
    [
        10262.8145,
        5484.4755,
        12108.9859,
        1849.0390,
        1477.4370,
        248.8621,
        153.3800,
        67.6714,
        20.8445,
        12.9813,
        2.1013,
        1.1904,
        1.5950,
        0.4915,
        0.8006,
        0.3887,
        0.3557,
        0.3300,
        0.2980,
        0.5263,
        0.6522,
        0.6062,
        1.9373,
        1.4232,
        2.6640,
        2.8987,
        6.9818,
        2.7981,
        6.4229,
        15.0862,
        28.0206,
    ],
]


for item in data:
    for i in range(0, len(item)):
        # data[i] = data[i] * 1000
        item[i] = math.log10(item[i])

# print(data)

df_log10 = pd.concat(
    [
        pd.DataFrame({"8": data[0]}),
        pd.DataFrame({"16": data[1]}),
        pd.DataFrame({"20": data[2]}),
        pd.DataFrame({"24": data[3]}),
        pd.DataFrame({"30": data[4]}),
    ],
    axis=1,
)
# df_log10 = pd.DataFrame({"8": data[0], "16": data[1]})
sel_df = df_log10.loc[:, ["8", "16", "20", "24", "30"]]

# plot scatter
cmap = matplotlib.colormaps.get_cmap("tab10")
colors = [cmap(i) for i in np.linspace(0, 1, 5)]

plt.scatter(x=sel_df.index, y=sel_df["8"], c=colors[0], label="N=8", s=40)
plt.scatter(x=sel_df.index, y=sel_df["16"], c=colors[1], label="N=16", s=40)
plt.scatter(x=sel_df.index, y=sel_df["20"], c=colors[2], label="N=20", s=40)
plt.scatter(x=sel_df.index, y=sel_df["24"], c=colors[3], label="N=24", s=40)
plt.scatter(x=sel_df.index, y=sel_df["30"], c=colors[4], label="N=30", s=40)
ax = plt.gca()

# # set marker
# markers = ['o', 's', 'D']
# for i, line in enumerate(ax.get_lines()):
#     line.set_marker(markers[i])
ax.set_xlabel("K steps with Las Vegas")
ax.set_ylabel("log10 of time (ms)")
ax.grid(linestyle="--", linewidth=0.5, color="gray", alpha=0.5)
ax.legend()
plt.savefig("algo2log10_4816.png", dpi=600, bbox_inches="tight")

```

