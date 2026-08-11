# Instituto de Biologia do Solo — Repositório de Dados

[![License: CC BY 4.0](https://img.shields.io/badge/License-CC%20BY%204.0-lightgrey.svg)](https://creativecommons.org/licenses/by/4.0/)
[![License: CC0](https://img.shields.io/badge/License-CC0%201.0-lightgrey.svg)](https://creativecommons.org/publicdomain/zero/1.0/)

Repositório centralizado de dados, scripts e materiais suplementares de publicações científicas do **Instituto de Biologia do Solo (IBS)**. Cada projeto possui depósito independente no Zenodo com DOI próprio e versionamento individual.

📚 [Guia de Início Rápido](docs/QUICK_START.md) | 🔗 [Integração Zenodo](docs/ZENODO_INTEGRATION.md) | 🤝 [Como Contribuir](CONTRIBUTING.md)

## Estrutura do Repositório

```
.
├── publications/                  # Um diretório por publicação científica
│   └── YYYY_autor_journal/
│       ├── .zenodo.json           # Metadados para depósito no Zenodo
│       ├── CITATION.cff           # Citação formal do conjunto de dados
│       ├── README.md
│       ├── data/                  # raw/ e processed/
│       ├── scripts/               # Análises reprodutíveis
│       └── results/               # Figuras e tabelas
├── data/                          # Dados gerais/compartilhados do instituto
│   └── raw/                       # Dados brutos originais (imutáveis)
├── metadata/                      # Esquemas e padrões de metadados
│   └── schemas/                   # Templates Darwin Core
├── docs/                          # Documentação e templates
│   └── templates/                 # Modelos reutilizáveis
├── .github/
│   └── workflows/
│       └── zenodo-deposit.yml     # Workflow para depósito por projeto
├── CITATION.cff                   # Citação do repositório como um todo
├── DATA_POLICY.md                 # Política de dados abertos
├── CONTRIBUTING.md                # Guia de contribuição
├── CHANGELOG.md                   # Histórico de versões
└── README.md
```

## Publicações

| Projeto | DOI | Descrição |
|---------|-----|-----------|
| [2026_lima_neotropical_ento](publications/2026_lima_neotropical_ento/) | *pendente* | Taxonomia codificada de *Mucrosomia* (Collembola: Isotomidae) |
| [2026_Zeppelini_troglobius](publications/2026_Zeppelini_troglobius/) | *pendente* | Filogenia de Collembola troglobio |

## DOI por Projeto — Fluxo Zenodo

Cada pasta em `publications/` é um depósito Zenodo independente:

- **`.zenodo.json`** — metadados do depósito (título, autores, palavras-chave, licença, relação com o artigo)
- **GitHub Actions** — o workflow [`.github/workflows/zenodo-deposit.yml`](.github/workflows/zenodo-deposit.yml) faz o upload via API do Zenodo ao ser acionado manualmente
- **DOI conceito** — cada projeto recebe um DOI permanente que sempre aponta para a versão mais recente
- **DOI de versão** — cada nova versão do depósito recebe seu próprio DOI

Consulte [docs/ZENODO_INTEGRATION.md](docs/ZENODO_INTEGRATION.md) para o guia completo.

## Adicionando um Novo Projeto

```bash
# 1. Crie a pasta com a estrutura padrão
mkdir -p publications/YYYY_autor_journal/{data/{raw,processed},scripts,results}

# 2. Copie e preencha o template de metadados
cp docs/templates/zenodo_metadata_template.json publications/YYYY_autor_journal/.zenodo.json

# 3. Adicione um CITATION.cff e README.md ao projeto

# 4. Ao publicar: acione o workflow Zenodo via GitHub Actions
#    Actions → "Zenodo Deposit" → Run workflow → informar nome do projeto
```

## Padrões de Dados

Dados biológicos seguem o padrão **Darwin Core** (DwC), garantindo interoperabilidade com GBIF e SiBBr. Ver esquemas em [metadata/schemas/](metadata/schemas/).

## Licenciamento

- **Dados e metadados**: [CC0 1.0](LICENSE-CC0.md) — domínio público
- **Scripts e documentação**: [CC BY 4.0](LICENSE-CC-BY-4.0.md)

A licença de cada conjunto de dados é declarada no respectivo `.zenodo.json` e `CITATION.cff`.

## Como Citar

Cada projeto tem seu próprio `CITATION.cff` e DOI Zenodo. Para citar o repositório institucional como um todo:

```bibtex
@dataset{ibs_dados,
  author    = {{Instituto de Biologia do Solo}},
  title     = {Instituto de Biologia do Solo — Repositório de Dados},
  year      = {2026},
  publisher = {Zenodo},
  doi       = {10.5281/zenodo.XXXXXXX}
}
```

## Reprodutibilidade

Scripts são organizados sequencialmente (ex: `01_limpeza.R`, `02_analise.R`) e cada projeto documenta o ambiente computacional utilizado (`environment/`, `renv.lock`, `requirements.txt` ou `environment.yml`).

## Política de Dados Abertos

Consulte [DATA_POLICY.md](DATA_POLICY.md) para a política completa de compartilhamento, embargo e requisitos de citação.

## Contribuindo

Consulte [CONTRIBUTING.md](CONTRIBUTING.md) para diretrizes sobre submissão de dados e código.

---

**Última atualização**: Agosto 2026

