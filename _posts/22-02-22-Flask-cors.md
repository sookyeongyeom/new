---
title: Flask CORS 설정
category: Flask
---

> Flask CORS 설정

직접 헤더에 추가해주는 방법도 있지만 간단히 사용할 수 있는 모듈이 있다.

- 모듈 설치

```bash
pip install flask_cors
```

- CORS 설정

```python
from flask_cors import CORS

app = Flask(__name__)
CORS(app)
```