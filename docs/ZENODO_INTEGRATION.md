# Integração com Zenodo — DOI por Projeto

Este repositório adota uma estratégia de **depósito individual por publicação**: cada pasta em `publications/` gera um registro independente no Zenodo, com seu próprio DOI conceito e DOIs de versão.

## Estrutura de DOIs

```
Repositório GitHub
└── publications/
    ├── 2026_lima_neotropical_ento/   →  DOI Zenodo: 10.5281/zenodo.AAAAAAA
    └── 2026_Zeppelini_troglobius/   →  DOI Zenodo: 10.5281/zenodo.BBBBBBB
```

- **DOI conceito**: permanente, sempre aponta para a versão mais recente do depósito
- **DOI de versão**: imutável, identifica uma versão específica dos dados

## Pré-requisitos

### 1. Token Zenodo

1. Acesse [zenodo.org/account/settings/applications](https://zenodo.org/account/settings/applications)
2. Clique em **New token** em "Personal access tokens"
3. Marque os escopos `deposit:write` e `deposit:actions`
4. Copie o token gerado

### 2. Secret no GitHub

1. No repositório GitHub: **Settings → Secrets and variables → Actions**
2. Clique em **New repository secret**
3. Nome: `ZENODO_TOKEN`
4. Valor: o token copiado acima

---

## Arquivos de Metadados — `.zenodo.json`

Cada projeto deve conter um arquivo `.zenodo.json` na raiz da sua pasta.

**Localização:** `publications/YYYY_autor_journal/.zenodo.json`

**Template:** [`docs/templates/zenodo_metadata_template.json`](templates/zenodo_metadata_template.json)

### Campos obrigatórios

| Campo | Descrição |
|-------|-----------|
| `title` | Título no formato "Data and scripts for: [título do artigo]" |
| `description` | Descrição dos dados e análises incluídos |
| `upload_type` | `"dataset"` para dados; `"software"` se predominantemente scripts |
| `creators` | Lista de autores com `name`, `affiliation` e `orcid` |
| `license` | `"cc-by-4.0"` ou `"cc-zero"` |

### Relacionando ao artigo publicado

Após o artigo ser publicado, adicione o DOI do artigo em `related_identifiers`:

```json
"related_identifiers": [
  {
    "identifier": "https://doi.org/10.XXXXX/XXXXX",
    "relation": "isSupplementTo",
    "scheme": "doi",
    "resource_type": "publication-article"
  }
]
```

---

## Depositando via GitHub Actions

O workflow [`.github/workflows/zenodo-deposit.yml`](../.github/workflows/zenodo-deposit.yml) realiza o depósito via API do Zenodo.

### Novo depósito (primeira vez)

1. Vá para **Actions → Zenodo Deposit → Run workflow**
2. Preencha:
   - **project**: nome da pasta (ex: `2026_lima_neotropical_ento`)
   - **zenodo_id**: deixe **vazio**
   - **publish**: `false` (recomendado — revise antes de publicar)
3. Execute o workflow
4. Anote o **Deposit ID** exibido no sumário do job
5. Acesse `https://zenodo.org/deposit/<DEPOSIT_ID>`, revise e publique manualmente

> Após publicar, atualize o `CITATION.cff` e o `README.md` do projeto com o DOI gerado.

### Nova versão de depósito existente

1. Vá para **Actions → Zenodo Deposit → Run workflow**
2. Preencha:
   - **project**: nome da pasta
   - **zenodo_id**: ID do depósito existente (ex: `1234567`)
   - **publish**: `true` ou `false`

> O ID do depósito está na URL do registro: `zenodo.org/record/1234567`

---

## Depósito Manual (alternativa)

Se preferir depositar diretamente pelo site:

1. Acesse [zenodo.org/deposit/new](https://zenodo.org/deposit/new)
2. Faça upload de um ZIP da pasta do projeto
3. Preencha os metadados conforme o `.zenodo.json`
4. Clique em **Save** → revise → **Publish**

---

## Badge de DOI

Após publicar, adicione o badge no `README.md` do projeto:

```markdown
[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.XXXXXXX.svg)](https://doi.org/10.5281/zenodo.XXXXXXX)
```

---

## Atualizando Dados (Nova Versão)

1. Faça as alterações na pasta do projeto e commit no GitHub
2. Use o workflow com o `zenodo_id` existente (cria nova versão automaticamente)
3. O DOI conceito permanece; um novo DOI de versão é gerado
4. Atualize o `CHANGELOG.md` do projeto

---

## Estrutura Recomendada por Projeto

```
publications/YYYY_autor_journal/
├── .zenodo.json          # Metadados Zenodo (obrigatório)
├── CITATION.cff          # Citação formal (obrigatório)
├── README.md
├── data/
│   ├── raw/              # Dados brutos (imutáveis)
│   └── processed/
├── scripts/              # Scripts numerados sequencialmente
├── results/              # Figuras e tabelas
└── environment/          # renv.lock / requirements.txt / environment.yml
```
