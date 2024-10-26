# 1. 安装 docker
请参考 docker 的[官方文档](https://docs.docker.com/get-docker/)

# 2. 准备文件
保存如下内容为 `docker-compose.yml`
```yml
version: "3"

services:
  lobe-chat:
    image: lobehub/lobe-chat
    restart: always
    environment:
      - OPENAI_MODEL_LIST=-all,+gpt-3.5-turbo,+gpt-3.5-turbo-0613,+gpt-3.5-turbo-16k,+gpt-3.5-turbo-16k-0613,+gpt-3.5-turbo-1106,+gpt-4-0125-preview,+gpt-4-turbo-preview,+gpt-4-1106-preview,+gpt-4-vision-preview,+gpt-4-0613,+gpt-4,+gpt-4-32k,+gpt-4-32k-0613,+gpt-3.5-turbo-0125,gpt-4-turbo-2024-04-09,gpt-4o,gpt-4o-2024-05-13
      - OPENAI_PROXY_URL=https://burn.hair/v1
    ports:
      - "127.0.0.1:3210:3210"

  chatgpt-next-web:
    image: yidadaa/chatgpt-next-web
    restart: always
    environment:
      - BASE_URL=https://burn.hair/
      - CUSTOM_MODELS=-all,+gpt-3.5-turbo,+gpt-3.5-turbo-0613,+gpt-3.5-turbo-16k,+gpt-3.5-turbo-16k-0613,+gpt-3.5-turbo-1106,+gpt-4-0125-preview,+gpt-4-turbo-preview,+gpt-4-1106-preview,+gpt-4-vision-preview,+gpt-4-0613,+gpt-4,+gpt-4-32k,+gpt-4-32k-0613,+gpt-3.5-turbo-0125,gpt-4-turbo-2024-04-09,gpt-4o,gpt-4o-2024-05-13
    ports:
      - "127.0.0.1:3000:3000"

  watchtower:
    image: containrrr/watchtower
    restart: always
    volumes:
      - /var/run/docker.sock:/var/run/docker.sock

```

# 3. 运行
```bash
docker-compose up -d
```

# 4. 访问
打开浏览器，访问 `http://localhost:3000` 或 `http://localhost:3210` ，填入你的 API Key 即可开始使用
