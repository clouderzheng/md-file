##������ʽ
##������ʽ

###Ԫ�ַ�
    .   �����ַ������н���������ƥ��Ҳ���ܲ�ƥ�䣩
    /s  ���ַ���[ \t\n\x0B\f\r]
    /s  �ǿ��ַ���[^\s]
    /d  ����[0-9]
    /D  ������[^0-9]
    /w  �����ַ�[a-zA-Z_0-9]
    /W  �ǵ����ַ�[^\w]
    
###�ַ���
    [abc]     a��b �� c�����ࣩ
    [^abc]     �κ��ַ������� a��b �� c���񶨣�
    [a-zA-Z] 	a �� z �� A �� Z����ͷ����ĸ�������ڣ���Χ��
    [a-d[m-p]] 	a �� d �� m �� p��[a-dm-p]��������
    [a-z&&[def]] 	d��e �� f��������
    [a-z&&[^bc]] 	a �� z������ b �� c��[ad-z]����ȥ��
    [a-z&&[^m-p]] 	a �� z������ m �� p��[a-lq-z]����ȥ��

###�߽�ƥ����
    ^       �еĿ�ͷ
    \$      �еĽ�β
    \b      ���ʱ߽�
    \B      �ǵ��ʱ߽�
    \A      ����Ŀ�ͷ
    \G      ��һ��ƥ��Ľ�β
    \Z      ����Ľ�β�����������Ľ�����
    \z      ����Ľ�β
    

###����ʹ������
    
    ������ ��abc��  abc�е�����һ��
    Բ����  ��ab��  ab��Ϊһ��������
    ������   {x} ��������{1}һ�� {1��}����һ�� {1,3}����һ�Σ�����3��
    
###����

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
       "              <input type=\"hidden\" name=\"message_desc\" value=\"�������ظ�\" /><br/>                             "+
       "              <input type=\"hidden\" name=\"order_id\" value=\"RSR281248\" /><br/>                                  "+
       "         </form>                                                                                                    "+
       "                                                                                                                    "+
       "     </body>                                                                                                        "+
       " </html>";
###��ȡ������
    Pattern pattern = Pattern.compile("<input[\\s\\S]+name=\"order_id\"+[\\s]+value=\"([\\s\\S]*?)\"");
###��ȡ��ַ����
    Pattern pattern = Pattern.compile("<form[\\s\\S]+action=\"([\\s\\S]+?)\"");

##���ݴ���
###URL���ӷ�ʽ  
####����
    @Test
    public void testSendMes(){
        Map<String, Object> map = new HashMap<String, Object>();
        map.put("name", "֣����");
        map.put("age", "23");
        map.put("gender", "��");
        map.put("address", "�Ĵ��ɶ�");
        map.put("interest", "��Ƥ");
        map.put("appearance", "handsome");
        map.put("appid", "100012");
        map.put("sign", Md5Encrypt.md5(JSON.toJSONString(map)));
        
        try {
            URL url = new URL("http://192.168.1.108:9112/sendMes/getObject");
            
            URLConnection connection = url.openConnection();//����һ�� URLConnection ��������ʾ�� URL �����õ�Զ�̶�������ӡ�
            connection.setRequestProperty("Content-Type","application/json");//ָ������Ϣ��װ��������  reqesutΪ��  @responseBody����
            connection.setDoOutput(true);//֧�����
            connection.setDoInput(true);//֧������
            
            String param = JSON.toJSONString(map);
            OutputStream out = connection.getOutputStream();
            out.write(param.getBytes("UTF-8"));
            BufferedReader reader = new BufferedReader(new InputStreamReader(connection.getInputStream()));
            String result = null;
            StringBuilder buffer = new StringBuilder();
            while(null != (result = reader.readLine())){
                buffer.append(result);
            }
            System.out.println("���ؽ��----->"+buffer);
        }
        catch (Exception e) {
            e.printStackTrace();
        }
    }
###HttpClient ����
####���� @Test
    public void sendInfoBynvps(){
        try {
            HttpClient httpClient = new SSLClient();
            HttpPost postMethod = new HttpPost("http://192.168.1.108:9112/sendMes/getObject1");
            List<BasicNameValuePair> nvps = new ArrayList<BasicNameValuePair>();
            nvps.add(new BasicNameValuePair("name", "֣����"));
            nvps.add(new BasicNameValuePair("gender", "��"));
            nvps.add(new BasicNameValuePair("age", "23"));
            nvps.add(new BasicNameValuePair("address", "�Ĵ��ɶ�"));
            nvps.add(new BasicNameValuePair("interest", "��Ƥ"));
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
    �÷�������ʹ��@responseBody ���ղ���   ����request.getParamterMap ��  ֱ��ʵ����ղ�Ϊ��
    