# 场景和举例

下面就来介绍一下XPath的常见使用场景和具体的示例。

## XPath常见使用场景

比如之前自己就遇到过的：

* `Docbook`的`xml`的处理中的`XSLT`中使用`xpath`
* `Beautifulsoup`中的html的提取
* `Selenium`中元素的选择
* `Scrapy`的`Selector`中提取内容

## XPath使用举例

TODO：
1.把selenium相关的帖子中的示例代码，尤其是关于xpath的，整理过来供参考

### 常见符号和属性判断

#### `@属性`举例

对于判断元素中是否包含某个属性（注意不是去判断属性的值），则语法是：`[@someProperty]`

比如：
```html
<span aria-label="Price" class="x-hidden-focus">$799.00</span>
```
和
```html
<div class="price-text srv_price">
    <s class="srv_saleprice" aria-label="Full price was $1,699.00">$1,699.00</s>
    <span>&nbsp;</span>
    <div class="price-disclaimer ">
        <span aria-label="Now $1,299.00" class="x-hidden-focus">$1,299.00</span>
    </div>
</div>
```

只想要判断spand中存在aria-label属性即可，则可以用：`//span[@aria-label]`

更多例子如下：

* `@class="dropdown-menu"`
    * `cartNumOptionElemList = driver.find_elements_by_xpath('//ul[@class="dropdown-menu"]/li[@role="option"]')`
* `@name="loginfmt"`
    * `inputEmailElement = WebDriverWait(driver, gCfg["waitTimeout"]).until(
    EC.presence_of_element_located((By.XPATH, '//input[@type="email" and @name="loginfmt"]')))`
* `@id="idSIButton9"`
    * `nextElement = driver.find_element_by_xpath('//input[@type="submit" and @id="idSIButton9" and @value="Next"]')`

#### selenium中特殊列表元素的选择

之前遇到列表选项的html不是`select`的`option`，而是：
```html
<ul id="22bc22dd-ef9d-4d3c-8de9-1e7bc704f9f9_menu" role="group" aria-labelledby="22bc22dd-ef9d-4d3c-8de9-1e7bc704f9f9" class="dropdown-menu">
            <li role="option"> 
<a data-m="{&quot;aN&quot;:&quot;shoppingCart&quot;,&quot;cN&quot;:&quot;UpdateQuantity&quot;,&quot;bhvr&quot;:91,&quot;pid&quot;:&quot;8X58XHDX57SX&quot;,&quot;sku&quot;:&quot;F96R&quot;,&quot;itemCount&quot;:1}" id="22bc22dd-ef9d-4d3c-8de9-1e7bc704f9f9_menuItem_1" class="ember-view x-hidden-focus">                          1
                      
</a>            </li>
            <li role="option"> 
...
```
即，`ul`的`li`的列表

最后用代码：
```python
cartNumOptionElemList = driver.find_elements_by_xpath('//ul[@class="dropdown-menu"]/li[@role="option"]')
cartNumOptionCount = len(cartNumOptionElemList)
logging.info("cartNumOptionElemList=%s,cartNumOptionCount=%s", cartNumOptionElemList, cartNumOptionCount)
if cartNumOptionCount < gCfg["msStore"]["onceBuyNum"]:
    logging.error("Current Cart select max number %s < expected select number %s", cartNumOptionCount, gCfg["msStore"]["onceBuyNum"])
    driver.quit()
toSelectIdx = gCfg["msStore"]["onceBuyNum"] - 1
# carNumSelect = Select(cartNumOptionElemList)
# carNumSelect.select_by_index(gCfg["msStore"]["onceBuyNum"])
carNumSelectElem = cartNumOptionElemList[toSelectIdx]
logging.info("carNumSelectElem=%s", carNumSelectElem)
carNumSelectElem.click()
# aLinkElem = carNumSelectElem.find_element_by_link_text(str(gCfg["msStore"]["onceBuyNum"]))
# logging.info("aLinkElem=%s", aLinkElem)
# aLinkElem.click()
```

去实现，找到列表的元素，点击后下拉显示所有的选项，然后点击选中某个选项：

![seleium中点击下拉选项](../assets/img/seleium_click_option_list.png)
