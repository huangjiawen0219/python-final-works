# Python 2019秋季期末项目展示
- **代码GitHub的url** https://github.com/huangjiawen0219/python-final-things
- **pythonanywhere**的url http://huangjiawen.pythonanywhere.com/?

## 网页功能
- 通过用户的选择主题，展示关于ted主题的内容。
- 背景故事
- 可视化数据
- 相关分析/总结
- 数据故事

## 功能扩展
- 用户可通过多种自定的选择跳转交互页面，查看进行数据筛选后不同的内容。

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

## 数据交互档描述
- 是否含有合适的推导式
# 浏览量和评论数的关系
@app.route('/Scatter')
def index_bar():
    ted = pd.read_csv("./static/data/ted_main.csv")
    ted['film_date'] = ted['film_date'].apply(lambda x: datetime.datetime.fromtimestamp(int(x)).strftime('%d-%m-%Y'))
    ted['published_date'] = ted['published_date'].apply(
        lambda x: datetime.datetime.fromtimestamp(int(x)).strftime('%d-%m-%Y'))
    r = (
        EffectScatter()
            .add_xaxis(ted['views'].values.tolist())
            .add_yaxis('商家A', ted['comments'].values.tolist())
            .set_global_opts(
            title_opts=opts.TitleOpts(title="EffectScatter-基本示例"),
            xaxis_opts=opts.AxisOpts(
                type_="value",  # x轴数据类型是连续型的
                min_=0  # x轴范围最小为20
            ))
    )
    return render_template('index.html',
                           myechart=r.render_embed(),select=list(res.keys()))

- 处理数据
for i in df:
    if i[0] not in res:
        res[i[0]] = {i[1]: 1}
    else:
        if i[1] not in res[i[0]]:
            res[i[0]][i[1]] = 1
        else:
            res[i[0]][i[1]] += 1

- 是否含有合适的数据结构嵌套
# 浏览量和评论数TOP10视频是
@app.route('/bar1')
def index_bar_every_1_tp():
    ted = pd.read_csv("./static/data/ted_main.csv")
    ted['film_date'] = ted['film_date'].apply(lambda x: datetime.datetime.fromtimestamp(int(x)).strftime('%d-%m-%Y'))
    ted['published_date'] = ted['published_date'].apply(
        lambda x: datetime.datetime.fromtimestamp(int(x)).strftime('%d-%m-%Y'))
    views_ted = ted[['main_speaker', 'title', 'published_date', 'views', 'comments', 'tags', 'speaker_occupation',
                     'num_speaker']].sort_values(by='views', ascending=False)

    views_ted_1 = ted[['main_speaker', 'title', 'published_date', 'views', 'comments', 'tags', 'speaker_occupation',
                       'num_speaker']].sort_values(by='comments', ascending=False)
    bar = (
        Bar()
            .add_xaxis(views_ted.head(10).main_speaker.values.tolist())
            .add_yaxis("top10", views_ted.head(10).views.values.tolist())
            .set_global_opts(title_opts=opts.TitleOpts(title="浏览量和评论数TOP10视频"))
            .set_series_opts(
            label_opts=opts.LabelOpts(is_show=True),
        )
    )
    bar1 = (
        Bar()
            .add_xaxis(views_ted_1.head(10).main_speaker.values.tolist())
            .add_yaxis("top10", views_ted_1.head(10).comments.values.tolist())
            .set_global_opts(title_opts=opts.TitleOpts(title="浏览量和评论数TOP10视频"))
            .set_series_opts(
            label_opts=opts.LabelOpts(is_show=True),
        )
    )
    grid = (
        Grid()
            .add(bar, grid_opts=opts.GridOpts(pos_bottom="60%"))
            .add(bar1, grid_opts=opts.GridOpts(pos_top="60%"))
    )

    return render_template('index.html',
                           myechart=grid.render_embed(),select=list(res.keys()))
