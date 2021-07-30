# 逻辑操作

Xpath中的逻辑操作，主要有：

* `or`：逻辑`或`
* `and`：逻辑`与`
* `not`：逻辑`非`

#### or 逻辑或

举例：

可以同时搜到 **class是b_algo** 或 **class值以b_ad开头的** li元素

```python
allLiXpath = "//li[@class='b_algo' or starts-with(@class, 'b_ad')]"
resultLiList = resultElem.find_elements_by_xpath(allLiXpath)
```

#### not 逻辑非

举例：

* `//input[@name="identity" and not (contains(@class,'A'))]`
* `//input[not(@class)]`
