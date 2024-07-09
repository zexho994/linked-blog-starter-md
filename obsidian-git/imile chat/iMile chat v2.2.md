
https://testerhome.com/topics/39628

# 需求说明

| 版本   | 功能点        | 说明                                  |
| ---- | ---------- | ----------------------------------- |
| v1.0 | 基础对话       | 回答用户关于自动化平台的问题。                     |
| v1.0 | 基础检索       | 在对话的基础上，返回参考的结果，实现检索。               |
|      | 生成 mock 数据 | 根据实际代码和用例，自动一键生成 mock 数据            |
|      | 自动更新接口文档   | 当代码发生变动时，AI分析改动，来维护旧文档              |
|      | 生成测试用例     |                                     |
|      | 分析报告       |                                     |
|      | 预测         | 根据接口/用例/测试结果，发现潜在问题                 |
|      | 高级对话       | 在基础之上，融合其他系统数据，丰富回答的内容<br>结合接口的实际代码 |
|      |            |                                     |

## 功能点：
### v2.2 对话和检索




### 生成mock数据

> 没人想耗费很多时间写Mock

![[Pasted image 20240709092528.png]]

### 字段更新接口文档

> 改了代码，忘记改文档，是最容易发生得事情。


![[Pasted image 20240709093058.png]]

![[Pasted image 20240709093129.png]]

![[Pasted image 20240709093140.png]]




# 技术方案：

## itp 接口

### 获取用例列表

```json
{
  "content": [
    {
      "classificationId": 0,
      "classificationIds": [
        0
      ],
      "classificationName": "string",
      "collectUser": [
        "string"
      ],
      "containsSet": 0,
      "createTime": "2024-07-09T10:09:01.714Z",
      "createUserName": "string",
      "description": "string",
      "groupId": 0,
      "groupName": "string",
      "id": 0,
      "isEnabled": true,
      "itemCount": 0,
      "name": "string",
      "status": 0,
      "systemId": 0,
      "systemName": "string",
      "type": 0,
      "updateTime": "2024-07-09T10:09:01.714Z",
      "updateUserName": "string",
      "versionId": 0,
      "versionIds": [
        0
      ],
      "versionName": "string",
      "versionNames": [
        "string"
      ]
    }
  ],
  "empty": true,
  "first": true,
  "last": true,
  "number": 0,
  "numberOfElements": 0,
  "pageable": {
    "offset": 0,
    "pageNumber": 0,
    "pageSize": 0,
    "paged": true,
    "sort": {
      "empty": true,
      "sorted": true,
      "unsorted": true
    },
    "unpaged": true
  },
  "size": 0,
  "sort": {
    "empty": true,
    "sorted": true,
    "unsorted": true
  },
  "totalElements": 0,
  "totalPages": 0
}
```
### 获取接口列表

```json
{
  "content": [
    {
      "addType": 0,
      "appId": 0,
      "appName": "string",
      "calcTime": "2024-07-09T11:12:02.802Z",
      "classificationId": 0,
      "classificationIds": [
        0
      ],
      "classificationName": "string",
      "createTime": "2024-07-09T11:12:02.803Z",
      "createUserId": "string",
      "createUserName": "string",
      "description": "string",
      "groupId": 0,
      "groupName": "string",
      "id": 0,
      "isDeleted": true,
      "isEnabled": true,
      "name": "string",
      "relativePath": "string",
      "requestMethod": "string",
      "systemId": 0,
      "systemName": "string",
      "updateTime": "2024-07-09T11:12:02.803Z",
      "updateUserId": "string",
      "updateUserName": "string",
      "versionId": 0,
      "versionIds": [
        0
      ],
      "versionName": "string",
      "versionNames": [
        "string"
      ],
      "workFlowStatus": 0
    }
  ],
  "empty": true,
  "first": true,
  "last": true,
  "number": 0,
  "numberOfElements": 0,
  "pageable": {
    "offset": 0,
    "pageNumber": 0,
    "pageSize": 0,
    "paged": true,
    "sort": {
      "empty": true,
      "sorted": true,
      "unsorted": true
    },
    "unpaged": true
  },
  "size": 0,
  "sort": {
    "empty": true,
    "sorted": true,
    "unsorted": true
  },
  "totalElements": 0,
  "totalPages": 0
}
```
### 获取用例详情


### 获取接口详情
```json
{
  "code": "0",
  "msg": "操作成功",
  "data": {
    "createUserId": "roc",
    "createUserName": "roc",
    "createTime": "2024-06-25T09:26:27.670+0000",
    "updateUserId": "roc",
    "updateUserName": "roc",
    "updateTime": "2024-06-25T09:26:27.670+0000",
    "isDeleted": false,
    "id": 2097,
    "name": "订单详情查看- OFD",
    "description": "",
    "groupId": 1,
    "systemId": 45,
    "appId": null,
    "versionId": 0,
    "classificationIds": [
      0,
      266
    ],
    "classificationId": 266,
    "isEnabled": true,
    "branchId": 0,
    "requestMethod": "POST",
    "relativePath": "/dms/dapp/more/info/detail",
    "dataFormat": 1,
    "protobuf": {
      "requestPath": null,
      "requestMessage": null,
      "responseSuccessPath": null,
      "responseSuccessMessage": null,
      "responseFailurePath": null,
      "responseFailureMessage": null
    },
    "requestHeaders": [
      {
        "key": "Authorization",
        "value": "Bearer {{Authorization}}",
        "example": null
      },
      {
        "key": "Content-Type",
        "value": "application/x-www-form-urlencoded",
        "example": null
      },
      {
        "key": "deviceid",
        "value": "b2c624e8187420af",
        "example": null
      },
      {
        "key": "timezone",
        "value": "Asia/Riyadh",
        "example": null
      },
      {
        "key": "platform",
        "value": "android",
        "example": null
      },
      {
        "key": "appcode",
        "value": "com.scm.app.deliveryapp",
        "example": null
      },
      {
        "key": "locale",
        "value": "en_US",
        "example": null
      },
      {
        "key": "lang",
        "value": "en_US",
        "example": null
      },
      {
        "key": "client",
        "value": "DeliveryApp",
        "example": null
      }
    ],
    "requestParameters": [
      {
        "key": "taskId",
        "value": "1223232323",
        "isRequired": null,
        "example": null,
        "description": null
      }
    ],
    "requestBody": {
      "enctype": "raw",
      "raw": "{\n    'currentPage': \"1\",\n    'showCount': \"10\"\n}",
      "jsonData": null,
      "jsonList": null,
      "urlEncodedPairs": null,
      "formDataPairs": null,
      "empty": false
    },
    "responseBodyExample": {
      "format": "raw",
      "raw": null,
      "jsonData": null
    },
    "workFlowStatus": 1,
    "hasDebugDataSet": false,
    "hasPassDataSet": false,
    "addType": 0,
    "calcTime": null,
    "performance": null,
    "inCase": null,
    "versionNames": null,
    "versionName": "Master",
    "classificationNames": [
      "我的接口",
      "Tasks"
    ]
  }
}
```

## 设计 Es 索引

### 接口信息


### 用例信息



## 设计查询模式


## 数据全量同步

通过API接口主动，实现加载器

## 增量同步
回调接口，实现更新接口

## 调试 Prompt


## 测试问答效果








# 流程图
![[iMile  chat 对接 自动化测试]]