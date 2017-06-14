![](http://wiki.ziroom.com/plugins/servlet/confluence/placeholder/macro?definition=e3RvY30&locale=zh_CN&version=2)

  


1. ## **资质认证是否完成展示接口**

   **URL**

   {baseurl}/customer/${LOGIN\_UNAUTH}/getCertification

   **HTTPS请求方式**

   POST

   **返回格式**

   JSON

   **是否需要登录**

   是

   **请求参数**

   | 参数名 | 参数类型 | 是否必须 | 参数说明 |
   | :--- | :--- | :--- | :--- |
   | uid | string | 是 | 用户uid |

   **返回结果**

   | {    "status": 0,    "message": "",    "data": {        "fullFlag": "1",        "isCantactAuth": "1",        "isIdentityAuth": "1",        "isFinishHead": "1"    }} |
   | :--- |


   **返回字段说明**

   | 参数名 | 参数类型 | 参数说明 |
   | :--- | :--- | :--- |
   | fullFlag | string | 是否资质认证完成 |
   | isContactAuth | string | 是否联系方式认证完成 |
   | isIdentityAuth | string | 是否身份信息认证完成 |
   | isFinishHead | string | 是否个人信息认证完成 |

   **其它说明**

   完成返回1，否则返回0

2. ## **房东联系方式回显接口**

   **URL**

   {baseurl}/customer/${LOGIN\_AUTH}/getContactInfo

   **HTTPS请求方式**

   POST

   **返回格式**

   JSON

   **是否需要登录**

   是

   **请求参数**

   | 参数名 | 参数类型 | 是否必须 | 参数说明 |
   | :--- | :--- | :--- | :--- |
   | param | string | 是 | 加密参数串 |

   **返回结果**

   |  |
   | :--- |


   ```
   {
       "status": 0,
       "message": "",
       "data": {
           "customerMobile": "18500167077",
           "areaList": [
               {
                   "code": "100000",
                   "name": "中国",
                   "selected":"1"
               },
               {
                   "code": "100001",
                   "name": "美国",
                   "selected":"0"
               }
           ]
       }
   }
   ```

       **返回字段说明**

| 参数名 | 参数类型 | 参数说明 |
| :--- | :--- | :--- |
| customerMobile | String | 手机号码 |
| areaList | List&lt;areaVo&gt; | 地区列表 |

     **其它说明**

     选中返回1，否则返回0







