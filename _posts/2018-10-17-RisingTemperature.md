---
layout:     post
title:      Rising Temperature
subtitle:   DATE_ADD
date:       2018-10-07
author:     ACInfinity
header-img: img/post-bg-ios10.jpg
catalog: true
tags:
    - Leetcode
    - SQL
---
#Rising Temperature
Weather有Id, RecordDate, Temperature三列;
求所有比昨天气温高的记录的Id;
注意日期比较不能直接+ - 运算, 须用Date函数来计算,
如果直接+, 相当于将日期转成了数值进行运算，比如20180131 + 1 = 20180132， 显然0132这个日期是不存在的, 那么结果将会出错。
```sql
SELECT
	w1.Id AS Id
FROM
	Weather w1
JOIN Weather w2 ON w1.RecordDate = DATE_ADD(w2.RecordDate, INTERVAL 1 DAY)
WHERE
	w1.Temperature > w2.Temperature
```

```sql
SELECT
	w1.Id AS Id
FROM
	Weather w1
JOIN Weather w2 ON DATEDIFF(w1.RecordDate, w2.RecordDate) = 1
WHERE
	w1.Temperature > w2.Temperature
```