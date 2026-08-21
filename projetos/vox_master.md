VoxMaster — Treino de Dicção Gamificado com IA
Plataforma full-stack para treino de dicção e pronúncia, transformando prática de fala em algo mensurável, progressivo e divertido — no estilo dos apps de aprendizado de idiomas mais populares.

—
O usuário grava um áudio lendo um texto-alvo; o áudio é transcrito via Whisper (OpenAI) e comparado ao texto-alvo por distância de Levenshtein, gerando um score técnico de aderência.
—
Um LLM (GPT) analisa o resultado à luz da profissão informada pelo usuário, gerando feedback qualitativo, com progresso alimentando níveis, XP, streaks e boost de aniversário.
—
Pipeline de avaliação modelado como grafo de estados (LangGraph): cada etapa — transcrição, avaliação técnica, análise de cargo, decisão, avanço de nível — é um nó independente e testável, com roteamento condicional.
—
Backend em DDD: entidades e value objects (User, Exercício, Tentativa, TextoAlvo) concentram as regras de negócio; casos de uso orquestram a aplicação; repositórios abstraem a persistência em PostgreSQL.
—
Frontend em Next.js 15 + Tailwind CSS v4, com design system próprio inspirado na estética gamificada de apps de aprendizado.
Node.js
Fastify
LangGraph
OpenAI
PostgreSQL
Next.js 15
Tailwind CSS
Vitest