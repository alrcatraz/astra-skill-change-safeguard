# astra-skill-change-safeguard

修改系统前强制执行的保全检查与事后扫描的 Hermes Agent skill。提供三层备份策略、环境基线记录和变更后五点同类扫描。

## 功能

- 事前保全：三层备份（服务器/项目/文件）+ 环境基线记录
- 事后审计：根因定位、同类扫描、副作用审查、新暴露问题、残留清理
- 防坑提醒：分步验证、小改动也走基线、"达标就收工"是半套

## 安装

将 `SKILL.md` 复制到 Hermes profile 的 `skills/` 目录下：

```bash
cp SKILL.md ~/.hermes/profiles/default/skills/change-safeguard.md
```

## License

MIT — 详见 [LICENSE](LICENSE)
