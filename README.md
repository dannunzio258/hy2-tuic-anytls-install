# HY2 + TUIC5 + AnyTLS 一键安装脚本

适用于 Debian 12 和 Alpine 的 sing-box 一键脚本，支持同时搭建：

- Hysteria2
- TUIC v5
- AnyTLS

脚本使用单个 sing-box 进程运行三种协议

## 一键安装

```sh
curl -fsSL https://raw.githubusercontent.com/dannunzio258/hy2-tuic-anytls-install/main/install-hy2-tuic-anytls.sh -o /tmp/install.sh && sh /tmp/install.sh
```

如果 Alpine 没有 curl，可以先执行：

```sh
apk add --no-cache ca-certificates curl
```

或者使用 wget：

```sh
wget -O /tmp/install.sh https://raw.githubusercontent.com/dannunzio258/hy2-tuic-anytls-install/main/install-hy2-tuic-anytls.sh && sh /tmp/install.sh
```

## 默认配置

- Hysteria2 UDP 端口：`11451`
- TUIC v5 UDP 端口：`11452`
- AnyTLS TCP 端口：`11453`
- Hysteria2 默认上行：`50 Mbps`
- Hysteria2 默认下行：`200 Mbps`
- TLS：自签证书，客户端默认允许不安全证书

安装过程中可以自定义端口、节点名称和是否开启 Hysteria2 端口跳跃。

## 管理命令

安装完成后可使用 `sb` 管理：

```sh
sb
```

显示节点链接，等同于：

```sh
sb show
```

查看服务状态：

```sh
sb status
```

重启服务：

```sh
sb restart
```

查看日志：

```sh
sb log
```

查看帮助：

```sh
sb help
```

## 节点信息

安装完成后会输出可直接导入 v2rayN 的链接。

节点链接也会保存到：

```sh
/etc/sing-box/v2rayn-links.txt
```

再次查看节点信息：

```sh
sb
```

## 放行端口

请在 VPS 防火墙和云服务商安全组中放行：

- `11451/udp`
- `11452/udp`
- `11453/tcp`

如果你修改了默认端口，请放行你实际填写的端口。

## 注意事项

- 请勿公开分享安装后输出的节点链接。
- 如果怀疑链接泄露，重新运行脚本会生成新的密码和节点信息。
- 自签证书方便使用，但安全性不如真实域名证书。
- 不需要端口跳跃时建议不要开启，减少暴露面。
