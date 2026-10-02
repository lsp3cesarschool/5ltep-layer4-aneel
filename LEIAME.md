# 5LTEP-L4 · instância ANEEL (experimento de controle)

[![Tests](https://github.com/lsp3cesarschool/5ltep-layer4-aneel/actions/workflows/tests.yml/badge.svg)](https://github.com/lsp3cesarschool/5ltep-layer4-aneel/actions/workflows/tests.yml) [![Layer 4](https://img.shields.io/endpoint?url=https%3A%2F%2Fraw.githubusercontent.com%2Flsp3cesarschool%2F5ltep-layer4-aneel%2Fmain%2Fdocs%2Fdata%2Fstatus.pt.json)](https://github.com/lsp3cesarschool/5ltep-layer4-aneel/actions/workflows/monitor.yml) [![Cross-check](https://img.shields.io/endpoint?url=https%3A%2F%2Fraw.githubusercontent.com%2Flsp3cesarschool%2F5ltep-layer4-aneel%2Fmain%2Fdocs%2Fdata%2Fstatus-cross-check.pt.json)](https://github.com/lsp3cesarschool/5ltep-layer4-aneel/actions/workflows/cross_check.yml) [![License: MIT](https://img.shields.io/badge/License-MIT-blue.svg)](LICENSE)

[English](README.md) · **Português**

**Camada 4 do 5L-TEP (observabilidade e proveniência) aplicada ao portal de dados abertos da ANEEL, agência reguladora do setor elétrico:
outra instância do [5ltep-layer4](https://github.com/lsp3cesarschool/5ltep-layer4), montada pelo autor como caso de controle do
estudo do IBAMA.**

| Recurso | O que você encontra lá |
|---|---|
| 📊 **Painel** | [lsp3cesarschool.github.io/5ltep-layer4-aneel](https://lsp3cesarschool.github.io/5ltep-layer4-aneel/?lang=pt): mudanças por mês, onde estão os arquivos, últimas mudanças, saúde do monitoramento, todos os conjuntos |
| 📄 **Registro de mudanças** | [`changes.md`](changes.md) (em inglês): cada mudança detectada em palavras simples, reconstruído a cada ciclo |
| 🔗 **Registros de proveniência** | [`provenance_logs/`](provenance_logs/): uma cadeia W3C PROV-DM (JSON-LD) somente por acréscimo, por conjunto |
| 🏛️ **Instância principal** | [5ltep-layer4](https://github.com/lsp3cesarschool/5ltep-layer4): IBAMA, e a documentação completa |
| 🔁 **Outro controle** | [5ltep-layer4-recife](https://github.com/lsp3cesarschool/5ltep-layer4-recife): o portal do Recife |

> **Situação: demonstração de pesquisa.** Este repositório não é operado, afiliado ou endossado pela ANEEL; ele apenas lê os dados abertos da ANEEL. Ele mostra que o kit pode ser
> reutilizado em outro portal e não pressupõe que o publicador vá revisar seus resultados ou adotá-lo.
> Os alertas chegam ao mantenedor deste repositório, não ao publicador.

## Caso de uso em um parágrafo

A ANEEL publica no seu portal CKAN os dados do setor elétrico que regula: tarifas, geração,
indicadores de qualidade da distribuição, autos de infração e outros, muitos atualizados todo mês.
Suponha uma analista que baixa todo mês um conjunto de tarifas ou de qualidade e compara os meses:
se um arquivo for substituído, levado para outro servidor ou editado sem nova data de modificação,
a comparação mistura duas versões sem aviso. Esta instância lê os metadados de todos os conjuntos
da ANEEL a cada seis horas e registra cada mudança como uma entidade W3C PROV-DM ligada à versão
anterior, para que a analista veja quando um conjunto mudou, como, e se a mudança foi datada.

## Por que um experimento de controle

O kit da Camada 4 foi construído e avaliado no portal do IBAMA. A ANEEL é uma agência reguladora federal, de outro setor
(cerca de 70 conjuntos; um ciclo leva bem menos de um minuto). Este repositório roda **o mesmo código**, seguindo os passos de *Monitorando outro
portal CKAN* do README principal: só o `portal.json` (a URL do portal) e os textos deste README
mudaram. Onde a ANEEL publica de outro jeito que o IBAMA, a diferença aparece nos registros de
mudança, não no código. O monitoramento começa com uma linha de base: o primeiro ciclo não registra
mudança, só o estado com que todos os ciclos seguintes são comparados.

## O que mudou em relação à instância principal

| Arquivo | Mudança |
|---|---|
| `portal.json` | `portal_url` = `https://dadosabertos.aneel.gov.br` |
| `README.md`, `LEIAME.md`, `CITATION.cff` | este texto e a citação deste repositório |

Todo o resto é o código do `5ltep-layer4` no commit `469576e`
([469576e74bb9df39ce50e62b8347e245169345a7](https://github.com/lsp3cesarschool/5ltep-layer4/commit/469576e74bb9df39ce50e62b8347e245169345a7)). Os snapshots, os registros de
proveniência, o registro de mudanças e os dados do painel são gravados aqui pelos workflows.

## Como rodar, e como adaptar de novo

O workflow *5L-TEP Layer 4 Monitoring Workflow* roda a cada seis horas e pode ser iniciado à mão
(*Actions → Run workflow*); a verificação cruzada roda uma vez por dia. Localmente:

```bash
pip install -r requirements.txt
python main.py --max-datasets 5 --dry-run
```

Para apontar para outro portal CKAN, mude `portal_url` no `portal.json`; veja o README principal.

## Reprodutibilidade

Cada registro de proveniência traz a impressão digital da versão do conjunto que descreve, a
execução que a observou e o commit do código que rodou (`5ltep:commitSha`). O código é o commit de
origem acima; todo o resto é gravado pelos workflows, de modo que o histórico deste repositório é o
histórico do portal tal como observado.

## Limitações

As limitações da instância principal valem aqui. O portal da ANEEL é maior em arquivos do que em conjuntos: um conjunto com muitos recursos gera descrições de mudança longas quando todos são substituídos de uma vez.

## Documentação e referências

A documentação completa (taxonomia de mudanças, mapeamento PROV-DM, modelo de dois agentes,
verificação cruzada, configuração, avaliação e referências) está no
[repositório principal](https://github.com/lsp3cesarschool/5ltep-layer4/blob/main/LEIAME.md).

## Licença

MIT para o código ([LICENSE](LICENSE)). Cada conjunto da ANEEL declara sua licença no portal; este repositório guarda só snapshots de metadados e registros de proveniência derivados deles.
