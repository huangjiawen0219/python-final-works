# Python 2019秋季期末项目展示
- **代码GitHub的url** https://github.com/huangjiawen0219/python-final-things
- **pythonanywhere**的url http://huangjiawen.pythonanywhere.com/?

## HTML档描述
- 1.所有的HTML文件放置在templates文件夹中，其中base.html为基模板，其余html皆继承该基模板。
- 2.base.html设定基本flask html模版档
- 3.使用了 entry.html，为flask html模版档
- 4.用户输出结果页使用 summary.html
- 5.用户输出结果页使用了 viewlog.html
- 6.运用了HTML的<img>标签，插入了头部图片，实现头部图片的功能。
- 7.运用了HTML中<a href>标签，实现了点击图片跳转到相关网页链接的功能。

## Python档描述
- 1.安装并导入pandas、pyecharts、cufflinks、plotly等第三方包
- 2.运用了flask模板以及jinjia2呈现的web页面，从flask呈现模板
- 3.Flask提供了一个名为render_template的函数，将这个函数增加到从flask模板导入的函数列表中，根据需要调用这个函数，最终显示出Web应用的
  HTML表单。安装Flask环境，导入flask和render_template函数，创建Flask对象实例
- 4.Flask提供了一个内置对象，名为request。我们利用这个对象可以访问所提交的数据。
- 5.创建url和函数，用url修饰函数，呈现不同的HTML页面
- 6.request对象包含一个名为form的字典属性，可以访问从浏览器提交的HTML表单数据。
- 7.通过表单的功能，实现了数据的交互，可以从筛选按钮中选出相应的数据。

## Web app档描述
- 1.后端服务器成功启动：执行 app.py 启动后端服务器，等待web请求。启动成功出现：Running on http://127.0.0.1:5000/
- 2.接着，服务器访问 http://127.0.0.1:5000/ ，启动前端web 请求
- 3.app.py中执行了@app.route('/') 下的 index()函数，产生《TED INSIGHT》的HTML页面
- 4.紧接着，前端浏览器收到web响应，出现HTML页面


- 【前端页面——TED数据分析】
- 点击“TED数据分析”，即可跳转到【TED数据分析】
- 点击按钮“首页”，即可跳转到【首页】；
- 点击按钮“浏览数和top10的页面是”，即可跳转到【浏览数和top10的页面是】数据曲线图；
- 点击按钮“主讲人都来自什么职业”，即可跳转到【主讲人都来自什么职业】数据曲线图；
- 点击按钮“每个时间段的评论和浏览量”，即可跳转到【每个时间段的评论和浏览量】数据曲线图；
- 点击按钮“浏览量和评论数的关系”，即可跳转到【浏览量和评论数的关系】数据曲线图

-【前端页面——TED数据筛选】
- 点击“TED数据筛选”，即可跳转到【TED数据筛选】
- 点击按钮“首页”，点击“选择”，即可跳转到【首页】；
- 点击按钮选项“孩子们”，点击“选择”，即可跳转到【孩子们】数据曲线图；
- 点击按钮“内向的人”，点击“选择”，即可跳转到【内向的人】数据曲线图；
其他页面动作与以上相似。
