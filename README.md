# skill-videoprodutor — o Produtor

> **Norte:** entro com **um link / fonte de dados** → sai o **plano + a execução** de um **vídeo profissional** (propaganda ou explicativo). Uma coisa só, ponta a ponta.

**videoprodutor** ("o Produtor") é o **orquestrador** do ecossistema de vídeo do usuário, empacotado como skill
instalável. Ele não reinventa render nem geração — **coordena as peças que já existem** (planejamento, direção,
prompt, imagem, voz, render) numa linha de montagem única. Saída em **16:9 e 9:16**, dark premium INEMA.CLUB,
**tudo local** (sem chave de API). Imagem (flux2-klein) é o padrão; **SVG é fallback automático** quando não há
servidor de imagem.

## Por que existe

O usuário já tem ~11 skills e 6 motores de vídeo espalhados. **~70% da fábrica já existe**, mas falta a peça que
**conecta o link à execução automática**. Esta skill é essa peça.

Decisão estratégica: **não refazer do zero, não manter silos** — montar a fábrica reusando o que já funciona,
com Remotion como motor de render unificado (camada cinema do pixflow + componentes do remotion-templates para
texto cinético e ilustração de tópico).

## A linha de montagem

```
LINK / FONTE
  → entender (tema, dados, ângulo)
  → PLANO        (video-plan-editor → plano-edicao.json: roteiro, beats, tópicos, CTA)
  → DIREÇÃO+IMG  (mdd/promptprof brief fiel → flux2-klein imagem  OU  SVG auto)
  → VOZ+TIMING   (inemavox/Kokoro narração + durações + timestamps)
  → RENDER       (3 camadas: parallax/cinema + texto cinético + ilustração de tópico)
  → VÍDEO PROFISSIONAL  (preset: propaganda | explicativo · 16:9 + 9:16)
```

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

Peças reusáveis vivem em projetos próprios: `~/projetos/pixflow` (render cinema), `~/projetos/skill-video-plan-editor`,
`~/projetos/mdd`, `~/projetos/promptprof`, `~/projetos/fontefilm`, `~/projetos/remotion-templates`,
`~/projetos/inemaimg` (flux2-klein), `~/projetos/inemavox` (voz).

## Origem

Extraída e consolidada do projeto de arquitetura `videoprodutor` (docs `00..08` + caso de referência funcional
`videos/hormozi-12-dicas`, 3 camadas validadas). Esta skill é a destilação executável daquela análise.
