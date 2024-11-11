# 1. 内部接口文档

## 1.1 获取用户统计信息
时间是UTC时间。
* 需要系统访问令牌：设置-生成系统访问令牌
* GET `https://burn.hair/api/user/stat`
* 请求头 `Authorization: Bearer abcd`

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
