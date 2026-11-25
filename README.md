# Fable Lite ê°Å¸âÂ¶

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="48" />
  <p><strong>Arckhé AI</strong></p>
</div>


> Garimpe o **raciocêÂ­nio** dos modelos nos logs do Claude Code, meêÂ§a como cada um
> trabalha em **nêÂºmeros reais**, e transforme o delta num **playbook** que faz o
> Opus agir mais como o Fable 5.

NêÂ£o dêÂ¡ pra clonar o poder do Fable 5 ê¢â¬â esse poder estêÂ¡ nos pesos do modelo. Mas
os seus logs do Claude Code guardam o **ritmo de trabalho** de cada modelo que
vocêÂª usou. Este projeto extrai esse ritmo e o destila num playbook que vocêÂª
injeta em qualquer modelo (Opus, Codex, open-source) para uma execuêÂ§êÂ£o mais
disciplinada.

ê°Å¸ÅÂ **Curso (ARCKHê AI v2):** https://linnoff88-dev.github.io/

---

## O pipeline

```
~/.claude/projects/*.jsonl   (logs pesados)
        ê¢ââ
        ê¢âÂ¼  debloat_jsonl.py         destila 1 sessêÂ£o  ê¢â â transcriêÂ§êÂ£o leve (~74% menor)
        ê¢âÂ¼  extract_corpus.py        filtra por message.model ê¢â â corpus + nêÂºmeros
        ê¢âÂ¼  compare_models.py        Fable-5 vs Opus-4.8 ê¢â â o delta de ritmo
        ê¢âÂ¼  make_playbook.py         o delta ê¢â â playbook.md acionêÂ¡vel
        ê¢âÂ¼  hooks/inject-playbook.sh injeta no SessionStart (ou skill / CLAUDE.md)
```

## InêÂ­cio rêÂ¡pido

```bash
cd scripts
python3 debloat_jsonl.py                         # vêÂª o debloat (sessêÂ£o de exemplo)
python3 extract_corpus.py --list                 # quais modelos hêÂ¡ no seu histêÂ³rico?
python3 compare_models.py --a claude-fable-5 --b claude-opus-4-8 --out ../playbook/compare.json
python3 make_playbook.py --from-json ../playbook/compare.json --out ../playbook/fable-mindset-playbook.md
```

Sem dados do Fable? Use os traces abertos:
```bash
pip install datasets
python3 scripts/import_hf_traces.py --dataset Glint-Research/Fable-5-traces
```

## Achados reais (medidos neste histêÂ³rico)

| sinal | Fable-5 | Opus-4.8 | leitura |
|---|---|---|---|
| **% turnos que pensam antes de agir** | **99%** | 54% | **+45 pp ê¢â¬â o sinal forte e transferêÂ­vel** |
| ferramentas/turno (mêÂ©dia) | 6.57 | 7.86 | Fable foi mais econêÂ´mico |
| debloat | ê¢â¬â | ê¢â¬â | ~74% menor por sessêÂ£o |

> **Honestidade:** o TEXTO do raciocêÂ­nio nêÂ£o fica nos logs (vem cifrado, sêÂ³ a
> `signature`). Mede-se a **presenêÂ§a** do raciocêÂ­nio por turno, nêÂ£o o conteêÂºdo.
> E a amostra de Fable êÂ© pequena (7 sessêÂµes) ê¢â¬â o delta de pensar-antes êÂ© robusto;
> `read-before-edit`/`test-after-edit` sêÂ£o boa prêÂ¡tica, nêÂ£o delta firme.

## Estrutura

```
index.html              landing do curso (GitHub Pages)
curso/trilhaN/          trilhas e mêÂ³dulos (formato ARCKHê AI v2)
scripts/                o pipeline (Python stdlib puro) + demo_session.jsonl
prompts/PROMPTS.md      os 4 prompts PT-BR prontos pra colar
playbook/               o playbook gerado + compare.json
hooks/                  inject-playbook.sh + como plugar no SessionStart
skill/fable-mindset/    a skill empacotando a têÂ©cnica
```

## CrêÂ©ditos

MêÂ©todo inspirado na ideia de minerar os arquivos JSONL de sessêÂ£o para imitar o
"mindset" de um modelo. Dataset aberto de referêÂªncia:
[`Glint-Research/Fable-5-traces`](https://huggingface.co/datasets/Glint-Research/Fable-5-traces).
Feito para o [ARCKHê AI](https://ARCKHê AI).

---

<div align="center">
  <img src="capa/logo.svg" alt="Arckhé AI" height="32" />
  <p><strong>Arckhé AI</strong></p>
</div>