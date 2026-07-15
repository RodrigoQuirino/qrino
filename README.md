# Qrino

Portfólio pessoal + subdomínios para projetos MVP. Domínio: `qrino.com.br`.

Infra separada de qualquer outro projeto — LXC dedicada (VMID 104, `qrino-mvp`) no mesmo host Proxmox, túnel Cloudflare próprio, sem dependências cruzadas.

## Estrutura
```
docker-compose.yml   — stack do portfólio (nginx:alpine servindo public/)
public/
  index.html         — single page: hero (logo+tagline), portfólio, contato
  content.json       — conteúdo editável (tagline, itens do portfólio, contato) — editar aqui, não no HTML
  assets/logo.png    — logo (fundo transparente, texto preto — exige tema claro)
<mvp-nome>/          — 1 pasta por MVP futuro, cada um com sua própria stack
```

## Editar conteúdo do site
Basta editar `public/content.json` e fazer o deploy de novo (não precisa mexer no `index.html`):
- `tagline`: frase abaixo da logo
- `portfolio`: array de projetos (`name`, `description`, `url`) — adicionar um item novo pra cada projeto futuro
- `contact.linkedin` / `contact.email`: links da seção de contato

## Deploy
1. `pct push 104 <arquivo> /opt/docker/qrino-portfolio/<caminho>` para cada arquivo (ex.: `public/content.json` → `/opt/docker/qrino-portfolio/public/content.json`).
2. Se for a primeira vez (container ainda não existe): `pct exec 104 -- docker compose -f /opt/docker/qrino-portfolio/docker-compose.yml up -d`. Depois disso, só copiar os arquivos já é suficiente (nginx serve direto do volume, sem rebuild).

## Status
- [x] LXC 104 criada, Docker instalado
- [x] Túnel Cloudflare dedicado + DNS (`qrino.com.br`, `www.qrino.com.br`)
- [x] Site single page (hero + portfólio + contato) no ar, conteúdo via `content.json`
- [ ] Primeiro MVP
