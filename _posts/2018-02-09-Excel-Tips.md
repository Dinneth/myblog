---
layout: post
title: Excel技巧
tags:
  - learning
  - PC
  - Excel
---

总结一下自己常用的Excel技巧：

## 文本处理

### 清理不可见字符

` =TRIM(CLEAN(SUBSTITUTE(E2,"CHR(160)","")))
`

其中的**CHR(160)**可以是任何奇怪的字符，从源字符串中copy-paste即可