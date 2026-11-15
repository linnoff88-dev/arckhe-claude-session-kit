# claude-session-kit

**ðŸ‡§ðŸ‡· [PortuguÃªs](README.md) Â· ðŸ‡ºðŸ‡¸ [English](README.en.md) Â· ðŸ‡ªðŸ‡¸ [EspaÃ±ol](README.es.md)**

[![Claude Session Kit](guia/assets/banner.jpg)](https://inematds.github.io/claude-session-kit/guia/)

## ðŸ“– Guia de uso

Guia completo (landing + passo a passo): **https://inematds.github.io/claude-session-kit/guia/**

Kit pra manter sessÃµes do Claude Code enxutas: **statusline com cota real**
(5 h, semanal geral e semanal por modelo) + **trÃªs skills de sessÃ£o** + **plano
de otimizaÃ§Ã£o** que liga as duas coisas.

```
statusline/
  PROMPT.md               prompt pra instalar/configurar a statusline
  statusline-command.sh   o script (bash + jq + curl)
  settings-snippet.json   trecho do ~/.claude/settings.json
skills/
  PROMPT-instalar.md      prompt pra instalar as skills
  session-statusline/     checkpoint rÃ¡pido no meio do trabalho
  memory-audit/           auditoria de memÃ³ria e CLAUDE.md
  session-handoff/        resumo estruturado antes do /clear
  maestro-roteador/       escolhe modelo e esforÃ§o antes de despachar (quando a cota aperta)
  fable-mindset/          minera os JSONL das sessÃµes e gera playbook por modelo
PLANO-OTIMIZACAO.md       o ciclo checkpoint â†’ audit â†’ handoff e os gatilhos
```

## Statusline

```
nmaldaner@host:~/proj  Fable 5.1/medium  ctx 41%  5h:2%â†’19:10  w:69% F:80%!â†’14/09 21:00  d:40.9M
```

`w:` Ã© a cota semanal de todos os modelos; `F:` Ã© a cota semanal **do modelo
em uso** (a API manda `weekly_scoped`), com `!` quando estÃ¡ em alerta. Ã‰ a `F:`
que bloqueia primeiro â€” o script antigo sÃ³ mostrava a `w:` e por isso parecia
"nÃ£o atualizar".

InstalaÃ§Ã£o: cole `statusline/PROMPT.md` numa sessÃ£o do Claude Code, ou faÃ§a na
mÃ£o: copie o script pra `~/.claude/statusline-command.sh` e adicione o bloco de
`settings-snippet.json` ao `~/.claude/settings.json`.

## Skills

Cole `skills/PROMPT-instalar.md` numa sessÃ£o, ou copie as pastas pra
`~/.claude/skills/`. DivisÃ£o de trabalho e gatilhos em `PLANO-OTIMIZACAO.md`.

As trÃªs primeiras formam o ciclo (checkpoint â†’ audit â†’ handoff). As outras duas
sÃ£o apoio: `maestro-roteador` decide modelo/esforÃ§o quando a barra mostra `F:` em
alerta, e `fable-mindset` mede como cada modelo trabalha a partir dos mesmos JSONL
que alimentam o `d:` da barra.

## Teoria por trÃ¡s

O curso **Mestre em Contexto e Tokens** (https://inematds.github.io/cctop/) Ã© a
base deste kit: releitura de contexto, prompt caching, rotina de `/clear` e
`/compact`, handoff estruturado e subagentes. O kit Ã© a versÃ£o ferramenta do curso.

Plugins de terceiros compatÃ­veis com o ciclo (nÃ£o incluÃ­dos): `context-mode`,
`claude-mem`, `claudex`.

## Requisitos

Claude Code com login OAuth (claude.ai), `jq`, `curl`. O script lÃª o token de
`~/.claude/.credentials.json` localmente; nada sai da mÃ¡quina alÃ©m da chamada
ao endpoint oficial de uso.

Projeto de pesquisa/educaÃ§Ã£o â€” INEMA.

---

Projeto adaptado da comunidade INEMA TDS - Marca Arckhe