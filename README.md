# linux-code
 Various kinds of Linux code search on the Internet by myself and use to review.<br/>
 记录我自己在网上收集到的各种用到的 Linux code

## Linux-debian

 **前置-Frist**<br/>
    `apt update` 

 **安装-install**<br/>
    `apt install curl` 
  
 **命令-command**<br/>
    `date -R` 查看时间 | `ate --set` 修改时间


## v2ray-code 

 **服务器**
  1. `curl -O https://raw.githubusercontent.com/v2fly/fhs-install-v2ray/master/install-release.sh` (下载安装脚本)<br/>
  2. `bash install-release.sh` (安装|更新 V2ray主程序  (`bash install-release.sh -h` 帮助))<br/>
  3. `systemctl start|enable|stop v2ray` (启动|自动启动|关闭 V2ray)<br/>
   
  `jq . config.json`-检查`config.json`语法<br/>

  <br/>[**客户端**](https://github.com/v2fly/v2ray-core/releases)<br/>
  

<br/>
  
  [config]()-我的配置文件  |  [geosite/ip.dat]()-第三方规则 <br/>
  
 ### 服务器config
  ```
  {
  "inbounds": [
    {
      "port": 16823, // 服务器监听端口
      "protocol": "vmess",    // 主传入协议
      "settings": {
        "clients": [
          {
            "id": "b831381d-6324-4d53-ad4f-8cda48b30811",  // 用户 ID，客户端与服务器必须相同
            "alterId": 0
          }
        ]
      }
    }
  ],
  "outbounds": [
    {
      "protocol": "freedom",  // 主传出协议
      "settings": {}
    }
  ]
}
```
### 客户端config
  ``` 
  {
  "inbounds": [
    {
      "port": 1080, // 监听端口
      "protocol": "socks", // 入口协议为 SOCKS 5
      "sniffing": {
        "enabled": true,
        "destOverride": ["http", "tls"]
      },
      "settings": {
        "auth": "noauth"  //socks的认证设置，noauth 代表不认证，由于 socks 通常在客户端使用，所以这里不认证
      }
    }
  ],
  "outbounds": [
    {
      "protocol": "vmess", // 出口协议
      "settings": {
        "vnext": [
          {
            "address": "serveraddr.com", // 服务器地址，请修改为你自己的服务器 IP 或域名
            "port": 16823,  // 服务器端口
            "users": [
              {
                "id": "b831381d-6324-4d53-ad4f-8cda48b30811",  // 用户 ID，必须与服务器端配置相同
                "alterId": 0 // 此处的值也应当与服务器相同
              }
            ]
          }
        ]
      }
    }
  ]
}
```  
  

