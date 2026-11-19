# Fable Lite ðŸ”¶

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="48" />
  <p><strong>Arckhé AI</strong></p>
</div>


> Garimpe o **raciocÃ­nio** dos modelos nos logs do Claude Code, meÃ§a como cada um
> trabalha em **nÃºmeros reais**, e transforme o delta num **playbook** que faz o
> Opus agir mais como o Fable 5.

NÃ£o dÃ¡ pra clonar o poder do Fable 5 â€” esse poder estÃ¡ nos pesos do modelo. Mas
os seus logs do Claude Code guardam o **ritmo de trabalho** de cada modelo que
vocÃª usou. Este projeto extrai esse ritmo e o destila num playbook que vocÃª
injeta em qualquer modelo (Opus, Codex, open-source) para uma execuÃ§Ã£o mais
disciplinada.

ðŸŒ **Curso (INEMA.CLUB v2):** https://inematds.github.io/fablelite/

---

## O pipeline

```
~/.claude/projects/*.jsonl   (logs pesados)
        â”‚
        â–¼  debloat_jsonl.py         destila 1 sessÃ£o  â†’ transcriÃ§Ã£o leve (~74% menor)
        â–¼  extract_corpus.py        filtra por message.model â†’ corpus + nÃºmeros
        â–¼  compare_models.py        Fable-5 vs Opus-4.8 â†’ o delta de ritmo
        â–¼  make_playbook.py         o delta â†’ playbook.md acionÃ¡vel
        â–¼  hooks/inject-playbook.sh injeta no SessionStart (ou skill / CLAUDE.md)
```

## InÃ­cio rÃ¡pido

```bash
cd scripts
python3 debloat_jsonl.py                         # vÃª o debloat (sessÃ£o de exemplo)
python3 extract_corpus.py --list                 # quais modelos hÃ¡ no seu histÃ³rico?
python3 compare_models.py --a claude-fable-5 --b claude-opus-4-8 --out ../playbook/compare.json
python3 make_playbook.py --from-json ../playbook/compare.json --out ../playbook/fable-mindset-playbook.md
```

Sem dados do Fable? Use os traces abertos:
```bash
pip install datasets
python3 scripts/import_hf_traces.py --dataset Glint-Research/Fable-5-traces
```

## Achados reais (medidos neste histÃ³rico)

| sinal | Fable-5 | Opus-4.8 | leitura |
|---|---|---|---|
| **% turnos que pensam antes de agir** | **99%** | 54% | **+45 pp â€” o sinal forte e transferÃ­vel** |
| ferramentas/turno (mÃ©dia) | 6.57 | 7.86 | Fable foi mais econÃ´mico |
| debloat | â€” | â€” | ~74% menor por sessÃ£o |

> **Honestidade:** o TEXTO do raciocÃ­nio nÃ£o fica nos logs (vem cifrado, sÃ³ a
> `signature`). Mede-se a **presenÃ§a** do raciocÃ­nio por turno, nÃ£o o conteÃºdo.
> E a amostra de Fable Ã© pequena (7 sessÃµes) â€” o delta de pensar-antes Ã© robusto;
> `read-before-edit`/`test-after-edit` sÃ£o boa prÃ¡tica, nÃ£o delta firme.

## Estrutura

```
index.html              landing do curso (GitHub Pages)
curso/trilhaN/          trilhas e mÃ³dulos (formato INEMA.CLUB v2)
scripts/                o pipeline (Python stdlib puro) + demo_session.jsonl
prompts/PROMPTS.md      os 4 prompts PT-BR prontos pra colar
playbook/               o playbook gerado + compare.json
hooks/                  inject-playbook.sh + como plugar no SessionStart
skill/fable-mindset/    a skill empacotando a tÃ©cnica
```

## CrÃ©ditos

MÃ©todo inspirado na ideia de minerar os arquivos JSONL de sessÃ£o para imitar o
"mindset" de um modelo. Dataset aberto de referÃªncia:
[`Glint-Research/Fable-5-traces`](https://huggingface.co/datasets/Glint-Research/Fable-5-traces).
Feito para o [INEMA.CLUB](https://inema.club).

---

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="32" />
  <p><strong>Arckhé AI</strong></p>
</div>