# 常见函数

* `start-with()`：以某值开头的
* `text()`：文本值
* `last()`：最后一个
* `concat()`：拼接多个内容

下面详细介绍：

## `start-with`

举例：

html：

```html
<li class="b_ad">
    xxx
</li>

<li class="b_ad b_adBottom">
    yyy
</li>

<li class="b_algo">
    aaa
</li>

<li class="b_algo">
    bbb
</li>
```

希望同时找到class是

* 普通元素的：`b_algo`
* 广告Ad元素的：以`b_ad`开始的

代码：

```python
allLiXpath = "//li[@class='b_algo' or starts-with(@class, 'b_ad')]"
resultLiList = resultElem.find_elements_by_xpath(allLiXpath)
```

## text()

* 对于HTML代码：
```html
<a target="_self" href="/s?rsv_idx=1&amp;wd=111&amp;usm=3&amp;ie=utf-8&amp;sl_lang=en&amp;rsv_srlang=en&amp;rsv_rq=en&amp;rqlang=cn">英文结果</a>
```
定位英文结果即可使用：
`//a[text()="英文结果"]`

另外一个例子：
* `clickHereBtnElement = driver.find_element_by_xpath('//a[text()="click here"]')` 中的 `text()="click"`

## last()

* `//input[@name="identity"][last()]`

## concat()

举例：

* docbook的xml的处理 -》XSLT中使用xpath
    ```xml
    <xsl:key name="book" match="books/book" use="concat(@title, '|', @author)"/>
    ```
* 其他例子
  * `concat('un', 'grateful')` -> `ungrateful`
  * `concat('Thy ', (), 'old ', "groans", "", ' ring', 'yet', ' in', ' my', ' ancient',' ears.')` -> `Thy old groans ring yet in my ancient ears.`
