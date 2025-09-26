# search-api

此库[fork](https://github.com/ikechan8370/search-api)自用，为[chatgpt-plugin](https://github.com/ikechan8370/chatgpt-plugin.git)的搜索api后端

如需自己本地跑可按步骤部署

**如果要使用谷歌搜索则需要获取 Google API Key**

- 点击[这里]( https://console.cloud.google.com/)访问官网

- 在左侧导航栏中，找到 “API 和服务” -> “凭据”

- 点击 “+ 创建凭据” -> “API 密钥”，然后复制生成的密钥

- 在 “API 和服务” -> “库” 中搜索Custom Search API并启用

- 把密钥填在main.go的21行

```Go
var geminiKeys = []string{"你的密钥"}
```

## win

- 需要先安装[Go](https://go.dev/dl/)

1. 找个地方克隆项目：

```sh
git clone https://github.com/kvcfdd/search-api.git
```

2. search-api目录下运行命令完成编译

```sh
go run .
```

- 这时候不出意外已是运行状态，可运行以下命令生成一个exe文件，后续点击即可运行

```sh
go build
```

## Linux

**这里以Debian为例**

- 依次运行命令即可

```sh
1.更新软件包列表
sudo apt update
2.安装Go
sudo apt install golang-go -y
3.克隆并编译项目(默认放在opt/search-api)
git clone https://github.com/kvcfdd/search-api.git /opt/search-api
cd /opt/search-api
go build -o search-api .
启动
./search-api
```

- 如需开机自启

1. 运行命令创建service 文件

```sh
sudo nano /etc/systemd/system/search-api.service
```

2. 写入以下内容

```sh
[Unit]
Description=Search API Service
After=network.target

[Service]
Type=simple
User=root

WorkingDirectory=/opt/search-api
ExecStart=/opt/search-api/search-api

Restart=on-failure
RestartSec=5s

[Install]
WantedBy=multi-user.target
```

3. 重新加载 systemd 配置

```sh
sudo systemctl daemon-reload
```

4. 后台启动

```sh
sudo systemctl start search-api
```

5. 检查服务状态

```sh
sudo systemctl status search-api
```

- 如果正常，会看到绿色的圆点

6. 设置开机自启

```sh
sudo systemctl enable search-api
```
