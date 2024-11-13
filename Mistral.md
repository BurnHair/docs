# 接口地址

`https://api.burn.hair/v1/chat/completions`

# 接口列表
建议选择 `mistral-large-2402` 性能最强
```
ministral-3b-2410
ministral-3b-latest
ministral-8b-2410
ministral-8b-latest
open-mistral-7b
mistral-tiny
mistral-tiny-2312
open-mistral-nemo
open-mistral-nemo-2407
mistral-tiny-2407
mistral-tiny-latest
open-mixtral-8x7b
mistral-small
mistral-small-2312
open-mixtral-8x22b
open-mixtral-8x22b-2404
mistral-small-2402
mistral-small-2409
mistral-small-latest
mistral-medium-2312
mistral-medium
mistral-medium-latest
mistral-large-2402
mistral-large-2407
mistral-large-latest
codestral-2405
codestral-latest
codestral-mamba-2407
open-codestral-mamba
codestral-mamba-latest
pixtral-12b-2409
pixtral-12b
pixtral-12b-latest
mistral-embed
```

# 请求方式
与 GPT 一样，替换模型名称即可
* POST `https://burn.hair/v1/chat/completions`

* 请求头 `Authorization: Bearer sk-xxxx`

* 请求体
  
```json
{
    "model": "mistral-large-latest",
    "messages": [
        {
            "role": "user",
            "content": "hello world"
        }
    ],
    "temperature": 0.7
}
```

# lobechat
<img width="714" alt="iShot_2024-11-13_19 15 57" src="https://github.com/user-attachments/assets/0341ce81-d28d-431c-837b-b1b75b12a740">

