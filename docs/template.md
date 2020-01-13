### 全局标签

**网站名字**

功能说明：输出当前网站的名字

使用方法：`{{ sitename }}`

**网站描述**

功能说明：输出当前网站的描述

使用方法：`{{ sitedesc }}`

**网站关键词**

功能说明：输出当前网站的主关键词

使用方法：`{{ sitekey }}`

**网站URL**

功能说明：输出当前网站的URL地址，带http的主域名，例：http://www.domain.com

使用方法：`{{ siteurl }}`

**分隔符**

功能说明：输出一个分隔符，每个站随机固定一个符号，例：- | 

使用方法：`{{ sep }}`

**meta标签集**

功能说明：输出默认定义好的meta数据块，其中包含keyword标签、description标签、og标签数据输出的标签块内容已由后台自动填补

使用方法：`{% raw meta_info %}`

**seo标题**

功能说明：输出网站seo标题

使用方法：`{% seotitle %}`

**随机号码**

功能说明：生成随机11位电话号码

使用方法：`{{ tel }}`

**随机邮箱**

功能说明：生成随机以当前域名结尾的企业邮箱

使用方法：`{{ email }}`

**随机数**

功能说明：生成小于500的随机数

使用方法：`{{ rand(500) }}`

**栏目标签**

功能说明：该标签是一个for循环，默认输出当前网站的所有栏目信息。

基本语法：`{% for c_info in cats(num="") %}...{% end %}`

发送参数：

+ num：返回数量，默认返回所有

返回参数：

+ u：栏目URL
+ n：栏目名字

使用方法：
    
    <ul>
      {% for c_info in cats(num="") %}
      <li class=""><a href="{{siteurl}}/{{c_info['u']}}/">{{c_info['n']}}</a></li>
      {% end %}
    </ul>


**关键词标签**

功能说明：该标签是一个for循环，根据传进来的参数输出关键词列表。

基本语法：`{% for item in tags(num="",cat_uri="",tag=""，length="") %}...{% end %}`

发送参数：

+ num：返回数量，可为空
+ cat_uri：相关的分类
+ tag：相关的关键词
+ length：标签长度


返回参数：

+ tags：关键词


使用方法：
    
    {% for item in tags(num=5,cat_uri="",tag="考试",length=4) %}
      <li>{{ item }}</li>
    {%end%}

**文章标签**

功能说明：该标签是一个for循环，根据传进来的参数输出文章列表。

基本语法:

`{% get_article(type="",col="",area="",key="",rand="",flag="",num=5) %}...{% end %}`

发送参数：

- type：文章类型，可为空
	- hot：热门文章
	- low：全站最差
	- pic：全部包含图片
	- rand：全站随机，使用此类型后rand参数将无效
	- today：今日文章
	- week：本周文章
	- month：本月文章
	- year：本年文章
	- area：按地区获取，以area参数值为准
	- key：按关键词获取，以key参数值为准
	- flag：以flag参数值为准
	- new - 最新文章
- flag：文章标识，此参数表示获取需要获取某个类型的文章，可为空
	- h：头条
	- c：推荐
	- p：图片
	- b：加粗
	- j：跳转
- rand：是否随机，此参数表示是否随机获取文章，可为空
	- 0：不随机
	- 1：随机
- num：要获取的文章数量
- col：所属栏目URL，此参数表示获取某个栏目下的文章，可为空
- area：所属地区，此参数表示获取某个地区相关的文章，可为空
- key：关键词，此参数表示获取跟某个关键词相关的文章，可为空

返回参数：

- id：文章id
- title：文章标题
- content：文章内容
- img_url：文章主图url
- cat_uri：所属分类url
- author：文章作者
- tags：文章标签
- date：文章时间

使用方法：

    {% for post in get_article(type="new", col="", area="", key="", rand="", flag="", num=10) %}
    <li>
      <a href="{{siteurl}}/{{post['cat_uri']}}/{{post['id']}}.html">
        <img src="{{post['img_url']}}"
        {{post['title']}}
      </a>
    </li>
    {% end %}

**内容截取标签**

功能说明：该标签是一个函数，根据传进来的参数返回截取的内容。

基本语法:`{%raw abstract(content="",num="") %}`

发送参数：

- content：原始内容，不可为空
- num：截取前多少个字，可为空，默认截取100个字

返回参数：

- 直接返回截取的内容

使用方法：

    {%raw abstract(item['content'],120) %}

### 内容页标签

**og信息**

功能说明：输出当前文章的og信息

使用方法：`{% raw og_info %}`

post标签是一个数组，里面存储了当前文章的所有信息

**文章标题**

功能说明：输出当前文章的标题

使用方法：`{{post['title']}}`

**发布时间**

功能说明：输出当前文章的发布时间

使用方法：`{{post['date']}}`

**文章作者**

功能说明：输出当前文章的作者

使用方法：`{{post['author']}}`

**文章标签**

功能说明：输出当前文章的所有标签

使用方法：`{{post['tags']}}`

**文章内容**

功能说明：输出当前文章的内容

使用方法：`{% raw post['content'] %}`

**文章主图**

功能说明：输出当前文章的主图URL

使用方法：`{{post['img_url']}}`

**上一篇相关标签**

功能说明：当前文章的上一篇文章

使用方法：`{% up_article %}`

功能说明：上一篇文章的标题

使用方法：`{{up_article[0]['title']}}`

功能说明：上一篇文章的id

使用方法：`{{up_article[0]['id']}}`

配合if语句使用，基本语法如下：

    {% if up_article %}
        上一篇: <a href="{{siteurl}}/{{category['u']}}/{{up_article[0]['id']}}.html">{{up_article[0]['title']}}</a>
    {% else %}
        上一篇: <a href="{{siteurl}}/{{category['u']}}/">返回列表</a>
    {% end %}


**下一篇相关标签**

功能说明：当前文章的下一篇文章

使用方法：`{% down_article %}`

功能说明：下一篇文章的标题

使用方法：`{{down_article[0]['title']}}`

功能说明：下一篇文章的id

使用方法：`{{down_article[0]['id']}}`

配合if语句使用，基本语法如下：

    {% if down_article %}
        下一篇: <a href="{{siteurl}}/{{category['u']}}/{{down_article[0]['id']}}.html">{{down_article[0]['title']}}</a>
    {% else %}
        下一篇: <a href="{{siteurl}}/{{category['u']}}/">返回列表</a>
    {% end %}

### 关键词页相关标签

**关键词**

功能说明：输出当前页面的关键词

使用方法：`{% raw main_key %}`

**关键词描述**

功能说明：输出html代码，内容为当前页面的描述，包含关键词和网站名等信息，用于页面head中

使用方法：`{% raw tag_desc %}`

### 文章tags标签

功能说明：获取文章关键词的名字和URL

使用范围：在获取到文章之后使用，处理文章的tags时必须使用此方法

基本语法：`{% for tag in article['tags'] %}...{% end %}`

基本使用：

    {% for post in get_article(num=5") %}
        {% for tag in post['tags'] %}
            <a href="{{tag['url']}}">{{tag['tag']}}</a>
        {% end %}
    {% end %}

### 栏目页、内容页通用栏目标签

category标签是一个数组，里面存储了当前栏目的所有信息

**栏目名字**

功能说明：输出当前栏目名字
使用方法：`{{category['n']}}`

**栏目URL**

功能说明：输出当前栏目的相对网址
使用方法：`{{category['u']}}`

**栏目描述**

功能说明：输出当前栏目描述
使用方法：`{{category['d']}}`

**栏目关键词**

功能说明：输出当前栏目描述
使用方法：`{{category['k']}}`

## 栏目页、关键词页文章标签

该标签是一个for循环，遍历输出当前栏目下的文章，默认已分页

基本语法：

`{%set data=get_posts(30) %}`
`{% for item in data['post'] %}`

返回参数：

- id：文章id
- title：文章标题
- content：文章内容
- author：文章作者
- tags：文章标签
- date：发布时间

基本使用： 

    {%set data=get_posts(30) %}
    {% for item in data['post'] %}
    <li>
      <h2>
        <a href="{{siteurl}}/{{category['u']}}/{{item['id']}}.html">{{item['title']}}</a></h2>
        <div class="single-meta">
          <span class="time">时间：{{item['date']}}</span>
          <span class="author pull-right">作者：{{item['author']}}</span>
        </div>
            <p>{%raw abstract(item['content']) %}&hellip;</p>
            <div class="post-tags mt20">标签：{{item['tags']}}</div>
    </li>
    {%end%}

### 栏目页、关键词页通用分页标签


该标签是一个for循环，根据参数自动生成当前栏目的分页代码

基本语法：

`{% for i in page_num_list(tag='',style='',current_style='',current_tag='') %}{% end %}`

发送参数：

- tag：每个分页数字的HTML标签种类，如div或span
- style：每个分页数字所在的HTML标签的class值
- current_style：当前页码的HTML标签的class值，不设置则默认使用参数style的值
- current_tag：当前页码的HTML标签种类，不设置则默认使用参数tag的值


返回参数：

- 返回HTML文本

基本使用：

    {% for i in page_num_list(tag='span', style='page-numbers', current_style='current') %}
    {% raw i %}
    {% end %}

### 搜索功能接口

功能说明：根据传入内容搜索全站文章，将会跳转到关键词页面

接口地址：`/search`

请求方法：POST

发送参数：

- s：需要搜索的内容

响应内容：

- 跳转到结果页

### 获取各类型文章方法集合

参数说明：

| **参数** | **参数值** | **说明** |
| :---: | :---: | :---: |
| type | hot：全站热门</br>low：全站最差</br>pic：全部包含图片</br>rand：全站随机（使用此类型后rand参数将无效）</br>today：今日文章</br>week：本周文章</br>month：本月文章</br>year：本年文章</br>area：按地区获取，以area参数值为准</br>key：按关键词获取，以key参数值为准</br>flag：以flag参数值为准</br>new-最新文章 | 按参数值回去各种类型的文章，目前返回id，title，cat_uri，content，img_url |
| num | 5 | 获取的文章数量，默认5 |
| col | lanmu | 通过栏目uri获取指定栏目下的文章 |
| key | 关键词1 | 通过关键词获取文章 |
| rand | 1|0 | 是否随机，1为真，0为否 |
| flag | h | 文章标识，头条h，推荐c，图片p，加粗b，跳转j，无标识'' |
| area | 广州 | 通过地区获取文章 |


**获取热门文章**

可选参数：col,rand,flag,num

获取全站热门文章：`get_article(type="hot", col="", area="", key="", rand="", flag="", num=6)`

获取当前栏目下热门文章：`get_article(type="hot", col=cat_uri, area="", key="", rand="", flag="", num=6)`

获取全站热门随机文章：`get_article(type="hot", col="", area="", key="", rand=1, flag="", num=6)`

获取当前栏目下热门随机文章：`get_article(type="hot", col="", area="", key="", rand=1, flag="", num=6)`


**获取冷门文章**

可选参数：col,rand,flag,num

获取全站冷门文章：`get_article(type="low", col="", area="", key="", rand="", flag="", num=6)`

获取当前栏目下冷门文章：`get_article(type="low", col=cat_uri, area="", key="", rand="", flag="", num=6)`

获取全站冷门随机文章：`get_article(type="low", col="", area="", key="", rand=1, flag="", num=6)`

获取当前栏目下冷门随机文章：`get_article(type="low", col=cat_uri, area="", key="", rand=1, flag="", num=6)`

**获取包含主图文章**

可选参数：col,rand,flag,num

获取全站包含主图文章：`get_article(type="pic", col="", area="", key="", rand="", flag="", num=6)`

 获取当前栏目下包含主图文章：`get_article(type="pic", col=cat_uri, area="", key="", rand="", flag="", num=6)`

获取全站包含主图随机文章：`get_article(type="pic", col="", area="", key="", rand=1, flag="", num=6)`

获取当前栏目下包含主图随机文章：`get_article(type="pic", col=cat_uri, area=cat_uri, key="", rand=1, flag="", num=6)`

**获取随机文章**

可选参数：col,rand,num

获取全站随机文章：`get_article(type="rand", col="", area="", key="", rand="", flag="", num=6)`
`get_article(type="rand", col="", area="", key="", rand=0, flag="", num=6)`
`get_article(type="rand", col="", area="", key="", rand=1, flag="", num=6)`

 获取当前栏目下随机文章：`get_article(type="rand", col=cat_uri, area="", key="", rand="", flag="", num=6)`
`get_article(type="rand", col=cat_uri, area="", key="", rand=0, flag="", num=6)`
`get_article(type="rand", col=cat_uri, area="", key="", rand=1, flag="", num=6)`

**获取时间修改文章**

可选参数：col,flag,num

获取随机时间文章：全站当天
`get_article(type="today", col="", area="", key="", rand="", flag="", num=6)`

当前栏目当天
`get_article(type="today", col=cat_uri, area="", key="", rand="", flag="", num=6)`

全站本周
`get_article(type="week", col="", area="", key="", rand="", flag="", num=6)`

当前栏目本周
`get_article(type="week", col=cat_uri, area="", key="", rand="", flag="", num=6)`

全站本月
`get_article(type="month", col="", area="", key="", rand="", flag="", num=6)`

当前栏目本月
`get_article(type="month", col=cat_uri, area="", key="", rand="", flag="", num=6)`

全站本年
`get_article(type="year", col="", area="", key="", rand="", flag="", num=6)`

当前栏目本年
`get_article(type="year", col=cat_uri, area="", key="", rand="", flag="", num=6)`

**获取相关地区文章**

可选参数：col,area,rand,flag,num

获取全站地区文章：`get_article(type="area", col="", area="广州", key="", rand="", flag="", num=6)`

获取当前栏目下地区文章：`get_article(type="area", col=cat_uri, area="广州", key="", rand="", flag="", num=6)`

获取全站本地区下随机文章：`get_article(type="area", col="", area="广州", key="", rand=1, flag="", num=6)`

 获取当前栏目下本地区下随机文章：`get_article(type="area", col=cat_uri, area="广州", key="", rand=1, flag="", num=6)`

**获取相关关键词文章**

可选参数：col,key,rand,flag,num

获取全站关键词文章：`get_article(type="key", col="", area="", key="高考", rand="", flag="", num=6)`

 获取当前栏目下关键词文章：`get_article(type="key", col=cat_uri, area="", key="高考", rand="", flag="", num=6)`

 获取全站本关键词的随机文章：`get_article(type="key", col="", area="", key="高考", rand=1, flag="", num=6)`

 获取当前栏目下本关键词的随机文章：`get_article(type="key", col=cat_uri, area="", key="高考", rand=1, flag="", num=6)`

**获取置顶文章**

可选参数：col,rand,flag,num

获取全站置顶文章：`get_article(type="flag", col="", area="", key="", rand="", flag="h", num=6)`

 获取当前栏目下置顶文章：`get_article(type="flag", col=cat_uri, area="", key="", rand="", flag="h", num=6)`

 获取全站置顶随机文章：`get_article(type="flag", col="", area="", key="", rand=1, flag="h", num=6)`

 获取当前栏目下置顶随机文章：`get_article(type="flag", col=cat_uri, area="", key="", rand=1, flag="h", num=6)`

**获取最新文章**

可选参数：col,flag,num

获取全站最新文章：`get_article(type="new", col="", area="", key="", rand="", flag="", num=6)`

获取当前栏目下最新文章：`get_article(type="new", col=cat_uri, area="", key="", rand="", flag="", num=6)`
