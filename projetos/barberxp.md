BarberXP — Gestão de Barbearias
Plataforma SaaS multi-tenant para gestão completa de barbearias, criada para resolver um problema real e pouco explorado no Brasil: a maioria dos salões ainda funciona no improviso, com agendamento por WhatsApp, comissões calculadas manualmente e nenhum controle real de fluxo de caixa.

—
Centraliza agendamento online, controle financeiro (receitas, despesas e caixa em tempo real), cálculo automático de comissões por barbeiro e gestão de estoque integrada ao financeiro.
—
Motor de gamificação com tiers progressivos (Bronze, Carbon, Prata, Diamante), pontos, desafios, ranking entre clientes e resgate de recompensas, para transformar clientes esporádicos em recorrentes.
—
Backend em Fastify/TypeScript (domain, application, infrastructure), Prisma sobre PostgreSQL, JWT e multi-tenancy com isolamento de dados desde a concepção — incluindo painel de Super Admin com auditoria entre tenants.
—
Frontend em Next.js 16 (App Router), React 19, Tailwind CSS v4 e Zustand, com três áreas de acesso: cliente, barbeiro/admin e super admin.
—
Mais de 80 arquivos de teste no backend (Vitest) cobrindo domínio, casos de uso e integração HTTP com banco real, além de testes de componentes e hooks no frontend. Em validação com barbearias reais em Manaus.

tecnologias
Fastify
TypeScript
Next.js 16
React 19
Prisma
PostgreSQL
Zustand
Docker
Vitest