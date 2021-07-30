# 判断比较

* `!=`：不等于

## !=

Selenium的Chrome的driver中用xpath去查找元素，是可以通过：

```python
//a[@id="uhf-shopping-cart" and @aria-label!="0 items in shopping cart"]
```

实现判断，只匹配到

```python
id="uhf-shopping-cart" aria-label="2 items in shopping cart"
```

这类元素，而不匹配：

```python
id="uhf-shopping-cart" aria-label=“0 items in shopping cart"
```

即xpath支持：

```python
@someProperty!="some not expected text"
```

这种写法的
