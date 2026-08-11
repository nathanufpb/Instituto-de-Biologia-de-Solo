# Instituto de Biologia do Solo — Coleção de Datasets e Publicações Científicas

[![DOI](https://zenodo.org/badge/DOI/10.5281/zenodo.PENDENTE.svg)](https://doi.org/10.5281/zenodo.PENDENTE)

Este é o **registro guarda-chuva** (umbrella record) do Instituto de Biologia do Solo (IBS) no Zenodo. Ele não contém dados próprios — sua função é **agregar e referenciar** todos os datasets científicos publicados pelo instituto, fornecendo um ponto de entrada institucional único para descoberta e citação.

## Datasets referenciados

| Projeto | DOI | Descrição |
|---------|-----|-----------|
| [2026_lima_neotropical_ento](../publications/2026_lima_neotropical_ento/) | [10.5281/zenodo.21881749](https://doi.org/10.5281/zenodo.21881749) | Taxonomia codificada de *Mucrosomia* (Collembola: Isotomidae) |
| [2026_Zeppelini_troglobius](../publications/2026_Zeppelini_troglobius/) | [10.5281/zenodo.21890449](https://doi.org/10.5281/zenodo.21890449) | Redescoberta e redescrição de *Troglobius brasiliensis* (Collembola: Paronellidae) |

## Como funciona a relação entre os registros

- Este registro guarda-chuva referencia cada dataset via `related_identifiers` com relação **`hasPart`**
- Cada dataset individual referencia de volta este registro via relação **`isPartOf`**
- Essa hierarquia é reconhecida por sistemas de indexação como DataCite e OpenAIRE, permitindo navegação entre o "todo" institucional e as "partes" (cada publicação)

## Adicionando um novo dataset à coleção

Ao publicar um novo projeto em `publications/`:

1. Publique o DOI do novo dataset normalmente (ver [docs/ZENODO_INTEGRATION.md](../docs/ZENODO_INTEGRATION.md))
2. Adicione uma entrada `hasPart` neste `.zenodo.json` apontando para o novo DOI
3. Adicione uma entrada `isPartOf` no `.zenodo.json` do novo projeto apontando para o DOI deste registro guarda-chuva
4. Crie uma nova versão deste registro guarda-chuva (`draft_id`/`zenodo_id` no workflow) para refletir a atualização

## Licença

[CC BY 4.0](../LICENSE-CC-BY-4.0.md)

## Como Citar

Cite os datasets individuais listados acima. Este registro serve apenas como agregador institucional.
