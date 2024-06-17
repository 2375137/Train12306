# API文档
## 1. 用户登录
### 路径
`/login/<name>`
### 方法
`GET`, `POST`
### 功能描述
根据不同的用户类型进行登录验证。
### 参数
- `name`: 用户类型，支持`12306`和`owner`。
### 返回
- 当`name`为`12306`时，调用`Login.route`方法进行登录处理。
- 当`name`为`owner`时，使用`Owner`类进行登录验证。如果验证成功，返回包含`code`和`data`的响应，其中`code`为`0`表示登录成功，`data`包含验证信息但不包括`token`。如果验证失败，返回错误信息。
- 如果`name`不是上述两种类型，返回错误信息，`code`为`-1`，`msg`为`login type error`。
## 2. 查询
### 路径
`/search`
### 方法
`GET`, `POST`
### 功能描述
根据不同的查询类型，提供车站大屏信息、车站信息、车票信息、个人车票查询以及订单查询服务。
### 参数
- `type`: 查询类型，支持`StationScreen`、`Station`、`ticket`、`MyQuery`和`Order`。
- 根据不同的`type`，需要提供不同的附加参数。
### 返回
- 当`type`为`StationScreen`时，需要提供`station`和可选的`flag`参数。如果车站代码有效，返回车站大屏信息，否则返回错误信息。
- 当`type`为`Station`时，需要提供`station_type`和`station`参数。如果参数正确，返回车站信息，否则返回错误信息。
- 当`type`为`ticket`时，需要提供`begin`、`end`和`date`参数。如果参数正确，返回车票信息，否则返回错误信息。
- 当`type`为`MyQuery`时，需要提供`operation`参数，以及根据操作类型可能需要的其他参数。根据操作类型返回个人车票查询结果或验证信息。
- 当`type`为`Order`时，需要提供`index`、`start_date`、`end_date`和`status`参数。返回订单查询结果。
- 如果`type`不是上述支持的类型，返回错误信息。
请注意，这里的API描述是基于您提供的代码片段，并且假设`Station`、`StationScreen`、`SearchTicket`、`Search`、`Verify`和`Order`类中的方法有相应的实现来处理查询逻辑。实际的API行为可能需要结合完整的代码上下文来确定。

## 3. 更新车站信息
### 路径
`/update_station`
### 方法
`GET`, `POST`
### 功能描述
更新车站信息。
### 参数
无
### 返回
处理结果。
## 4. 获取favicon
### 路径
`/favicon.ico`
### 方法
`GET`, `POST`
### 功能描述
返回网站的favicon图标。
### 参数
无
### 返回
`favicon`字符串。
# 错误码说明
- `code: 0`: 操作成功。
- `code: 1`: 参数错误或操作失败。
- `code: -1`: 服务器错误或其他未知错误。
# 示例
## 用户登录示例
```text
"POST" /login/12306
```
响应:
```json
{
  "code": "0",
  "data": {
    "username": "user123",
    "session_id": "abc123"
  }
}
```
## 查询车站大屏信息示例
```text
"GET" /search?type=StationScreen&station=SHH
```
响应:
```json
{
  "code": "0",
  "data": {
    "station_name": "上海虹桥",
    "trains": [
      {
        "train_number": "G123",
        "departure_time": "12:30",
        "arrival_time": "15:00",
        "status": "准时"
      },
      {
        "train_number": "D456",
        "departure_time": "13:45",
        "arrival_time": "16:15",
        "status": "晚点"
      }
    ]
  }
}
```
## 更新车站信息示例
```text
"POST" /update_station
```
响应:
```json
{
  "code": "0",
  "msg": "Station information updated successfully."
}
```
请注意，以上示例仅用于说明API的使用方式，实际的响应内容可能会根据应用程序的状态和数据库的实际情况而有所不同。
