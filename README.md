# GEO — QGIS MCP (Model Context Protocol)

Repositório para centralizar referências, estudos e o desenvolvimento de soluções que integram o **QGIS** com o **Model Context Protocol (MCP)**, permitindo que agentes de IA (Claude, Copilot CLI, etc.) operem o QGIS de forma programática: criação e manipulação de projetos, camadas, geoprocessamento via Processing Toolbox, estilização, edição de feições, geração de mapas e muito mais.

## Contexto

Este repositório apoia o desenvolvimento de soluções geoespaciais corporativas para saneamento (DAE Jundiaí). Com o licenciamento do ArcGIS Enterprise temporariamente indisponível, o QGIS passa a ser a plataforma primária de desenvolvimento no curto prazo — e a integração com MCP abre caminho para automação assistida por IA em tarefas como:

- Estruturação e validação de bases geoespaciais (redes de água/esgoto, cadastro técnico, UCs, bacias, recursos hídricos)
- Prototipação rápida de ferramentas e fluxos de geoprocessamento em PyQGIS
- Geração de mapas e materiais visuais para apresentações e convencimento interno sobre a necessidade de uma equipe de SIG mais robusta
- Exploração de modelos analíticos, automações e integrações de dados

## O que é o QGIS MCP

O [Model Context Protocol (MCP)](https://modelcontextprotocol.io) é um padrão aberto que permite a um agente de IA descobrir e chamar "ferramentas" (tools) expostas por um servidor externo. Aplicado ao QGIS, a arquitetura típica é:

```
Agente de IA (Claude, Copilot CLI, ...)
        │  MCP (stdio / SSE)
        ▼
Servidor MCP (Python, fora do QGIS)
        │  socket TCP
        ▼
Plugin QGIS (roda dentro do QGIS, escuta comandos)
        │  API PyQGIS
        ▼
QGIS (projetos, camadas, processing, canvas...)
```

O plugin dentro do QGIS abre um servidor de socket não bloqueante; o servidor MCP traduz as chamadas do agente em comandos PyQGIS e as envia por esse socket. Isso permite que qualquer cliente compatível com MCP controle o QGIS sem modificações no agente.

## Referências

| # | Referência | Descrição |
|---|---|---|
| 1 | [jjsantos01/qgis_mcp](https://github.com/jjsantos01/qgis_mcp) | Implementação original/mais conhecida. Plugin QGIS + servidor MCP em Python (inspirado no BlenderMCP). ~14 ferramentas: projetos, camadas, execução de algoritmos do Processing, código PyQGIS arbitrário, renderização. |
| 2 | [nkarasiak/qgis-mcp](https://github.com/nkarasiak/qgis-mcp) | Fork/evolução com escopo bem mais amplo: 118 ferramentas (ou 27 agrupadas), suporte a múltiplos clientes MCP simultâneos, autenticação opcional por token, SQL, estilização avançada (categorizado/graduado), layouts e atlas. |
| 3 | [Vídeo (YouTube)](https://www.youtube.com/watch?v=4CLuPG8xBGg) | Demonstração prática de uso do QGIS MCP. |
| 4 | [QGIS MCP Plugin — repositório oficial de plugins](https://plugins.qgis.org/plugins/qgis_mcp_plugin/) | Página de distribuição do plugin no QGIS Plugin Repository, instalável via Gerenciador de Complementos do QGIS. |

Notas mais detalhadas e uma comparação de arquitetura entre as referências 1 e 2 estão em [`docs/referencias-qgis-mcp.md`](docs/referencias-qgis-mcp.md).

## Estrutura do repositório

```
GEO/
├── README.md
├── LICENSE
├── docs/
│   └── referencias-qgis-mcp.md   # notas e comparação das referências
└── examples/
    └── README.md                 # casos de uso e prompts para o contexto DAE Jundiaí
```

## Roadmap

- [ ] Instalar e testar localmente o plugin `qgis_mcp` (jjsantos01) com um agente MCP
- [ ] Avaliar `nkarasiak/qgis-mcp` como alternativa mais completa
- [ ] Mapear casos de uso prioritários (cadastro técnico, redes, geoprocessamento em lote)
- [ ] Documentar fluxos de automação PyQGIS via MCP para tarefas recorrentes
- [ ] Registrar aprendizados e riscos (segurança, execução arbitrária de código, ambiente corporativo)

## Licença

Código próprio deste repositório sob licença MIT ([LICENSE](LICENSE)). Qualquer código adaptado do plugin QGIS de referência deve respeitar a licença GPL v2+ do projeto original; servidores MCP próprios podem ser licenciados como MIT, seguindo o mesmo modelo de licenciamento dual adotado pelas referências.
