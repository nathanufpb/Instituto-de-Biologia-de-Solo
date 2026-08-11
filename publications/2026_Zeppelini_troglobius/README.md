# The Elusive *Troglobius brasiliensis* (Collembola: Paronellidae)

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.21890449.svg)](https://doi.org/10.5281/zenodo.21890449)

Dados, scripts e materiais suplementares do artigo:

> Zeppelini, D., de Brito, R. A., Ferreira, A. S., Lopes, B. C. H., Brito, N. P., de Oliveira-Neto, M. A., & de Lima, E. C. A. (em revisão). The elusive *Troglobius brasiliensis* (Collembola: Paronellidae), a critically endangered species rediscovered and redescribed in its habitat and food web.
>
> ⚠️ Artigo em processo de revisão por pares. DOI e dados do periódico serão adicionados após a publicação.

## Descrição

Este repositório contém os dados moleculares e scripts utilizados no estudo da redescoberta e redescrição de *Troglobius brasiliensis*, espécie troglobítica de Collembola (Paronellidae) criticamente ameaçada, em seu hábitat e teia alimentar. A árvore de máxima verossimilhança foi inferida com 54 sequências de Paronellidae obtidas do GenBank, incluindo uma nova sequência gerada neste estudo. Inclui também o conjunto de dados **DELTA** com a taxonomia codificada de Paronellidae.

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
├── taxonomy-delta/
│   └── Paronellidae coded taxonomy.dtz/  # Projeto DELTA (taxonomia codificada de Paronellidae)
└── data/                               # Dados brutos e processados (a preencher)
```

## Métodos

| Etapa | Ferramenta | Versão |
|-------|-----------|--------|
| Alinhamento | MACSE | v2.07 |
| Seleção de modelo | ModelTest-NG (via IQ-TREE) | — |
| Inferência filogenética | IQ-TREE | — |
| Partições de códons | `gerar_particoes_codon.py` | — |
| Taxonomia codificada | DELTA (DEscription Language for TAxonomy) | — |

**Suporte de ramos**: UFBoot (ultrafast bootstrap, 1000 réplicas)

## Sequências

- **Gene**: COI (citocromo oxidase subunidade I)
- **Total**: 54 sequências de Paronellidae
- **Fonte**: GenBank + 1 sequência nova de *Troglobius brasiliensis*
- **Acessions GenBank**: GQ374044–GQ374058, KJ716828, KM978343–KM978406, KY052898–KY052899, MG036988, MG318457, MK431896, MK510939–MK510940, MT357591–MT357642

## Taxonomia DELTA (`taxonomy-delta/`)

O diretório contém o projeto **Paronellidae coded taxonomy.dtz**, criado com o *FreeDELTA Editor (DELTAfree)*, contendo a matriz de caracteres morfológicos codificados para táxons da família Paronellidae, incluindo *Troglobius brasiliensis*.

### Arquivos do projeto DELTA
- `chars` — arquivo de caracteres morfológicos
- `items` — arquivo de táxons codificados
- `specs` — especificações do projeto
- `cnotes` — notas sobre os caracteres
- `tonat` — arquivo de tradução para linguagem natural (geração de descrições)

### Software
Abra o projeto com o [FreeDELTA Editor (DELTAfree)](https://www.delta-intkey.com/).

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

Este depósito é disponibilizado sob [CC BY 4.0](../../LICENSE-CC-BY-4.0.md). As sequências obtidas do GenBank permanecem sujeitas às políticas de acesso público do NCBI.

## Como Citar

Ver `CITATION.cff` nesta pasta ou o DOI Zenodo no badge acima.
