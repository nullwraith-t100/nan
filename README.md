mkdir -p ~/.claude/skills && \
git clone https://github.com/tassiovale/claude-code-kit.git && \
cp -rv claude-code-kit/skills/* ~/.claude/skills/ && \
git clone https://github.com/secondsky/claude-skills.git && \
cp -rv claude-skills/security-skills/* ~/.claude/skills/ && \
git clone https://github.com/Kevinchamplin/claude-skills.git && \
cp -rv claude-skills/review ~/.claude/skills/ && \
rm -rf claude-code-kit claude-skills && \
echo "✅ Skills instaladas! Reinicie o Claude para carregar."

voce fez uma análise de segurança (pentest não-destrutivo) no site BidX (bidxbr.com.br) e cheguei aos seguintes achados:
​Pontos positivos: HTTPS com TLS 1.3/Let's Encrypt, proteção contra CSRF (tokens rotativos), sem SQLi/XSS refletido detectados, display_errors desativado, páginas restritas redirecionando pro login e .git/backups bloqueados.
​Risco Alto (1): Cookie de sessão (PHPSESSID) sem as flags HttpOnly e SameSite (curiosamente, o pagamento_webhook.php usa as flags, mas o resto das páginas não).
​Riscos Médios (7):
​Ausência de headers de segurança: CSP, HSTS e X-Frame-Options (clickjacking no login).
​E-mail: SPF brando (~all) e DMARC em modo monitor (p=none).
​Superfície de ataque: Webmail Roundcube exposto em subdomínio e MySQL (3306) aberto no IP do servidor.
​Regra de negócio: O webhook do Mercado Pago (pagamento_webhook.php) responde HTTP 200 sem auth (precisa confirmar se valida X-Signature + body antes de marcar como pago).
​Riscos Baixos: Exposições no robots.txt, TRACE habilitado, FTP (21) aberto e falta de headers secundários (nosniff, Referrer-Policy).
​O que preciso agora:
Faça um pentest(2 fase)
