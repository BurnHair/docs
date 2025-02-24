# 接口地址

`https://api.burn.hair`  或 `https://burn.hair/`

小分队提供两种类型的 Claude 接口

* default：第三方接口
* VIP： Anthropic Claude 官方接口

令牌 - 编辑 - 令牌分组，可以随意切换



## ChatGPTNextWeb
<img width="927" alt="nextweb" src="https://github.com/user-attachments/assets/5400424d-95bf-4642-b23a-1c6443b6c12e">

## LobeChat
<img width="1060" alt="lobe-claude" src="https://github.com/user-attachments/assets/b678d7a6-d6ff-46c7-857e-eb04686b104e">

_________________

下面是API 接口，Claude的接口有两种格式，请根据自己的需求进行选择

# Claude 格式

## 请求方式
* 网址 `https://api.burn.hair/v1/messages` ，或 `https://burn.hair/v1/messages`
* 请求头: `x-api-key: 本站的令牌`
* 请求体
```json
{
    "model": "claude-3-haiku-20240307",
    "max_tokens": 1024,
    "messages": [
        {
            "role": "user",
            "content": "Hello, world"
        }
    ]
}
```

对于支持深度思考的模型，如 `claude-3-7-sonnet-20250219`，请求体如下，思考token要小于最大token。详情[可见官方文档](https://docs.anthropic.com/en/docs/build-with-claude/extended-thinking)
```json
{
    "model": "claude-3-7-sonnet-20250219",
    "max_tokens": 10240,
    "thinking": {
        "type": "enabled",
        "budget_tokens": 3000
    },
    "messages": [
        {
            "role": "user",
            "content": "hello"
        }
    ]
}

```
## 响应
```json
{
    "id": "msg_01SVN2qDfHPQQnv1yV5HNHHS",
    "type": "message",
    "role": "assistant",
    "model": "claude-3-haiku-20240307",
    "content": [
        {
            "type": "text",
            "text": "Hello! I'm an AI assistant created by Anthropic. It's nice to meet you. How can I assist you today?"
        }
    ],
    "stop_reason": "end_turn",
    "stop_sequence": null,
    "usage": {
        "input_tokens": 10,
        "output_tokens": 30
    }
}
```

# OpenAI 兼容格式
## 请求方式
* 网址：`https://api.burn.hair/v1/chat/completions`
* 请求头： `Authorization: Bearer 本站令牌`
* 请求体：
```json
{
    "model": "claude-3-haiku-20240307",
    "max_tokens": 1024,
    "messages": [
        {
            "role": "user",
            "content": "Hello, world"
        }
    ]
}
```
## 响应
```json
{
    "id": "msg_01VXmrACmtER7tDZNQoUxCey",
    "model": "claude-3-haiku-20240307",
    "object": "chat.completion",
    "created": 1730633726,
    "choices": [
        {
            "index": 0,
            "message": {
                "role": "assistant",
                "content": "Hello! It's nice to meet you."
            },
            "finish_reason": "stop"
        }
    ],
    "usage": {
        "prompt_tokens": 10,
        "completion_tokens": 16,
        "total_tokens": 26
    }
}
```

# 流式请求
```python
import anthropic

key = "sk-225mYe"

baseurl = "https://api.burn.hair/v1/messages"
client = anthropic.Anthropic(base_url=baseurl, api_key=key)

with client.messages.stream(
    max_tokens=1024, messages=[{"role": "user", "content": "hi"}], model="claude-3-haiku-20240307"
) as stream:
    for text in stream.text_stream:
        print(text, end="", flush=True)
```
