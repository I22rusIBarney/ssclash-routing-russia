# ==========================================================
#  RoscomVPN routing (template_remnawave.yaml) + SSClash
# ==========================================================
proxy-providers:
  bobrgo:
    type: http
    url: "https://твоя ссылка подписки"
    path: ./providers/название твоей подписки.yaml
    interval: 86400
    health-check:
      enable: true
      url: https://www.gstatic.com/generate_204
      interval: 300

# --- изменено под SSClash: был mixed-port: 7890 ---
tproxy-port: 7894
mode: rule
log-level: silent
allow-lan: false
ipv6: false
unified-delay: true
tcp-concurrent: true
external-controller: 127.0.0.1:9090
# --- на роутере процессов нет, в оригинале было strict ---
find-process-mode: off

tun:
  enable: true
  device: clash-tun
  stack: mixed
  auto-route: false
  auto-redirect: false
  auto-detect-interface: false

profile:
  store-selected: true
  store-fake-ip: true

dns:
  enable: true
  listen: 0.0.0.0:7874
  ipv6: false
  enhanced-mode: fake-ip
  fake-ip-range: 198.18.0.1/16
  fake-ip-filter:
    - rule-set:private-domains
  # твоя строка из старого конфига, не из репозитория — удали, если не нужна
  nameserver-policy:
    '+.polaris-iot.com': 'https://77.88.8.8/dns-query'
  default-nameserver:
    - https://77.88.8.8/dns-query
    - https://8.8.8.8/dns-query
  proxy-server-nameserver:
    - https://77.88.8.8/dns-query
    - https://8.8.8.8/dns-query
  direct-nameserver:
    - https://77.88.8.8/dns-query
    - https://8.8.8.8/dns-query
  nameserver:
    - https://8.8.8.8/dns-query#PROXY

sniffer:
  enable: true
  override-destination: false
  parse-pure-ip: true
  sniff:
    HTTP:
      ports:
        - 80
        - 8080-8880
    TLS:
      ports:
        - 443
        - 8443
  skip-dst-address:
    - 224.0.0.0/3
    - 10.0.0.0/8
    - 127.0.0.0/8
    - 100.64.0.0/10
    - 172.16.0.0/12
    - 198.18.0.0/15
    - 169.254.0.0/16
    - 192.168.0.0/16
    - 192.0.0.0/24
    - 192.0.2.0/24
    - 192.88.99.0/24
    - 198.51.100.0/24
    - 203.0.113.0/24
    - fc00::/7
    - ff00::/8
    - fe80::/10
    - ::/127

proxy-groups:
  - name: 🛡️ VPN
    icon: https://cdn.jsdelivr.net/gh/Koolson/Qure@master/IconSet/Color/Hijacking.png
    type: select
    url: https://www.gstatic.com/generate_204
    include-all: true
    proxies:
      - ⚡️ Авто

  - name: 📺 Youtube
    icon: https://cdn.jsdelivr.net/gh/Koolson/Qure@master/IconSet/Color/YouTube.png
    type: select
    include-all: true
    proxies:
      - 🛡️ VPN

  - name: 💬 Discord.exe
    icon: https://cdn.jsdelivr.net/gh/Koolson/Qure@master/IconSet/Color/Discord.png
    type: select
    include-all: true
    proxies:
      - 🛡️ VPN

  - name: 🎮 Игры
    icon: https://cdn.jsdelivr.net/gh/Koolson/Qure@master/IconSet/Color/Game.png
    type: select
    include-all: true
    proxies:
      - 🔓 Без VPN
      - 🛡️ VPN

  - name: ⚡️ Авто
    type: url-test
    tolerance: 150
    url: https://www.gstatic.com/generate_204
    interval: 300
    include-all: true
    hidden: true

  - name: PROXY
    type: select
    hidden: true
    proxies:
      - 🛡️ VPN

  - name: 🔓 Без VPN
    type: select
    hidden: true
    proxies:
      - DIRECT

  - name: ⛔ Блок
    type: select
    hidden: true
    proxies:
      - REJECT

  - name: ⏭️ Пропуск
    type: select
    hidden: true
    proxies:
      - PASS

rule-anchor:
  domain: &domain {type: http, behavior: domain, format: mrs, interval: 86400}
  ipcidr: &ipcidr {type: http, behavior: ipcidr, format: mrs, interval: 86400}
  classical: &classical {type: http, behavior: classical, format: yaml, interval: 86400}

rule-providers:
  private-domains:
    <<: *domain
    url: https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geosite/release/mihomo/private.mrs
    path: ./ruleset/geosite-private.mrs
  category-ru:
    <<: *domain
    url: https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geosite/release/mihomo/category-ru.mrs
    path: ./ruleset/category-ru.mrs
  whitelist:
    <<: *domain
    url: https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geosite/release/mihomo/whitelist.mrs
    path: ./ruleset/whitelist.mrs
  microsoft:
    <<: *domain
    url: https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geosite/release/mihomo/microsoft.mrs
    path: ./ruleset/microsoft.mrs
  apple:
    <<: *domain
    url: https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geosite/release/mihomo/apple.mrs
    path: ./ruleset/apple.mrs
  google-play:
    <<: *domain
    url: https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geosite/release/mihomo/google-play.mrs
    path: ./ruleset/google-play.mrs
  epicgames:
    <<: *domain
    url: https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geosite/release/mihomo/epicgames.mrs
    path: ./ruleset/epicgames.mrs
  origin:
    <<: *domain
    url: https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geosite/release/mihomo/origin.mrs
    path: ./ruleset/origin.mrs
  riot:
    <<: *domain
    url: https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geosite/release/mihomo/riot.mrs
    path: ./ruleset/riot.mrs
  escapefromtarkov:
    <<: *domain
    url: https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geosite/release/mihomo/escapefromtarkov.mrs
    path: ./ruleset/escapefromtarkov.mrs
  steam:
    <<: *domain
    url: https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geosite/release/mihomo/steam.mrs
    path: ./ruleset/steam.mrs
  twitch:
    <<: *domain
    url: https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geosite/release/mihomo/twitch.mrs
    path: ./ruleset/twitch.mrs
  twitch-ads:
    <<: *domain
    url: https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geosite/release/mihomo/twitch-ads.mrs
    path: ./ruleset/twitch-ads.mrs
  pinterest:
    <<: *domain
    url: https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geosite/release/mihomo/pinterest.mrs
    path: ./ruleset/pinterest.mrs
  faceit:
    <<: *domain
    url: https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geosite/release/mihomo/faceit.mrs
    path: ./ruleset/faceit.mrs
  github:
    <<: *domain
    url: https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geosite/release/mihomo/github.mrs
    path: ./ruleset/github.mrs
  youtube:
    <<: *domain
    url: https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geosite/release/mihomo/youtube.mrs
    path: ./ruleset/youtube.mrs
  telegram:
    <<: *domain
    url: https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geosite/release/mihomo/telegram.mrs
    path: ./ruleset/telegram.mrs
  win-spy:
    <<: *domain
    url: https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geosite/release/mihomo/win-spy.mrs
    path: ./ruleset/win-spy.mrs
  torrent-domains:
    <<: *domain
    url: https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geosite/release/mihomo/torrent.mrs
    path: ./ruleset/torrent-domains.mrs
  category-ads:
    <<: *domain
    url: https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geosite/release/mihomo/category-ads.mrs
    path: ./ruleset/category-ads.mrs
  private-ips:
    <<: *ipcidr
    url: https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geoip/release/mihomo/private.mrs
    path: ./ruleset/geoip-private.mrs
  direct-ips:
    <<: *ipcidr
    url: https://cdn.jsdelivr.net/gh/hydraponique/roscomvpn-geoip/release/mihomo/direct.mrs
    path: ./ruleset/direct-ips.mrs
  torrent-clients:
    <<: *classical
    url: https://raw.githubusercontent.com/legiz-ru/mihomo-rule-sets/main/other/torrent-clients.yaml
    path: ./ruleset/torrent-clients.yaml
  games:
    <<: *classical
    url: https://raw.githubusercontent.com/roscomvpn/custom-category/release/mihomo/games.yaml
    path: ./ruleset/games.yaml
  ru-apps:
    <<: *classical
    url: https://raw.githubusercontent.com/roscomvpn/custom-category/release/mihomo/ru-apps.yaml
    path: ./ruleset/ru-apps.yaml

rules:
  - RULE-SET,private-ips,DIRECT,no-resolve
  - IP-CIDR,::/0,REJECT-DROP,no-resolve
  - AND,((NETWORK,UDP),(DST-PORT,443)),REJECT-DROP
  - RULE-SET,private-domains,DIRECT
  - RULE-SET,category-ads,REJECT-DROP
  - RULE-SET,win-spy,REJECT-DROP
  - RULE-SET,torrent-domains,DIRECT
  - RULE-SET,google-play,PROXY
  - RULE-SET,twitch-ads,PROXY
  - RULE-SET,youtube,📺 Youtube
  - RULE-SET,telegram,PROXY
  - RULE-SET,github,PROXY
  - RULE-SET,epicgames,🎮 Игры
  - RULE-SET,origin,🎮 Игры
  - RULE-SET,riot,🎮 Игры
  - RULE-SET,escapefromtarkov,🎮 Игры
  - RULE-SET,steam,🎮 Игры
  - RULE-SET,faceit,🎮 Игры
  - RULE-SET,twitch,DIRECT
  - RULE-SET,microsoft,DIRECT
  - RULE-SET,apple,DIRECT
  - RULE-SET,pinterest,DIRECT
  - RULE-SET,category-ru,DIRECT
  - RULE-SET,whitelist,DIRECT
  - RULE-SET,torrent-clients,DIRECT
  - PROCESS-NAME-REGEX,discord,💬 Discord.exe
  - PROCESS-NAME-REGEX,vesktop,💬 Discord.exe
  - RULE-SET,games,🎮 Игры
  - RULE-SET,ru-apps,DIRECT
  - RULE-SET,direct-ips,DIRECT
  - MATCH,PROXY
