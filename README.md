# 问题反馈

* 在[讨论区](https://github.com/orgs/BurnHair/discussions)中可以进行问题反馈
* 文档持续更新中，请点击md文件查看具体使用方法

# 接口地址

* 全球可用：`https://burn.hair`
* 中国加速（测试阶段）：`https://cn-test.burn.hair`

# 1. 内部接口文档

## 1.1 获取用户统计信息

* 需要系统访问令牌：设置-生成系统访问令牌
* GET `https://burn.hair/api/user/stat`
* 请求头 `Authorization: Bearer sk-xxxx`

```json
{
    "token": [
        {
            "key": "sk-YZ1213466d",
            "status": "enabled",
            "name": "status",
            "created_time": "2024-05-07 19:05:58",
            "accessed_time": "2024-06-24 16:00:33",
            "expired_time": "never",
            "remain_quota": 2171914,
            "remain_quota_dollar": 4.343828,
            "unlimited_quota": true,
            "used_quota": 2828086,
            "used_quota_dollar": 5.656172
        },
        {
            "key": "sk-bNd123475a",
            "status": "enabled",
            "name": "鸭梨",
            "created_time": "2024-03-23 18:43:10",
            "accessed_time": "2024-07-06 13:11:56",
            "expired_time": "never",
            "remain_quota": -6319582,
            "remain_quota_dollar": -12.639164,
            "unlimited_quota": true,
            "used_quota": 946792,
            "used_quota_dollar": 1.893584
        }
    ],
    "user": {
        "free_quota": 827272,
        "free_quota_dollar": 1.654544,
        "bonus_quota": 19827263,
        "bonus_quota_dollar": 39.65453,
        "paid_quota": 37479605,
        "paid_quota_dollar": 74.959206,
        "total_quota": 58134140,
        "total_quota_dollar": 116.26828,
        "used_quota": 967381,
        "used_quota_dollar": 1.934762,
        "request_count": 108359
    }
}
```

# 2. Open AI 接口文档

## 2.1 获取支持的模型列表

* GET `https://burn.hair/v1/models`
* 请求头 `Authorization: Bearer sk-xxxx`

```json
{
  "data": [
    {
      "id": "gpt-3.5-turbo",
      "object": "model",
      "created": 0,
      "owned_by": "system"
    },
    {
      "id": "gpt-4-32k-0613",
      "object": "model",
      "created": 0,
      "owned_by": "system"
    }
  ],
  "object": "list"
}
```

## 2.2 Chat Competions

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

## 2.3 whisper

* POST `https://burn.hair/v1/audio/transcriptions`

* 请求头 `Authorization: Bearer sk-xxxx`

* 请求体 `form-data`，两个字段 `model: whisper-1`，`file: 你的音频文件路径`

```json
{
  "text": "so that they know it's a better world for them."
}
```

## 2.4 TTS

* POST `https://burn.hair/v1/audio/speech`

* 请求头 `Authorization: Bearer sk-xxxx`

* 请求体为json，会返回一个音频文件供下载
* model 选择 `tts-az-1`
  时，[voice 的值请参考文档](https://learn.microsoft.com/en-us/azure/ai-services/speech-service/language-support?tabs=tts)
  ，推荐 `zh-CN-XiaoxiaoMultilingualNeural`

```json
{
  "model": "tts-1",
  "input": "Hello world",
  "voice": "alloy"
}
```

## 2.5 DALL·E

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

## 2.6 embeddings

* POST `https://burn.hair/v1/embeddings`

* 请求头 `Authorization: Bearer sk-xxxx`

* 请求体为json

```json
{
  "input": "Your text string goes here",
  "model": "text-embedding-3-large"
}
```

## 2.7 gpt-3.5-turbo-instruct

注意 instruct 的请求接口和格式与 Chat Completions不同

* POST `https://burn.hair/v1/completions`
* 请求头 `Authorization: Bearer sk-xxxx`

* 请求体为json

```json
{
  "model": "gpt-3.5-turbo-instruct",
  "prompt": "Say this is a test",
  "max_tokens": 7,
  "temperature": 0
}
```

## 2.8 Batch

**暂时不可用**

批量处理是异步的，适合对实时性要求不高的任务。有如下限制：

* 上传的文件会在1小时内过期，并且为了避免滥用限制每个文件最多 10M
* 任务信息会保留24小时，任务通常会在2小时内完成
* 任务完成后，下载文件会在3小时内过期，请及时下载

具体请求方法如下，Authorization不再赘述

### 2.8.1 上传文件

* POST https://burn.hair/v1/files
* form data，两个字段
* `purpose: batch`
* `file: 你的文件路径`，格式为 jsonl，如下

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

### 2.8.2 提交处理

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

### 2.8.3 查看处理状态

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

`status` 字段会表示请求状态，`in_progress` 为处理中，`complete` 为处理完成；如果处理完成，那么 `output_file_id` 字段也会提供一个
ID

### 2.8.4 获取处理结果

* GET https://burn.hair/v1/files/file-OfYicuFI9l0E6hL300HwutypCiM/content

系统会返回 `application/octet-stream` 的jsonl文件，文本内容如下

```jsonl
{"id":"batch_SVrZ7umUwFGq06i-wFXym07Ad4U","custom_id":"123a","response":{"status_code":200,"request_id":"req_1ab16c70fcf311eea2910242ac120009","body":{"choices":[{"finish_reason":"stop","index":0,"logprobs":null,"message":{"content":"我，V，谨庄严宣誓。","role":"assistant"}}],"created":1713383154,"id":"chatcmpl-9F5W6CqNoAA7Qgc1ZyGS0LSIGG0UC","model":"gpt-35-turbo","object":"chat.completion","system_fingerprint":null,"usage":{"completion_tokens":15,"prompt_tokens":29,"total_tokens":44}}},"error":null}
{"id":"batch_SVrZ7umUwFGq06i-wFXym07Ad4U","custom_id":"124a","response":{"status_code":200,"request_id":"req_1b795c4ffcf311eea2910242ac120009","body":{"choices":[{"finish_reason":"stop","index":0,"logprobs":null,"message":{"content":"我是一个开发的语言模型，我没有实体身份。我工作的目标是回答用户的问题和提供相关的信息。有什么我可以帮助你的吗？","role":"assistant"}}],"created":1713383155,"id":"chatcmpl-9F5W728FkYlTqgO9JLLsWmXhudP9Q","model":"gpt-35-turbo","object":"chat.completion","system_fingerprint":null,"usage":{"completion_tokens":53,"prompt_tokens":12,"total_tokens":65}}},"error":null}

```

