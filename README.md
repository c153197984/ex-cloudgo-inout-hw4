# HW4：ex-cloudgo-inout

---

## 任务要求
1. 支持静态文件服务
2. 支持简单 js 访问
3. 提交表单，并输出一个表格
4. 对 `/unknown` 给出开发中的提示，返回码 `5xx`

## 任务结果
1. 运行成功后命令行信息如下：
    >  D:\workspace\gp\src\github.com\c153197984\ex-cloudgo-inout> go run main.go
    > [negroni] listening on :8080

    用浏览器进入`localhost:8080/static/`能看到到`assets/index.html`网页。
    
    用浏览器进入`localhost:8080/static/images/`会显示文件列表。
    
    用浏览器进入`localhost:8080/static/images/x.jpg`能看到具体图片。

2. 运行成功后命令行信息同上。
    javascript代码通过获取到Go返回的JSON对象来实现DOM对应元素的替换。

    ```HTML
    <div>
        <p class="item-name">物品名：</p>
        <p class="item-price">价格：</p>
    </div>
    ```

    替换成：
    
    ```HTML
    <div>
        <p class="item-name">物品名：whit55k</p>
        <p class="item-price">价格：66666</p>
    </div>
    ```

3. 在`localhost:8080/static/`定义一个表单（包含物品和价格），跳转到`localhost:8080/record`来实现POST提交的完成。

工作原理：
在record中显示一个表格形式的模板页面，页面位于项目文件夹`/templates/record.tmpl`。
当出现一下情况时重定向到`localhost:8080/static/`：

   1.若进入`localhost:8080/record`的方法为GET

   2.进入`localhost:8080/record`的方法为POST，但价格不是一个符合要求的数字（整数或两位以内小数）。
        
当进入`localhost:8080/record`的方法为POST，且价格合法，就将表单数据应用于模板页面显示。

4. 实现`NotImplemented`和`NotImplementedHandler`（模仿`NotFound`和`NotFoundHandler`）。
    访问`localhost:8080/api/unknown`，页面501 Not Implemented，终端显示
    > [negroni] 2018-1-15T23:38:57+08:00 | 501 |      0s | localhost:8080 | GET /api/unknown
