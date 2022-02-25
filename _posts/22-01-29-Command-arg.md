---
title: 명령행 인수 받기
category: [Study, Python]
---

# 명령행 인수 받기

> 명령행 옵션으로 인수 받기

```python
import argparse

parser = argparse.ArgumentParser()
parser.add_argument('-n', type=str, help="name")
args = parser.parse_args()
name = args.n
```

<br>

> 명령행 옵션 없이 인수 받기

```python
import sys

args = sys.argv[1:]
```