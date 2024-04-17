# 1. Open AI 接口
## Chat Competions
* 接口 `https://burn.hair/v1/chat/completions`

* 请求头 `Authorization: Bearer sk-xxxx`

* 请求体

```json
{
  "model": "gpt-3.5-turbo",
  "messages": [
    {
      "role": "user",
      "content": "重复我说的话：我，V，谨庄严宣誓。"
    }
  ],
  "temperature": 0.7
}
```
<img src="https://assets.burn.hair/postman.png" width="100%" />

请根据个人需要更换其他模型。

## whisper
* 接口 `https://burn.hair/v1/audio/transcriptions`

* 请求头 `Authorization: Bearer sk-xxxx`

* 请求体 是form-data，两个字段 model: whisper-1，file: 你的音频文件


## TTS
* 接口 `https://burn.hair/v1/audio/speech`

* 请求头 `Authorization: Bearer sk-xxxx`

* 请求体为json，会返回一个音频文件供下载
```json
{
    "model": "tts-1",
    "input": "Hello world",
    "voice": "alloy"
}
```

## DALL·E
* 接口 `https://burn.hair/v1/images/generations`

* 请求头 `Authorization: Bearer sk-xxxx`

* 请求体为json
```json
{
    "model": "dall-e-3",
    "prompt": "a white siamese cat",
    "n": 1,
    "size": "1024x1024"
}
```

# 2. 支持 Claude 吗
暂时不支持...
* `https://burn.hair/v1/completions`
* `Authorization: Bearer sk-...`

```json
{
    "model": "claude-3-opus-20240229",
    "max_tokens": 1024,
    "messages": [
        {"role": "user", "content": "Hello, world"}
    ]
}

{
    "id": "msg_01QoZJu2xEKgbyqYMXKbEbSD",
    "type": "message",
    "role": "assistant",
    "content": [
        {
            "type": "text",
            "text": "Hello!"
        }
    ],
    "model": "claude-2.1",
    "stop_reason": "end_turn",
    "stop_sequence": null,
    "usage": {
        "input_tokens": 12,
        "output_tokens": 6
    }
}

```
