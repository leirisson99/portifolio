SGI — Sistema de Gestão de Licenças
Plataforma SaaS multi-tenant para empresas que precisam controlar licenças, alvarás e documentos obrigatórios sem depender de planilhas.

—
Centraliza o cadastro de empresas, controle de licenças com status e histórico de renovação, upload e organização de documentos por pasta/área responsável.
—
Dispara alertas automáticos por e-mail antes de vencimentos, evitando o risco de uma empresa operar com licença vencida.
—
Backend em Node.js/TypeScript com Fastify e Prisma sobre PostgreSQL, em camadas (domain → application → infrastructure → HTTP), com JWT, RBAC por grupos de acesso e isolamento por tenant.
—
Frontend em Next.js 16 + React 19, componentes Radix UI e Tailwind, com design system próprio (paleta, tipografia e tokens documentados).
—
Construído com Spec Driven Development: cada módulo nasce de uma spec de regras de negócio antes do código, com testes unitários, de integração e E2E (Vitest + Playwright) derivados da especificação.

tecnologias
Node.js
Fastify
Prisma
PostgreSQL
Next.js 16
React 19
Radix UI
Playwright