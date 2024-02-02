# DuckAGI API接口

#### 说明
1、DuckAGI自有的接口，区别于openai的接口，一般用来操作和查询DuckAGI账户相关，比如查询余额等 <br>

- **注意事项**   
注意事项！！ 
``` 
现在主要发现是有3个问题，  
1、要加一个请求头，api接口文档中有说明：
curl -H "Content-Type: application/json" -H "Authorization: Bearer $api_secret_key" -XPOST https://api.duckagi.com/v1/chat/completions -d '{"messages": [{"role":"user","content":"请介绍一下你自己"}]}'  | iconv -f utf-8 -t utf-8  
2、messages传的不对，messages是array
3、api_secret_key传的不对，不能再传openai的key了，你要传你从DuckAGI拿到的key（不需要有openai的key）       
```
注：<br>
1、以下所有接口的base_url: `https://api.duckagi.com/` （支持https）<br>
2、API通过HTTP请求调用。每次请求，需要在HTTP头中携带用户的api_secret_key，用于认证。 开发者单独的api_secret_key，请从智增增管理后台获得。 
请求头形如：  
```
Content-Type: application/json
Authorization: Bearer $api_secret_key
```

#### 1、模型相关     

获取模型相关信息。    

- **请求URL**
> `v1/models`

- **请求方式** 
>**POST**

- **Header参数**
>
| 名称      |     值 | 
| :-------- | :--------|
| Content-Type| application/json| 
| Authorization| Bearer $api_secret_key|  

- **请求参数**
>
| 请求参数      |     参数类型 |   是否必须   |参数说明   |
| :-------- | :--------| :------ | :------ |   


- **请求示例**
>    
```
import http.client

conn = http.client.HTTPSConnection("api.duckagi.com")
payload = ''
headers = {
   'Authorization': 'Bearer {{YOUR_API_KEY}}',
   'User-Agent': 'Apifox/1.0.0 (https://apifox.com)'
}
conn.request("GET", "/v1/models", payload, headers)
res = conn.getresponse()
data = res.read()
print(data.decode("utf-8"))

```

- **返回示例**
>    
```
{
  "data": [
    {
      "id": "model-id-0",
      "object": "model",
      "owned_by": "organization-owner",
      "permission": [...]
    },
    {
      "id": "model-id-1",
      "object": "model",
      "owned_by": "organization-owner",
      "permission": [...]
    },
    {
      "id": "model-id-2",
      "object": "model",
      "owned_by": "openai",
      "permission": [...]
    }
  ],
  "object": "list"
}

```
