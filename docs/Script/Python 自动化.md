# Python 自动化

## 批量创建文件夹

```python
import csv
import os

base_path = './1902/'  # 创建文件夹路径
i = 0

# 从 csv 中读取
csv_name = './1902.csv'
csv_reader = csv.reader(open(csv_name))

for line in csv_reader:
    folder_name = line[0] + "_" + line[1] + "_" + line[2] # we'b'h
    res_path = base_path + folder_name
    if not os.path.exists(res_path):
        os.mkdir(res_path)  # 创建文件夹，格式是路径+文件夹名称
```

