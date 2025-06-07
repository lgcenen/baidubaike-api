# 百度百科-api
一个非官方的百度百科api库。

## 编辑器AI智能检测
*下列代码请求链接为：https://baike.baidu.com/*
### 接口基本信息

| 项目          | 说明                          |
|---------------|-----------------------------|
| 接口地址       | `/editor/helper/intercept`   |
| 请求方法       | `POST`                      |
| 内容类型       | `application/x-www-form-urlencoded; charset=UTF-8` |
| 认证方式       | Cookie 认证                  |

### 请求说明

#### 请求头 (Headers)
```http
POST /editor/helper/intercept HTTP/1.1
Host: baike.baidu.com
User-Agent: Mozilla/5.0
Accept: application/json
Content-Type: application/x-www-form-urlencoded
X-Requested-With: XMLHttpRequest
Cookie: BAIDUID=xxx; BDUSS=xxx
Referer: https://baike.baidu.com/editor/
```

### 响应说明

#### 成功响应

```
{
  "errno": 0,
  "errmsg": "",
  "data": {
    "warning": [],
    "notice": [],
    "notice_plus": []
  }
}
```

#### 响应字段说明

| 字段路径           | 类型   | 说明                                                                 |
|--------------------|--------|----------------------------------------------------------------------|
| `errno`            | int    | 错误码（0表示成功）                                                 |
| `errmsg`           | string | 错误信息（成功时为空）                                              |
| `data.warning`     | array  | 警告级别的问题列表（需优先修改）                                     |
| `data.notice`      | array  | 提示级别的问题列表（建议修改）                                       |
| `notice[].ruleId`  | int    | 规则编号（对应后台审核规则ID）                                       |
| `notice[].partType`| int    | 问题部位类型（104=文本内容）                                         |
| `notice[].detail`  | string | 具体修改建议                                                        |

#### 常见审核规则对照表

| ruleId | 问题类型           | 修改建议                                                                 |
|--------|--------------------|--------------------------------------------------------------------------|
| 96     | 时效性年龄描述     | 删除或更新会随时间变化的年龄信息（如"今年25岁"改为"出生于1999年"）         |
| 102    | 主观评价用语       | 删除"最好的"、"最著名的"等非客观描述                                      |
| 205    | 广告嫌疑内容       | 移除电话号码、网址等推广信息                                              |
