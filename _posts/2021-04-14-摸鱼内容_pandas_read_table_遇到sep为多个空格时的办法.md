---
layout:     post
title:      pandas_read_table_遇到sep为多个空格时的办法
subtitle:   学习
date:       2021-04-14
author:     simplex
header-img: img/page_back.jpg
catalog: true
tags:
    - 日常 
    - 学习
---

# pandas_read_table_遇到sep为多个空格时的办法

\s+

```python
pd.read_csv(file_path+"0.xyz", skiprows=2, header=None, sep='\s+')
"""
doc原话，还是要多看DOC呀
Delimiter to use. If sep is None, the C engine cannot automatically detect the separator, but the Python parsing engine can, meaning the latter will be used and automatically detect the separator by Python’s builtin sniffer tool, csv.Sniffer. In addition, separators longer than 1 character and different from '\s+' will be interpreted as regular expressions and will also force the use of the Python parsing engine. Note that regex delimiters are prone to ignoring quoted data. Regex example: '\r\t'.
"""

```

