##正则表达式
##正则表达式

###元字符
    .   任意字符（与行结束符可能匹配也可能不匹配）
    /s  空字符串[ \t\n\x0B\f\r]
    /s  非空字符串[^\s]
    /d  数字[0-9]
    /D  非数字[^0-9]
    /w  单词字符[a-zA-Z_0-9]
    /W  非单词字符[^\w]
    
###字符类
    [abc]     a、b 或 c（简单类）
    [^abc]     任何字符，除了 a、b 或 c（否定）
    [a-zA-Z] 	a 到 z 或 A 到 Z，两头的字母包括在内（范围）
    [a-d[m-p]] 	a 到 d 或 m 到 p：[a-dm-p]（并集）
    [a-z&&[def]] 	d、e 或 f（交集）
    [a-z&&[^bc]] 	a 到 z，除了 b 和 c：[ad-z]（减去）
    [a-z&&[^m-p]] 	a 到 z，而非 m 到 p：[a-lq-z]（减去）

###边界匹配器
    ^       行的开头
    \$      行的结尾
    \b      单词边界
    \B      非单词边界
    \A      输入的开头
    \G      上一个匹配的结尾
    \Z      输入的结尾，仅用于最后的结束符
    \z      输入的结尾
    

###括号使用限制
    
    方括号 【abc】  abc中的任意一个
    圆括号  （ab）  ab作为一个搜索组
    大括号   {x} 次数限制{1}一次 {1，}至少一次 {1,3}至少一次，至多3次
    
###例子

    static  String  html =  "<html>"+                                                                                       
       "     <head>                                                                                                         "+
       "         <meta http-equiv=\"Content-Type\" content=\"text/html; charset=utf8\">                                     "+
       "         <script type=\"text/javascript\">                                                                          "+
       "             function doSubmit(){                                                                                   "+
       "                 document.getElementById(\"form1\").submit();                                                       "+
       "             }                                                                                                      "+
       "         </script>                                                                                                  "+
       "     </head>                                                                                                        "+
       "     <body onload=\"doSubmit()\">                                                                                   "+
       "        <form id=\"form1\" method=\"post\" action=\"http://union.fastpay.rsrtech.net/union/toPayResultPage\">       "+
       "              <input type=\"hidden\" name=\"message_code\" value=\"000009\" /><br/>                                 "+
       "              <input type=\"hidden\" name=\"message_desc\" value=\"订单号重复\" /><br/>                             "+
       "              <input type=\"hidden\" name=\"order_id\" value=\"RSR281248\" /><br/>                                  "+
       "         </form>                                                                                                    "+
       "                                                                                                                    "+
       "     </body>                                                                                                        "+
       " </html>";
###获取订单号
    Pattern pattern = Pattern.compile("<input[\\s\\S]+name=\"order_id\"+[\\s]+value=\"([\\s\\S]*?)\"");
###获取地址链接
    Pattern pattern = Pattern.compile("<form[\\s\\S]+action=\"([\\s\\S]+?)\"");

##数据传输
###URL链接方式  
####例子
    @Test
    public void testSendMes(){
        Map<String, Object> map = new HashMap<String, Object>();
        map.put("name", "郑净云");
        map.put("age", "23");
        map.put("gender", "男");
        map.put("address", "四川成都");
        map.put("interest", "哈皮");
        map.put("appearance", "handsome");
        map.put("appid", "100012");
        map.put("sign", Md5Encrypt.md5(JSON.toJSONString(map)));
        
        try {
            URL url = new URL("http://192.168.1.108:9112/sendMes/getObject");
            
            URLConnection connection = url.openConnection();//返回一个 URLConnection 对象，它表示到 URL 所引用的远程对象的连接。
            connection.setRequestProperty("Content-Type","application/json");//指定流信息包装在请求体  reqesut为空  @responseBody接收
            connection.setDoOutput(true);//支持输出
            connection.setDoInput(true);//支持输入
            
            String param = JSON.toJSONString(map);
            OutputStream out = connection.getOutputStream();
            out.write(param.getBytes("UTF-8"));
            BufferedReader reader = new BufferedReader(new InputStreamReader(connection.getInputStream()));
            String result = null;
            StringBuilder buffer = new StringBuilder();
            while(null != (result = reader.readLine())){
                buffer.append(result);
            }
            System.out.println("返回结果----->"+buffer);
        }
        catch (Exception e) {
            e.printStackTrace();
        }
    }
###HttpClient 链接
####例子 @Test
    public void sendInfoBynvps(){
        try {
            HttpClient httpClient = new SSLClient();
            HttpPost postMethod = new HttpPost("http://192.168.1.108:9112/sendMes/getObject1");
            List<BasicNameValuePair> nvps = new ArrayList<BasicNameValuePair>();
            nvps.add(new BasicNameValuePair("name", "郑净云"));
            nvps.add(new BasicNameValuePair("gender", "男"));
            nvps.add(new BasicNameValuePair("age", "23"));
            nvps.add(new BasicNameValuePair("address", "四川成都"));
            nvps.add(new BasicNameValuePair("interest", "嗨皮"));
            nvps.add(new BasicNameValuePair("appearance", "handsome"));
            postMethod.setEntity(new UrlEncodedFormEntity(nvps, "UTF-8"));
            HttpResponse resp = httpClient.execute(postMethod);
            String str = EntityUtils.toString(resp.getEntity(), "UTF-8");
            System.out.println("notify data is ---->"+str);
        }
        catch (Exception e) {
            e.printStackTrace();
        }
    }
    该方法不可使用@responseBody 接收参数   但是request.getParamterMap 与  直接实体接收不为空
    