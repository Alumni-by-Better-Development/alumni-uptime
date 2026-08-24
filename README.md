# alumni-uptime

![Uptime 30d](https://img.shields.io/endpoint?url=https%3A%2F%2Fraw.githubusercontent.com%2FAlumni-by-Better-Development%2Falumni-uptime%2Fmain%2Fuptime.json)

Monitor de uptime do Portal Alumni (produção). Roda a cada ~5 minutos via GitHub Actions.

**Como o alerta chega:** quando um check falha, a run agendada falha e o GitHub envia
e-mail automaticamente para o dono do workflow (brunogilferro). Enquanto estiver fora,
cada run repete o alerta.

Checks:
- `api.portal.betteredtech.com.br/health` → espera **401** (hook de auth; 5xx/timeout = fora)
- `portal.betteredtech.com.br` → espera **2xx/3xx**
- **Certificado da API**: falha se vencer em menos de **14 dias** — alarme antecipado
  do incidente de 24/08/2026 (cert do Fly expirou sem renovar atrás do Cloudflare).

O job `keepalive` commita um heartbeat mensal para o GitHub não desativar o cron
(repos sem atividade por 60 dias têm schedules suspensos).
