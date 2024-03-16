---
id: maoyan
title: '🥪 采集猫眼电影榜'
---

这个示例演示用浏览器采集数据。

## ✅️️ 采集目标

目标网址：[https://www.maoyan.com/board/4](https://www.maoyan.com/board/4)

采集目标：排名、电影名称、演员、上映时间、分数

---

## ✅️️ 编码思路

按`F12`，可以看到每个电影信息都包含在`<dd>`元素中，因此可批量获取`<dd>`元素，遍历它们并再从其中获取每个电影的信息。

---

## ✅️️ 示例代码

以下代码可直接运行。

需要注意的是，这里用到记录器对象，详见[DataRecorder](https://g1879.gitee.io/datarecorderdocs/)。

```python
from DrissionPage import ChromiumPage
from DataRecorder import Recorder

# 创建页面对象
page = ChromiumPage()
# 创建记录器对象
recorder = Recorder('data.csv')
# 访问网页
page.get('https://www.maoyan.com/board/4')

while True:
    # 遍历页面上所有 dd 元素
    for mov in page.eles('t:dd'):
        # 获取需要的信息
        num = mov('t:i').text
        score = mov('.score').text
        title = mov('@data-act=boarditem-click').attr('title')
        star = mov('.star').text
        time = mov('.releasetime').text
        # 写入到记录器
        recorder.add_data((num, title, star, time, score))

    # 获取下一页按钮，有就点击
    btn = page('下一页', timeout=2)
    if btn:
        btn.click()
        page.wait.load_start()
    # 没有则退出程序
    else:
        break

recorder.record()
```

---

## ✅️️ 结果

程序生成一个结果文件 data.csv，内容如下：

```csv
1,我不是药神,"主演：徐峥,周一围,王传君",上映时间：2018-07-05,9.6
2,肖申克的救赎,"主演：蒂姆·罗宾斯,摩根·弗里曼,鲍勃·冈顿",上映时间：1994-09-10(加拿大),9.5
3,海上钢琴师,"主演：蒂姆·罗斯,比尔·努恩 ,克兰伦斯·威廉姆斯三世",上映时间：2019-11-15,9.3
4,绿皮书,"主演：维果·莫腾森,马赫沙拉·阿里,琳达·卡德里尼",上映时间：2019-03-01,9.5
5,霸王别姬,"主演：张国荣,张丰毅,巩俐",上映时间：1993-07-26,9.4

下面省略。。。
```
