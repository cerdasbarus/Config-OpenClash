# Config-OpenClash.

---
# =============== Barus-Config ================
# ================= RULES ==================
rule-providers:
  Direct:
    type: file
    behavior: classical
    path: "./rule_provider/Direct.yaml"
  Reject:
    type: file
    behavior: classical
    path: "./rule_provider/Reject.yaml"
  AdBlock:
    type: file
    behavior: classical
    path: "./rule_provider/AdBlock.yaml"
  YouTube:
    type: file
    behavior: classical
    path: "./rule_provider/YouTube.yaml"
  Facebook:
    type: file
    behavior: classical
    path: "./rule_provider/Facebook.yaml"
  TikTok:
    type: file
    behavior: classical
    path: "./rule_provider/TikTok.yaml"
  Sosmed:
    type: file
    behavior: classical
    path: "./rule_provider/Sosmed.yaml"
# ================= PROXY ==================
proxy-providers:
  Account-ETH2:
    type: file
    path: "./proxy_provider/Account-ETH2.yaml"
    health-check:
      enable: true
      url: http://www.gstatic.com/generate_204
      interval: '30'
  Account-ETH3:
    type: file
    path: "./proxy_provider/Account-ETH3.yaml"
    health-check:
      enable: true
      url: http://captive.apple.com/generate_204
      interval: '30'
  Account-INDO:
    type: file
    path: "./proxy_provider/Account-INDO.yaml"
    health-check:
      enable: true
      url: http://captive.apple.com/generate_204
      interval: '30'
# ================= GROUP ==================
proxy-groups:
- name: ➡️ETH1
  type: select
  disable-udp: false
  proxies:
  - DIRECT
  interface-name: eth1
  interval: '30'
#===========================================
- name: ➡️ETH2
  type: select
  disable-udp: false
  proxies:
  - DIRECT
  interface-name: eth2
  interval: '30'
#===========================================
- name: ➡️ETH3
  type: select
  disable-udp: false
  proxies:
  - DIRECT
  interface-name: eth3
  interval: '30'
#===========================================
- name: Account
  type: load-balance
  strategy: round-robin
  disable-udp: false
  use: 
  - Account-ETH2
  - Account-ETH3
  url: http://captive.apple.com/generate_204
  interval: '30'
- name: Account-INDO
  type: load-balance
  disable-udp: false
  use: 
  - Account-INDO
  url: http://captive.apple.com/generate_204
  interval: '30'
#===========================================
- name: AdBlock
  type: select
  disable-udp: false
  proxies:
  - REJECT
  - Account
#===========================================
- name: YouTube
  type: select
  disable-udp: false
  proxies:
  - Account
  - ➡️ETH1
  - ➡️ETH2
  - ➡️ETH3
#===========================================
- name: Facebook
  type: select
  disable-udp: false
  proxies:
  - Account
  - ➡️ETH1
  - ➡️ETH2
  - ➡️ETH3
#===========================================
- name: TikTok
  type: select
  disable-udp: false
  proxies:
  - Account
  - ➡️ETH1
  - ➡️ETH2
  - ➡️ETH3
#===========================================
- name: Sosmed
  type: select
  disable-udp: false
  proxies:
  - Account
  - ➡️ETH1
  - ➡️ETH2
  - ➡️ETH3
  #===========================================
- name: WhatsApp
  type: select
  disable-udp: false
  proxies:
  - Account-INDO
  - ➡️ETH1
  - ➡️ETH2
  - ➡️ETH3
#===========================================
- name: Remote
  type: fallback
  disable-udp: false
  proxies:
  - ➡️ETH2
  - ➡️ETH1
  - Account
  - ➡️ETH3
  url: http://captive.apple.com/generate_204
  interval: '30'
#===========================================
- name: Game
  type: fallback
  disable-udp: false
  proxies:
  - ➡️ETH1
  - ➡️ETH2
  - ➡️ETH3
  - Account
  url: http://captive.apple.com/generate_204
  interval: '30'
#===========================================
rules:
- RULE-SET,Direct,DIRECT
- RULE-SET,Reject,REJECT
- RULE-SET,AdBlock,AdBlock
- RULE-SET,YouTube,YouTube
- RULE-SET,Facebook,Facebook
- RULE-SET,TikTok,TikTok
- RULE-SET,Sosmed,Sosmed
# > Call Wa
- DST-PORT,3478/5060/5061,WhatsApp,udp
# > Remote
- DST-PORT,1194,Remote,tcp
- DST-PORT,9993,Remote,udp
# > Mobile Legends
- DST-PORT,5000-5059/5156/5530-5559/10003/30001-30021,Game,tcp
- DST-PORT,5000-5059/5105-5109/5500-5530/6789/9992/30001-30221,Game,udp
# > FreeFire
- DST-PORT,6006/6674/7006/8001/8006/9006/9137/10006/11006/12006/13006/3006/39698/39800,Game,tcp
- DST-PORT,6008/7008/8008/8130/8443/9008/9120/10008/10011/10012/10013/10014/10015/11008/12008/13008/14008/3008/39003/39006/39698/39779/39800,Game,udp
# > Highs Domino
- DST-PORT,30001-30300/26000-26030/26666,Game,tcp
# > PUBG
- DST-PORT,10012/13004/17000/17300/18081/20000-20002/20371,Game,tcp
- DST-PORT,10010/10013/10039/10096/10491/10612/11455/12235/13748/13894/13972/20000-20002,Game,udp
# > Point Blank
- DST-PORT,39190-39200/49001-49190,Game,tcp
# > COD
- DST-PORT,3013/10000-10019/18082/63010/63030,Game,tcp
- DST-PORT,7085-7786/7790-7995/8700/9030/10010-10019/17000-20100,Game,udp
# > AOV
- DST-PORT,10001-10094,Game,tcp
- DST-PORT,10101-10201/10080-10110/17000-18000,Game,udp
# > Stumble Guys
- DST-PORT,3055-3058,Game,udp
# > Genshin Impact
- DST-PORT,42472,Game,tcp
- DST-PORT,42472/22101-22102,Game,udp
# > Clash of Clans (COC) & Clash Royale
- DST-PORT,9330-9340,Game,tcp
- DST-PORT,9330-9340,Game,udp
# > League of Legends (LOL) Mobile
- DST-PORT,2080-2099,Game,tcp
- DST-PORT,5100,Game,udp
# > DOTA2
- DST-PORT,9100-9200/8230-8230/8110-8120/27000-28998,Game,tcp
- DST-PORT,27000-28998/39000,Game,udp
# > LINE Let’s Get Rich
- DST-PORT,10300-10515,Game,tcp
# ================= Barus ==================
- MATCH,Account
dns:
  nameserver:
  - dhcp://"eth1"
  - dhcp://"eth2"
  - dhcp://"eth3"
  - https://dns.adguard.com/dns-query
  - https://dns-google.com/dns-query
  - tls://dns.adguard.com
  - tls://dns-google.com/
  enable: true
  ipv6: false
  enhanced-mode: fake-ip
  fake-ip-range: 198.18.0.1/16
  listen: 127.0.0.1:7874
  fake-ip-filter:
  - "+.*"
  default-nameserver:
  - 192.168.2.1
  - 192.168.3.1
  - 192.168.4.1
unified-delay: true
allowinsecure: true
redir-port: 7892
tproxy-port: 7895
port: 7890
socks-port: 7891
mixed-port: 7893
mode: rule
log-level: silent
allow-lan: true
external-controller: 0.0.0.0:9090
secret: barus
bind-address: "*"
ipv6: false
tun:
  enable: true
  stack: system
  device: utun
  auto-route: false
  auto-detect-interface: false
  dns-hijack:
  - tcp://any:53
external-ui: "/usr/share/openclash/ui"
