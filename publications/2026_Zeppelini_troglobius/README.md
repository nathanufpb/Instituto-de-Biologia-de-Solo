# Filogenia Molecular de *Troglobius brasiliensis* (Collembola: Paronellidae)

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.XXXXXXX.svg)](https://doi.org/10.5281/zenodo.XXXXXXX)

Dados, scripts e materiais suplementares do artigo:

> Zeppelini, D. et al. (2026). *Título do artigo*. *Periódico*. https://doi.org/[A PREENCHER]

## Descrição

Este repositório contém os dados moleculares e scripts utilizados para a análise filogenética de *Troglobius brasiliensis*, uma espécie troglobítica de Collembola (Paronellidae), baseada no gene COI (citocromo oxidase I). A árvore de máxima verossimilhança foi inferida com 54 sequências de Paronellidae obtidas do GenBank, incluindo uma nova sequência gerada neste estudo.

## Conteúdo

```
2026_Zeppelini_troglobius/
├── scripts/
│   ├── Paronellidae_sequences/         # Sequências COI individuais do GenBank (.fasta)
│   ├── alinhamento_macse_atual.*       # Alinhamentos MACSE (nt, aa, limpo, trimado)
│   ├── alinhamento_macse_atual.partitions.nex.*  # Saídas IQ-TREE (árvore, modelos, suporte)
│   ├── gerar_particoes_codon.py        # Script Python para geração de partições de códons
│   └── macse_v2.07.jar                 # MACSE v2.07 (alinhamento consciente de códons)
├── results/
│   └── figures/
│       └── alinhamento_macse_atual.partitions.nex.contree.jpg  # Árvore ML com suporte UFBoot
└── data/                               # Dados brutos e processados (a preencher)
```

## Métodos

| Etapa | Ferramenta | Versão |
|-------|-----------|--------|
| Alinhamento | MACSE | v2.07 |
| Seleção de modelo | ModelTest-NG (via IQ-TREE) | — |
| Inferência filogenética | IQ-TREE | — |
| Partições de códons | `gerar_particoes_codon.py` | — |

**Suporte de ramos**: UFBoot (ultrafast bootstrap, 1000 réplicas)

## Sequências

- **Gene**: COI (citocromo oxidase subunidade I)
- **Total**: 54 sequências de Paronellidae
- **Fonte**: GenBank + 1 sequência nova de *Troglobius brasiliensis*
- **Acessions GenBank**: GQ374044–GQ374058, KJ716828, KM978343–KM978406, KY052898–KY052899, MG036988, MG318457, MK431896, MK510939–MK510940, MT357591–MT357642

## Como Reproduzir

```bash
# 1. Alinhar sequências com MACSE
java -jar macse_v2.07.jar -prog alignSequences \
  -seq [arquivo_entrada.fasta] \
  -out_NT alinhamento_macse_atual.macse.nt.fasta \
  -out_AA alinhamento_macse_atual.macse.aa.fasta

# 2. Gerar partições de códons
python gerar_particoes_codon.py alinhamento_macse_atual.macse.nt.clean.fasta

# 3. Inferência filogenética com IQ-TREE
iqtree2 -s alinhamento_macse_atual.macse.nt.clean.trimmed.fasta \
  -p alinhamento_macse_atual.partitions.nex \
  -B 1000 -T AUTO
```

## Licença

Dados: [CC0 1.0](../../LICENSE-CC0.md) | Scripts: [CC BY 4.0](../../LICENSE-CC-BY-4.0.md)

## Como Citar

Ver `CITATION.cff` nesta pasta ou o DOI Zenodo no badge acima.

## Estrutura do Projeto

```
EXEMPLO_2024_silva_ecology/
├── README.md                   # Este arquivo
├── data/
│   ├── raw/                    # Dados brutos originais
│   │   ├── field_data.csv
│   │   ├── soil_samples.csv
│   │   └── specimen_counts.csv
│   ├── processed/              # Dados processados
│   │   ├── community_matrix.csv
│   │   ├── environmental_vars.csv
│   │   └── diversity_metrics.csv
│   └── metadata/               # Metadados do projeto
│       ├── metadata.json
│       └── data_dictionary.csv
├── scripts/                    # Scripts de análise
│   ├── 01_data_cleaning.R
│   ├── 02_diversity_analysis.R
│   ├── 03_statistical_models.R
│   └── 04_figures_generation.R
├── mapas/                      # Mapas e dados espaciais
│   ├── site_locations.shp
│   ├── fragments_boundaries.shp
│   ├── mapa_area_estudo.pdf
│   └── mapa_pontos_coleta.pdf
├── imagens-pranchas/           # Pranchas de figuras e fotos
│   ├── prancha_especies.pdf
│   ├── fotos_campo/
│   └── fotos_laboratorio/
├── manuscritos/                # Versões do manuscrito
│   ├── v1_submitted.docx
│   ├── v2_revised.docx
│   ├── final_accepted.pdf
│   └── supplementary_material.pdf
├── taxonomia-delta/            # Dados taxonômicos (sistema DELTA)
│   ├── chars                   # Arquivo de caracteres
│   ├── items                   # Arquivo de táxons
│   ├── specs                   # Especificações
│   ├── intkey.ink             # Chave interativa
│   └── descriptions.txt        # Descrições geradas
├── results/                    # Resultados
│   ├── figures/
│   │   ├── figure1_map.pdf
│   │   ├── figure2_diversity.pdf
│   │   └── figure3_ordination.pdf
│   ├── tables/
│   │   ├── table1_sites.csv
│   │   └── table2_models.csv
│   └── supplementary/
│       └── tableS1_species_list.csv
├── docs/                       # Documentação
│   ├── methods_extended.md
│   ├── analysis_notes.md
│   └── field_protocol.md
└── environment/                # Ambiente reprodutível
    ├── renv.lock
    ├── sessionInfo.txt
    └── system_info.txt
```

## Resumo do Projeto

Este estudo investigou padrões de diversidade de fauna de solo em fragmentos de Mata Atlântica no estado de São Paulo, Brasil. Foram amostrados 20 fragmentos florestais ao longo de um gradiente de tamanho e isolamento.

### Objetivos

1. Caracterizar a composição de espécies de fauna de solo
2. Avaliar efeitos de tamanho e isolamento de fragmentos
3. Identificar grupos indicadores de qualidade ambiental

### Principais Resultados

- 150 espécies identificadas
- Riqueza correlacionada com tamanho do fragmento
- Grupos específicos sensíveis ao isolamento

## Como Reproduzir as Análises

### Requisitos

- R versão 4.3.0 ou superior
- RStudio (opcional mas recomendado)
- Pacotes R listados em `environment/renv.lock`

### Passo a Passo

1. **Clone o repositório**
   ```bash
   git clone https://github.com/nathanufpb/Instituto-de-Biologia-de-Solo.git
   cd Instituto-de-Biologia-de-Solo/publications/EXEMPLO_2024_silva_ecology
   ```

2. **Restaure o ambiente R**
   ```r
   install.packages("renv")
   renv::restore()
   ```

3. **Execute os scripts em ordem**
   ```r
   source("scripts/01_data_cleaning.R")
   source("scripts/02_diversity_analysis.R")
   source("scripts/03_statistical_models.R")
   source("scripts/04_figures_generation.R")
   ```

4. **Verifique os resultados**
   - Figuras estarão em `results/figures/`
   - Tabelas em `results/tables/`

## Dados

### Dados Brutos

Localizados em `data/raw/`:

- **field_data.csv**: Dados de campo (datas, coordenadas, condições)
- **soil_samples.csv**: Análises de solo (pH, matéria orgânica, textura)
- **specimen_counts.csv**: Contagens de espécimes por amostra

### Dados Processados

Localizados em `data/processed/`:

- **community_matrix.csv**: Matriz de abundância espécie × sítio
- **environmental_vars.csv**: Variáveis ambientais padronizadas
- **diversity_metrics.csv**: Índices de diversidade calculados

### Metadados

Localizados em `data/metadata/`:

- **metadata.json**: Metadados completos do projeto seguindo padrão institucional
- **data_dictionary.csv**: Dicionário de dados com descrição de todas as variáveis

## Mapas (`/mapas`)

Contém todos os dados espaciais e mapas do projeto:

### Shapefiles
- **site_locations.shp**: Pontos de coleta com coordenadas
- **fragments_boundaries.shp**: Limites dos fragmentos florestais

### Mapas Finais
- **mapa_area_estudo.pdf**: Mapa da área de estudo (para publicação)
- **mapa_pontos_coleta.pdf**: Mapa com localização das coletas

**Software usado**: QGIS 3.28, R (pacotes: sf, tmap, ggplot2)

## Imagens e Pranchas (`/imagens-pranchas`)

### Pranchas de Figuras
- **prancha_especies.pdf**: Prancha com fotos das espécies principais
- Figuras compostas para material suplementar

### Fotos de Campo
Pasta `fotos_campo/` contém:
- Fotos dos sítios de coleta
- Habitat e vegetação
- Processo de coleta

### Fotos de Laboratório
Pasta `fotos_laboratorio/` contém:
- Fotos dos espécimes
- Estruturas diagnósticas
- Material preservado

**Formato**: JPEG (alta qualidade, 300 DPI)  
**Nomenclatura**: `YYYY-MM-DD_local_tipo_sequencia.jpg`

## Manuscritos (`/manuscritos`)

Histórico de versões do manuscrito:

| Arquivo | Status | Data |
|---------|--------|------|
| v1_submitted.docx | Submetido | 2024-03-01 |
| v2_revised.docx | Revisado após peer review | 2024-04-15 |
| final_accepted.pdf | Versão final aceita | 2024-05-01 |
| supplementary_material.pdf | Material suplementar | 2024-05-01 |

**Importante**: Apenas versões finais e aceitas são públicas. Versões intermediárias são para controle interno.

## Taxonomia DELTA (`/taxonomia-delta`)

Sistema DELTA (DEscription Language for TAxonomy) para descrições taxonômicas:

### Arquivos DELTA
- **chars**: Arquivo de caracteres taxonômicos
- **items**: Arquivo de táxons (espécies) descritos
- **specs**: Especificações e configurações
- **intkey.ink**: Chave interativa de identificação
- **descriptions.txt**: Descrições padronizadas geradas

### Uso
```bash
# Gerar descrições
delta intkey.ink

# Criar chave interativa
intkey intkey.ink
```

### Referência
DELTA system: https://www.delta-intkey.com/

**Caracteres codificados**: 45 caracteres morfológicos  
**Táxons incluídos**: 28 espécies de fauna de solo

## Scripts

1. **01_data_cleaning.R**
   - Importa dados brutos
   - Remove outliers
   - Padroniza nomes de espécies
   - Gera dados processados

2. **02_diversity_analysis.R**
   - Calcula índices de diversidade (Shannon, Simpson, riqueza)
   - Análises de rarefação
   - Curvas de acumulação de espécies

3. **03_statistical_models.R**
   - Modelos lineares generalizados
   - Modelos de efeitos mistos
   - Testes de hipóteses

4. **04_figures_generation.R**
   - Gera todas as figuras do manuscrito
   - Figuras suplementares
   - Salva em formato publicável (PDF, 300 DPI)

## Licenças

- **Dados**: CC0 1.0 Universal (domínio público)
- **Código**: MIT License
- **Manuscrito**: Copyright dos autores

## Financiamento

- FAPESP - Processo 2022/12345-6
- CNPq - Processo 123456/2022-1

## Contato

**Autor Correspondente**: João Silva  
**Email**: joao.silva@example.com  
**ORCID**: 0000-0001-2345-6789

## Data de Disponibilização

**Dados brutos**: 15 de março de 2024  
**Manuscrito aceito**: 1 de abril de 2024  
**Publicação online**: 15 de maio de 2024

---

**Nota**: Esta é uma estrutura de EXEMPLO. Substitua por seus dados e informações reais ao criar um novo projeto.
