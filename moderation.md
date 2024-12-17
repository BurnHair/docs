本站支持 moderation
* POST https://burn.hair/v1/moderations
* POST https://api.burn.hair/v1/moderations

可用模型如下
omni-moderation-latest,omni-moderation-2024-09-26,text-moderation-latest,text-moderation-stable,text-moderation-007

Bearer token 方式认证


```json
{
    "model": "omni-moderation-latest",
    "input": "消费日志更新略有延迟，30 天后自动删除；鼠标悬停“模型”列显示价格详情。"
}
```
