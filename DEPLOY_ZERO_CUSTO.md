# MOUTRYX — Deploy zero custo

## Arquitetura
- Aplicação web/backend: Render Free Web Service
- PostgreSQL: Neon Free
- IA: opcional; o sistema funciona sem `GEMINI_API_KEY` e deve apenas desabilitar recursos de IA que exigem a chave.

## Configuração do Render
1. Conecte o repositório GitHub do MOUTRYX ao Render.
2. O `render.yaml` já define build, start, health check e plano Free.
3. Cadastre as variáveis secretas no Render:
   - `DATABASE_URL` = connection string PostgreSQL do Neon
   - `SESSION_SECRET` = valor aleatório forte (32+ caracteres)
   - `GEMINI_API_KEY` = deixar vazio se IA paga não for usada agora
4. O Render fornecerá uma URL `https://...onrender.com`.

## Banco Neon
Crie um projeto PostgreSQL no plano Free e use a connection string como `DATABASE_URL`. O backend executa as migrations na inicialização.

## Observações
- O serviço web Free pode entrar em sleep após 15 minutos sem tráfego e levar cerca de 1 minuto para acordar.
- O Postgres Free do Render foi deliberadamente evitado porque expira após 30 dias.
- Não coloque `DATABASE_URL` ou `SESSION_SECRET` no GitHub.
