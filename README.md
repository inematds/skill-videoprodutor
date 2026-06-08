# skill-videoprodutor

**videoprodutor** — "o Produtor": skill que orquestra **link/assunto → vídeo profissional** ponta a ponta
(plano → voz → arte → render em **3 camadas**), nos formatos **16:9 e 9:16**, dark premium INEMA.CLUB, **tudo local**
(sem chave de API). Imagem (flux2-klein) é o padrão; **SVG é fallback automático** quando não há servidor de imagem.

## Instalar
```bash
npx skills add inematds/skill-videoprodutor
```
Ou manualmente: copie/symlink `skill/videoprodutor` para `~/.claude/skills/videoprodutor`.

## O que ela faz
As **3 camadas** que tornam um vídeo "profissional" (não slideshow):
1. **Cinema** — fundo com profundidade (imagem + véu + parallax/ken-burns).
2. **Texto cinético** — número/título/ênfase animados (GSAP).
3. **Ilustração do tópico** — ícone/diagrama/contador que mostra o que se narra (SVG animado no fallback).

Linha de montagem: `link → plano (vpe) → roteiro → voz (Kokoro) → arte (flux2-klein OU SVG auto) → compor (3 camadas) → validar → render 16:9 + 9:16`.

## Conteúdo
- `skill/videoprodutor/SKILL.md` — gatilho + fluxo + regras de ouro.
- `skill/videoprodutor/references/` — pipeline, mapa-libs-motion (qual lib por tarefa), safe-zones (9:16), fallback-svg.
- `skill/videoprodutor/scripts/` — molde testado: `composition-template.mjs` (3 camadas, auto imagem→SVG, safe zones), `gen-imgs.mjs` (flux2-klein), `svg-icons.mjs` (ícones SVG animados), `fetch-fonts.mjs`.

## Dependências (resumo)
Node 22+, FFmpeg, HyperFrames (`npx hyperframes`), internet no render (GSAP via CDN), Kokoro TTS + GPU (voz).
Opcional (com fallback SVG): servidor de imagem inemaimg/flux2-klein em `:8000`.

## Origem
Extraída do projeto [inematds/videoprodutor](https://github.com/inematds/videoprodutor) — caso de referência
funcional em `videos/hormozi-12-dicas` e decisões de arquitetura em `docs/00..08`.
