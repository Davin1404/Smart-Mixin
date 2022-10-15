# ClashConfigProcesser  

## 一个开源的Clash配置预处理器。  

## Ver 2.0 will be ready soon!  

更加面向对象，语法更加简洁，交互更为友好，新版本2.0预览已经发布；请前往Release体验。  
在编写2.0的时候，程序经历了好几次重构；这些迭代都只为了一个目的，更简洁直观的操作。  
## 加载配置文件  
在2.0版本中
## 新建  
在2.0版本中，新建代理、代理组、规则的语法都发生了改变：  

### 新建代理  
```Python
Shadowsocks = Proxy(DICT={'name': '🇨🇳 Shadowsocks', 'type': 'ss', 'server': '127.0.0.1', 'port': '12345', 'cipher': 'chacha20-ietf-poly1305', 'udp': True, 'password': 'PassWD', 'plugin': 'obfs', 'plugin-opts': {'host': '6d1af65d074041a0.swcdn.apple.com', 'mode': 'http'}})
```  
另一种等价写法：
```Python
Shadowsocks = Proxy(YAML="""
- cipher: chacha20-ietf-poly1305
  name: "\U0001F1E8\U0001F1F3 Shadowsocks"
  password: PassWD
  plugin: obfs
  plugin-opts:
    host: 6d1af65d074041a0.swcdn.apple.com
    mode: http
  port: '12345'
  server: 127.0.0.1
  type: ss
  udp: true
""")
```

### 新建代理组  
这里有好几种等价方法：  
```Python
No = ProxyGroup(DICT={'name': 'No', 'url': 'https://cp.cloudflare.com/generate_204', 'type': 'select', 'proxies': [Shadowsocks, Trojan]})
```
```Python
No = ProxyGroup(YAML="""
- name: No
  proxies:
  - "\U0001F1E8\U0001F1F3 Shadowsocks"
  - "\U0001F1E8\U0001F1F3 Trojan"
  type: select
  url: https://cp.cloudflare.com/generate_204
""")
```
```Python
No = ProxyGroup(DICT={'name': 'No', 'url': 'https://cp.cloudflare.com/generate_204', 'type': 'select', 'proxies': []})
No.proxies = [Shadowsocks, Trojan] #书接上文
```  

### 新建规则
此二种方法等价：
```Python
R = Rule("DOMAIN-SUFFIX", "Apple.com", "\U0001F34E Apple")
```
```Python
R = Rule(YAML="DOMAIN-SUFFIX,Apple.com,\U0001F34E Apple")
```  

## 绑定与添加
