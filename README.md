# CQ码工具

可以完成CQ字符串与消息段数组之间的互相转换

## 安装

```shell
cargo add cqtool
cargo add serde_json
```

## 使用

### 将消息转为消息段数组格式

```rust
let cqstr = "你好[CQ:at,qq=123456]";
let cqjson:serde_json::Value = cqtool::to_arr_msg(cqstr).unwrap();
println!("{}",serde_json::to_string_pretty(&cqjson).unwrap());
```

输出：

```
[
  {
    "data": {
      "text": "你好"
    },
    "type": "text"
  },
  {
    "data": {
      "qq": "123456"
    },
    "type": "at"
  }
]
```

### 将消息转为CQ字符串格式

```rust
let json_arr:serde_json::Value = serde_json::json!([{"data": {"text": "你好"},"type": "text"},{"data": {"qq": "123456"},"type": "at"}]);
let cqstr = cqtool::to_str_msg(&json_arr).unwrap();
println!("{}", cqstr);
```

输出：

```
你好[CQ:at,qq=123456]
```


### 构造CQ码参数

```rust
let cqstr = format!("你好[CQ:at,qq={}]",cqtool::cq_params_encode("123456"));
println!("{}",cqstr);
```

输出：

```
你好[CQ:at,qq=123456]
```

### 构造CQ文本

```rust
let cqstr = format!("{}[CQ:at,qq=123456]",cqtool::cq_text_encode("你好"));
println!("{}",cqstr);
```
输出：

```
你好[CQ:at,qq=123456]
```
