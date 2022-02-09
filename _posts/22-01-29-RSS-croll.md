---
title: RSS 크롤링
category: Python
---

# RSS 크롤링

> RSS 크롤링

```python
import feedparser

url = "http://bepolar.tistory.com/rss"

d = feedparser.parse(url)
print(d.feed['title'])
for e in d.entries:
    print("Title : " + e.title)
    print("Link : " + e.link)
    print("Description : " + e.description)
    print("Published : " + str(e.published))
```