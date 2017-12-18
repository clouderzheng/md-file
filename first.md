

<script type="text/javascript" src="https://cdn.mathjax.org/mathjax/latest/MathJax.js?config=TeX-AMS_HTML"></script>
#接口文档
##文档说明
###数据类型
***
统一使用utf-8数据格式
___
###加密方式
***
数据按照ascii排序，以key=value&...的方式连接，最后加上key=key值，进行[md5](http://baike.baidu.com/link?url=15_MAs19tzxrxi84maRVXrHKgPLKsONG0L76fDMFQG9D92a9xhEEfajzaLpOMav_JaLmMknJigd2MS2MCt8ln_  "MD5说明")加密
***
>郑净云编写
>>2017.1.12
***

##文档更新说明
###加密规则
***
不再使用MD5加密，不安全，现在采用AES非对称加密，平台持有公玥，渠道持有私玥，加密时都采用自己的私玥加密，公玥揭秘，各自保管好自己的私玥，以防数据安全

###进件参数
#####      key|value
    phone|手机号
    merNo|平台商户号，平台唯一
    requestNo|请求流水号 保证每一条数据唯一
    agentId|代理商id
###返回参数
####    key|value
    requestNo|请求流水号，n每一次请求唯一
    channelNo|d渠道分配给商户交易商户号 每个商户必须唯一
    status|状态   1 成功 2 失败 
###交易参数
#####  key|value
    
    channelNo|渠道分配给商户商户号 每个商户必须唯一
    requestNo|请求流水号  每次请求必须唯一
    amount|交易金额  单位（分）
    rate|交易费率 以千位底   l例：  9  表示  0.009
###渠道统计
     |  channelId  |  trandeAmount  |  tradeTime  |
     |:-----:|:----|-----:|
    |浦发|单笔5000，单日20000|T1到账|


###表格
    | 姓名     | 年龄| 性别|
    
    
    |:--------|---------:|:-------:|
    | 张三| 18| 女      |
    | 小明| 23| 男      |
    
###color
<table border="1">
<caption>人物性格调查</caption>
    <tr>
        <td>name</td>
        <td>age</td>
        <td>gender</td>
        <td>interest</td>
    </tr>
     <tr>
        <td>night</td>
        <td>22</td>
        <td>男</td>
        <td>飙车</td>
    </tr>
     <tr>
        <td>lucy</td>
        <td>18</td>
        <td>女</td>
        <td>画画</td>
    </tr>

</table>

###AES加密
	[网址]http://tool.chacuo.net/cryptgetpubkey

