# mine_rules

自用规则分流，收集整理个人日常使用的代理规则，适用于 Clash、Surge、Quantumult X、Loon、Shadowrocket 等主流客户端。

规则以精简、实用、持续更新为原则，主要用于广告拦截、国内外流量分流、流媒体解锁等场景。

## 特性

- 多客户端支持：Clash、Surge、Quantumult X、Loon、Shadowrocket 等
- 规则分类清晰：广告、直连、代理、流媒体、自定义
- 持续更新：不定期补充和修正规则
- 轻量实用：只保留常用规则，减少冗余
- 可自由组合：可单独引用某一类规则，也可整体订阅

## 支持客户端

| 客户端 | 支持 | 说明 |
| --- | --- | --- |
| Clash / Clash Meta | ✅ | 使用 `rule-providers` 或直接引用 |
| Surge | ✅ | 使用 `RULE-SET` |
| Quantumult X | ✅ | 使用 `filter_remote` |
| Loon | ✅ | 使用 `Remote Rule` |
| Shadowrocket | ✅ | 使用远程规则链接 |
| Stash | ✅ | 兼容 Clash 规则格式 |

## 目录结构

目录按客户端分类，具体以仓库实际内容为准：

```
mine_rules/
├── Clash/
│   ├── rules.yaml
│   └── ...
├── Surge/
│   └── rules.list
├── QuantumultX/
│   └── rules.list
├── Loon/
│   └── rules.list
├── Shadowrocket/
│   └── rules.list
└── README.md
```

## 规则分类

- **广告拦截**：常见广告域名、统计域名、推广域名
- **国内直连**：国内常用网站、服务、CDN
- **国外代理**：需要代理访问的域名
- **流媒体**：Netflix、YouTube、Disney+、Spotify 等
- **自定义**：个人补充规则，按需启用

## 使用方式

### Clash

```yaml
rule-providers:
  mine_rules:
    type: http
    behavior: classical
    url: "https://raw.githubusercontent.com/SunMoonWithYou/mine_rules/main/Clash/rules.yaml"
    path: ./ruleset/mine_rules.yaml
    interval: 86400

rules:
  - RULE-SET,mine_rules,PROXY
  - MATCH,DIRECT
```

### Surge

```
[Rule]
RULE-SET,https://raw.githubusercontent.com/SunMoonWithYou/mine_rules/main/Surge/rules.list,PROXY
```

### Quantumult X

```
[filter_remote]
https://raw.githubusercontent.com/SunMoonWithYou/mine_rules/main/QuantumultX/rules.list, tag=mine_rules, force-policy=PROXY, enabled=true
```

### Loon

```
[Remote Rule]
https://raw.githubusercontent.com/SunMoonWithYou/mine_rules/main/Loon/rules.list, policy=PROXY, tag=mine_rules
```

### Shadowrocket

在“配置” -> “规则”中添加远程规则链接：

```
https://raw.githubusercontent.com/SunMoonWithYou/mine_rules/main/Shadowrocket/rules.list
```

## 更新机制

- 规则会不定期更新，建议客户端配置自动更新
- Clash 可通过 `interval` 设置更新间隔
- Surge、Quantumult X、Loon 等支持远程规则自动更新
- 也可以手动拉取最新规则

## 自定义规则

如果想在本地追加规则，可以：

1. Fork 本仓库，修改对应文件
2. 在客户端配置中，将本仓库规则放在前面，本地规则放在后面
3. 使用 `DOMAIN`、`DOMAIN-SUFFIX`、`IP-CIDR` 等语法自行补充

示例：

```
DOMAIN-SUFFIX,example.com,PROXY
DOMAIN-KEYWORD,example,DIRECT
IP-CIDR,1.2.3.0/24,DIRECT
```

## 常见问题

**Q：规则会导致某些网站无法访问吗？**

A：有可能。如果遇到误杀，可以在本地规则中优先放行，或提交 Issue 反馈。

**Q：规则适用于所有代理客户端吗？**

A：不同客户端语法不同，本仓库按客户端分类存放，请选择对应格式。

**Q：多久更新一次？**

A：不定时更新，取决于日常使用中发现的遗漏或变化。

**Q：可以商用吗？**

A：本仓库仅供个人学习与测试使用，请勿用于商业用途。

## 免责声明

- 本仓库规则仅供个人学习、测试与研究使用
- 请遵守当地法律法规，勿用于非法用途
- 使用本规则产生的任何后果由使用者自行承担
- 如有侵权，请联系删除

## License

MIT
