使用如下测试代码即可
```python
#!/usr/bin/env python3
# coding: utf-8
import time

from openai import OpenAI
import json

client = OpenAI(api_key="sk-1234", base_url="https://burn.hair/v1")

# 定义模拟获取天气的本地函数
def get_current_weather(location, unit):
    # Call the weather API
    return f"It's 21 {unit} in {location}"


# 定义chat接口需要的函数
functions = [
    {
        "name": "get_current_weather",
        "description": "Get the current weather in a given location",
        "parameters": {
            "type": "object",
            "properties": {
                "location": {
                    "type": "string",
                    "description": "The city and state, e.g. San Francisco, CA",
                },
                "unit": {"type": "string", "enum": ["celsius", "fahrenheit"]},
            },
            "required": ["location"],
        },
    }
]

# 第一次调用chat接口，返回的是函数调用的提示
messages = [{"role": "user", "content": "What's the weather like in Boston today with celsius?"}]
completion = client.chat.completions.create(
    model="gpt-3.5-turbo",
    messages=messages,
    functions=functions,
    function_call="auto",
)


response_message = completion.choices[0].message
function_name = response_message.function_call.name
function_args = json.loads(response_message.function_call.arguments)
function_response = get_current_weather(**function_args)
messages.append(response_message)
messages.append(
    {
        "role": "function",
        "name": function_name,
        "content": function_response,
    }
)

# # 第二次调用chat接口，返回的是chat的最终结果
completion_final = client.chat.completions.create(model="gpt-3.5-turbo", messages=messages, stream=False)
print(completion_final)

```
