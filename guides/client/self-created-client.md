---
sidebarDepth: 2
---

# 自定义客户端

> 在不了解API定义的情况下调用未公布的API可能会造成严重后果。 请不要滥用<auth_token>。

用户可以使用自己熟悉的语言开发客户端与MaxCloud集成， 可以按一下步骤进行操作：
1. 登陆及切换到目标组
2. 调用的API

## 1. 登陆及切换到目标组

### 登陆

```
curl --location --request POST 'https://maxcloud-api.spotmaxtech.com/api/login' \
--header 'User-Agent: apifox/1.0.0 (https://www.apifox.cn)' \
--header 'Content-Type: application/json' \
--data-raw '{
    "email":"<email>",
    "password":"<password>"
}'
```

输出示例

```
{
  "status": 200,
  "request_id": "5cadf7f6a9314d3ca24172114614e543",
  "message": "success",
  "data": {
    "id": 88,
    "group_admin": 1,
    "admin": 2,
    "change_password": 0,
    "token": "<auth_token>",
    "email": "<email>",
    "company": {
      "id": 1,
      "name": "DefaultTeam",
      "created_at": "2011-10-09 12:01:34"
    },
    "all_company": [
      {
        "id": 1,
        "name": "DefaultTeam",
        "created_at": "2011-10-09 12:01:34"
      },
      {
        "id": 2,
        "name": "AnotherTeam",
        "created_at": "2011-10-09 12:01:34"
      }
    ]
  },
  "time": 1684311747
}
```
保存<auth_token>，可以调用其他API时使用。 

### 切换到AnotherTeam组
如果需要操作的资源不在当前默认组DefaultTeam， 需要切换到资源所在的组, 获得操作资源的<auth_token2>

```
curl --location --request POST 'https://maxcloud-api.spotmaxtech.com/api/company/switch' \
--header 'authorization: <auth_token>' \
--header 'User-Agent: apifox/1.0.0 (https://www.apifox.cn)' \
--header 'Content-Type: application/json' \
--data-raw '{
    "company_id": 2
}'
```

输出示例

```
{
    "status": 200,
    "request_id": "17989b6c9f8947c9b592506480b0048c",
    "message": "success",
    "data": {
        "token": "<auth_token2>",
        "email": "<email>",
        "company": {
            "id": 2,
            "name": "AnotherTeam",
            "created_at": "2011-10-09 16:11:31"
        },
        "all_company": [
            {
                "id": 1,
                "name": "DefaultTeam",
                "created_at": "2011-10-09 12:01:34"
            },
            {
                "id": 2,
                "name": "AnotherTeam",
                "created_at": "2011-10-09 12:01:34"
            }
        ]
    },
    "time": 1684312261
}
```

## 2. 调用的API

目前可以调用的API如下

### 获取Ticket列表
```
curl 'https://maxcloud-api.spotmaxtech.com/api/tickets/search' \
  -H 'authority: maxcloud-api.spotmaxtech.com' \
  -H 'accept: application/json, text/plain, */*' \
  -H 'authorization: <auth_token2>' \
  -H 'user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/115.0.0.0 Safari/537.36' \
  --data-raw '{"start_time":1577808000000,"page_size":1,"page":1,"end_time":1693818887635,"query":""}' \
```

输出示例
```
{
    "status": 200,
    "err_code": 0,
    "message": "success",
    "data": {
        "total": 118,
        "page_size": 1,
        "page": 1,
        "tickets": [
            {
                "id": 101,
                "company_id": 1,
                "team_id": 1,
                "team_name": "",
                "created_by": "<email>",
                "assigned_to": "<email>",
                "updated_by": "<email>",
                "state": "open",
                "priority": 2,
                "root_cause": "",
                "subject": "pod event warn 需要解决",
                "content_type": "",
                "content": "",
                "comment_count": 5,
                "notification_list": [
                    "<email>"
                ],
                "created_at": "2023-05-11 16:34:54",
                "updated_at": "2023-05-11 16:37:43",
                "resources": null,
                "tips": ""
            },
            ... more tickets ...
        ],
        "search_scope": "0:company"
    },
    "time": 1684312548
}
```

### 查找BU是mtg的Ticket列表
```
curl 'https://maxcloud-api.spotmaxtech.com/api/tickets/search' \
  -H 'accept: application/json, text/plain, */*' \
  -H 'accept-language: zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7' \
  -H 'authorization: <auth_token2>' \
  -H 'user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/115.0.0.0 Safari/537.36' \
  --data-raw '{"page":1,"page_size":30,"start_time":1577808000000,"end_time":1693818887594,"query":"group_tag:mtg AND state:open"}' \
  --compressed
```

输出示例
```
{
    "status": 200,
    "err_code": 0,
    "message": "success",
    "data": {
        "total": 118,
        "page_size": 1,
        "page": 1,
        "tickets": [
            {
                "id": 101,
                "company_id": 1,
                "team_id": 1,
                "team_name": "",
                "created_by": "<email>",
                "assigned_to": "<email>",
                "updated_by": "<email>",
                "state": "open",
                "priority": 2,
                "root_cause": "",
                "subject": "pod event warn 需要解决",
                "content_type": "",
                "content": "",
                "comment_count": 5,
                "notification_list": [
                    "<email>"
                ],
                "created_at": "2023-05-11 16:34:54",
                "updated_at": "2023-05-11 16:37:43",
                "resources": null,
                "tips": ""
            },
            ... more tickets ...
        ],
        "search_scope": "0:company"
    },
    "time": 1684312548
}
```

### 查找BU是‘mgt’、标签是‘日志bug’的Ticket列表
```
curl 'https://maxcloud-api.spotmaxtech.com/api/tickets/search' \
  -H 'accept: application/json, text/plain, */*' \
  -H 'accept-language: zh-CN,zh;q=0.9,en-US;q=0.8,en;q=0.7' \
  -H 'authorization: <auth_token2>' \
  -H 'user-agent: Mozilla/5.0 (Macintosh; Intel Mac OS X 10_15_7) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/115.0.0.0 Safari/537.36' \
  --data-raw '{"page":1,"page_size":30,"start_time":1577808000000,"end_time":1693818887594,"query":"group_tag:mtg AND labels:日志bug AND state:open"}' \
  --compressed
```

输出示例
```
{
    "status": 200,
    "err_code": 0,
    "message": "success",
    "data": {
        "total": 118,
        "page_size": 1,
        "page": 1,
        "tickets": [
            {
                "id": 101,
                "company_id": 1,
                "team_id": 1,
                "team_name": "",
                "created_by": "<email>",
                "assigned_to": "<email>",
                "updated_by": "<email>",
                "state": "open",
                "priority": 2,
                "root_cause": "",
                "subject": "pod event warn 需要解决",
                "content_type": "",
                "content": "",
                "comment_count": 5,
                "notification_list": [
                    "<email>"
                ],
                "created_at": "2023-05-11 16:34:54",
                "updated_at": "2023-05-11 16:37:43",
                "resources": null,
                "tips": ""
            },
            ... more tickets ...
        ],
        "search_scope": "0:company"
    },
    "time": 1684312548
}
```
