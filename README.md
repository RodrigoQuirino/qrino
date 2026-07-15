# Qrino

Portfólio pessoal + subdomínios para projetos MVP. Domínio: `qrino.com.br`.

Infra separada de qualquer outro projeto — LXC dedicada (VMID 104, `qrino-mvp`) no mesmo host Proxmox, túnel Cloudflare próprio, sem dependências cruzadas.

## Estrutura
```
docker-compose.yml   — stack do portfólio (nginx:alpine servindo public/)
public/              — site estático do portfólio (placeholder por enquanto)
<mvp-nome>/           — 1 pasta por MVP futuro, cada um com sua própria stack
```

## Deploy
1. `pct push 104 <arquivo> /opt/docker/qrino-portfolio/<caminho>` para cada arquivo.
2. `pct exec 104 -- docker compose -f /opt/docker/qrino-portfolio/docker-compose.yml up -d`.

## Status
- [x] LXC 104 criada, Docker instalado
- [x] Túnel Cloudflare dedicado + DNS (`qrino.com.br`, `www.qrino.com.br`)
- [x] Placeholder no ar
- [ ] Identidade visual / conteúdo real do portfólio
- [ ] Primeiro MVP
