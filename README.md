# Clash-relay-docker
内置 Clash 同时支持 `relay` 模式转发的 Docker 镜像构建脚本

## 构建
```bash
docker build -t rabbir/clash-relay:latest . --no-cache
```

## 启动
```bash
docker run -d --restart always \
  -p 1080:7893 \
  -e RAB_SOCKS5_USERNAME=test \
  -e RAB_SOCKS5_PASSWORD=test \
  -e RAB_CLASH_RELAY_NODE_INFO="{name: relay_node, type: trojan, server: github.com, port: 443, password: my_password }" \
  -e RAB_CLASH_NODE_INFO="{name: node, type: trojan, server: github.com, port: 443, password: my_password }" \
  --name clash_relay \
  rabbir/clash-relay:latest
```
> **注意：** 节点 `name` 字段的值一定要为 `relay_node` 和 `node`。

## 测试
```bash
curl -x socks5://test:test@127.0.0.1:1080 ip.sb
```