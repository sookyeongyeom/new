---
title: 타이핑 효과
category: Python
---

# 타이핑 효과

> 타이핑 효과

```python
from time import sleep
import sys

def typing(text):
    for letter in text:
        sleep(0.05) 
        sys.stdout.write(letter)
        sys.stdout.flush()
```