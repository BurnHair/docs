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

# ChatGPTNextWeb 配置
<img width="927" alt="nextweb" src="https://github.com/user-attachments/assets/5400424d-95bf-4642-b23a-1c6443b6c12e">

# LobeChat 配置
<img width="1060" alt="lobe-claude" src="https://github.com/user-attachments/assets/b678d7a6-d6ff-46c7-857e-eb04686b104e">
