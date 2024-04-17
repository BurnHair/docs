# 1. Open AI 接口
## 1.1 Chat Competions
* POST `https://burn.hair/v1/chat/completions`

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

## 1.2 whisper
* POST `https://burn.hair/v1/audio/transcriptions`

* 请求头 `Authorization: Bearer sk-xxxx`

* 请求体 是form-data，两个字段 model: whisper-1，file: 你的音频文件


## 1.3 TTS
* POST `https://burn.hair/v1/audio/speech`

* 请求头 `Authorization: Bearer sk-xxxx`

* 请求体为json，会返回一个音频文件供下载
```json
{
    "model": "tts-1",
    "input": "Hello world",
    "voice": "alloy"
}
```

## 1.4 DALL·E
* POST `https://burn.hair/v1/images/generations`

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

## 1.5 Batch
批量处理是异步的，适合对实时性要求不高的任务。有如下限制：
* 上传的文件会在1小时内过期，并且为了避免滥用限制每个文件最多 10M
* 任务信息会保留24小时，任务通常会在2小时内完成
* 任务完成后，下载文件会在3小时内过期，请及时下载

具体请求方法如下，Authorization不再赘述

### 1.5.1. 上传文件
* POST https://burn.hair/v1/files
* form data
* purpose: batch
* file: 你的文件，格式为 jsonl，如下

```jsonl
{"custom_id":"123a","method":"POST","body":{"model":"gpt-3.5-turbo","messages":[{"role":"user","content":"重复我说的话：我，V，谨庄严宣誓。"}]},"url":"/v1/chat/completions"}
{"custom_id":"124a","method":"POST","body":{"model":"gpt-3.5-turbo","messages":[{"role":"user","content":"你是谁？"}]},"url":"/v1/chat/completions"}
```
一行一个请求，`custom_id` 是你用户后续追踪的ID，`method` 和 `url` 固定，`body` 是原来请求的全部内容

系统会返回如下内容
```json
{
    "bytes": 342,
    "created_at": 1713379306,
    "filename": "batch.jsonl",
    "id": "file-Q_XY9ZNevGHVq2XgcY0ec0strLQ",
    "object": "file",
    "purpose": "batch",
    "status": "processed",
    "status_details": null
}
```

### 1.5.2. 提交处理
* POST https://burn.hair/v1/batches
使用上一步的 `id`

```json
{
    "input_file_id": "file-yfJuOskphlGSTv_Z-D6wsdcd4Sc",
    "endpoint": "/v1/chat/completions",
    "completion_window": "24h"
  }
```
返回内容
```json
{
    "cancelled_at": null,
    "cancelling_at": null,
    "completed_at": null,
    "completion_window": "24h",
    "created_at": 1713379397,
    "endpoint": "/v1/completions",
    "error_file_id": null,
    "errors": null,
    "expired_at": null,
    "expires_at": null,
    "failed_at": null,
    "finalizing_at": null,
    "id": "batch_BplYziO3U0wFK895QfgwUmmJ3YQ",
    "in_progress_at": null,
    "input_file_id": "file-yfJuOskphlGSTv_Z-D6wsdcd4Sc",
    "metadata": {
        "batch_description": "",
        "customer_id": ""
    },
    "object": "batch",
    "output_file_id": null,
    "request_counts": {
        "completed": 0,
        "failed": 0,
        "total": 0
    },
    "status": "validating"
}
```

### 1.5.3. 查看处理状态
* GET https://burn.hair/v1/batches/batch_BplYziO3U0wFK895QfgwUmmJ3YQ
使用上一步得到的 `id`
返回内容
```json
{
    "id": "batch_BplYziO3U0wFK895QfgwUmmJ3YQ",
    "object": "batch",
    "endpoint": "/v1/completions",
    "errors": null,
    "input_file_id": "file-yfJuOskphlGSTv_Z-D6wsdcd4Sc",
    "completion_window": "24h",
    "status": "validating",
    "output_file_id": null,
    "error_file_id": null,
    "created_at": 1713379397,
    "in_progress_at": null,
    "expires_at": 0,
    "finalizing_at": null,
    "completed_at": null,
    "failed_at": null,
    "expired_at": null,
    "cancelling_at": null,
    "cancelled_at": null,
    "request_counts": {
        "total": 0,
        "completed": 0,
        "failed": 0
    },
    "metadata": {
        "batch_description": "",
        "customer_id": ""
    }
}
```

`status` 字段会表示请求状态，`in_progress` 为处理中，`complete` 为处理完成；如果处理完成，那么 `output_file_id` 字段也会提供一个 ID

### 1.5.4. 获取处理结果
* GET https://burn.hair/v1/files/file-OfYicuFI9l0E6hL300HwutypCiM/content

系统会返回 `application/octet-stream` 的jsonl文件，文本内容如下
```jsonl
{"choices":[{"finish_reason":"stop","index":0,"logprobs":null,"message":{"content":"我，V，谨庄严宣誓。","role":"assistant"}}],"created":1713379484,"id":"chatcmpl-9F4Yu13YkDF4tsxVGyIb5vwBiYoHs","model":"gpt-35-turbo","object":"chat.completion","system_fingerprint":null,"usage":{"completion_tokens":15,"prompt_tokens":29,"total_tokens":44}}
{"choices":[{"finish_reason":"stop","index":0,"logprobs":null,"message":{"content":"我是一个AI助手，由OpenAI开发。我的目标是提供有关各种主题的实用信息和帮助。","role":"assistant"}}],"created":1713379485,"id":"chatcmpl-9F4Yv3decY7CEqLlKxrPq7LKWo13k","model":"gpt-35-turbo","object":"chat.completion","system_fingerprint":null,"usage":{"completion_tokens":37,"prompt_tokens":12,"total_tokens":49}}
```

# 2. 支持 Claude 吗
暂时不支持...
* POST `https://burn.hair/v1/completions`
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
