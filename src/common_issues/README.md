# 常见问题

## 在当前节点下面搜索子节点=相对路径搜索

```html
<html>
    <ol id="b_results">
        <li class="b_ad">
            <ul>
                <li class="b_adLastChild">
                    <div class="sb_add sb_adTA">
                        <h2>
                            <a id="tile_link_cn" href="http://e.so.com/search/eclk">xxx</a>
                        </h2>
                    </div>
                </li>
            </ul>
        </li>

        <li class="b_algo">
            <h2>
                <a target="_blank" href="http://www.drv5.cn/azgame/77154.html">yyy</a>
            </h2>
        </li>
    </ol>
</html>
```

* `/`：从根节点开始算起，向下搜索
  * 说明：
    * 类似于文件夹的绝对路径
      * 举例
        * `/Users/limao/dev/`
  * 举例
    * `/html/ol/li[@class='b_ad']` 可定位到 `<li class="b_ad">`
* `//`：从（根节点向下）任意层级开始搜索
  * 举例
    * `//ol/li[@class='b_ad']` 或 `//li[@class='b_ad']` 均可定位到 `<li class="b_ad">`
* `./` 或 `.//`：**点**=`` 表示相对路径，相对当前元素，向下开始搜索子节点
  * 举例
    * 此处已获取到 `<li class="b_algo">`元素，想要去搜`<a target="_blank" href="http://www.drv5.cn/azgame/77154.html">yyy</a>`，则
      * 可以用
      * `./h2/a` 或 `.//a`
      * 不能用
        * `//h2/a`
          * 否则会误搜出 文件根节点开始的第一个`h2`的`a`，此处即`<li class="b_ad">`下面的`<a id="tile_link_cn" href="http://e.so.com/search/eclk">xxx</a>`

