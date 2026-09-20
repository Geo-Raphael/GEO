# Referências — QGIS + MCP

Notas de estudo sobre as implementações existentes de integração entre QGIS e o Model Context Protocol (MCP), usadas como ponto de partida para o desenvolvimento neste repositório.

## 1. jjsantos01/qgis_mcp

- Repositório: https://github.com/jjsantos01/qgis_mcp
- Arquitetura: plugin QGIS (servidor de socket dentro do QGIS) + servidor MCP em Python, comunicação bidirecional por socket.
- Inspiração declarada: BlenderMCP (Siddharth Ahuja), adaptando o mesmo padrão arquitetural para o QGIS.
- Ferramentas (14+): criação/carregamento de projeto, gestão de arquivos, adicionar/remover camadas vetoriais e raster, execução de algoritmos via Processing Toolbox, execução de código PyQGIS arbitrário, renderização do mapa e obtenção de feições.
- Requisitos: QGIS 3.x (testado em 3.22), Python 3.10+, gerenciador de pacotes `uv`, Claude Desktop.
- Instalação: clonar o repositório, copiar a pasta do plugin para o diretório de plugins do QGIS, configurar `claude_desktop_config.json` apontando para o servidor MCP.
- Uso: iniciar o plugin no QGIS, clicar em "Start Server", e usar as ferramentas expostas no cliente (ícone de martelo no Claude Desktop).

## 2. nkarasiak/qgis-mcp

- Repositório: https://github.com/nkarasiak/qgis-mcp
- Arquitetura: `Agente de IA ↔ Servidor MCP (FastMCP) ↔ socket TCP ↔ Plugin QGIS (QTimer, não bloqueante)`.
- Diferenciais em relação à referência 1:
  - Escopo muito maior: 118 ferramentas granulares (redutíveis a ~27 ferramentas agrupadas, para reduzir custo de contexto do agente).
  - Suporte a múltiplos clientes/agentes MCP simultâneos, não vinculado a um vendor específico (funciona com Claude Code, Copilot CLI, etc.).
  - Autenticação opcional por token — relevante para uso em máquinas compartilhadas/ambiente corporativo.
  - Cobertura funcional mais ampla: CRS, estilização categorizada/graduada e simbologia, edição de feições (criar/atualizar/excluir), seleções, cálculo de campos, execução de algoritmos e modelos em lote, consultas SQL, análise espacial, geração de atlas e layouts.
- Requisitos: QGIS 3.28+, gerenciador `uv` (instalação do servidor via `uvx` apontando para o repositório, sem necessidade de clonar).
- Licenciamento dual: plugin QGIS sob GPL v2+ (herdado do próprio QGIS), servidor MCP sob MIT.

## Comparação rápida

| Aspecto | jjsantos01/qgis_mcp | nkarasiak/qgis-mcp |
|---|---|---|
| Nº de ferramentas | ~14 | 118 (ou 27 agrupadas) |
| Múltiplos clientes MCP | Não (foco em Claude Desktop) | Sim (qualquer agente MCP) |
| Autenticação | Não mencionada | Token opcional |
| QGIS mínimo | 3.22 (3.x) | 3.28 |
| Instalação do plugin | Cópia manual da pasta | Gerenciador de Complementos do QGIS |
| Instalação do servidor | Clonar repositório | `uvx` direto do GitHub, sem clonar |
| Licença | Não detalhada nas notas iniciais | Plugin GPL v2+ / servidor MIT |

## 3. Vídeo de demonstração

- https://www.youtube.com/watch?v=4CLuPG8xBGg
- Demonstração prática do fluxo de uso do QGIS MCP (a ser complementada com anotações após revisão).

## 4. QGIS Plugin Repository — qgis_mcp_plugin

- https://plugins.qgis.org/plugins/qgis_mcp_plugin/
- Página oficial de distribuição do plugin no repositório de plugins do QGIS, permitindo instalação direta via **Complementos → Gerenciar e Instalar Complementos** dentro do QGIS (sem necessidade de cópia manual de arquivos).

## Pontos de atenção para uso corporativo (DAE Jundiaí)

- A ferramenta de "execução de código PyQGIS arbitrário" exposta ao agente de IA é poderosa, mas representa um vetor de risco (execução de código não sandboxado) — avaliar uso apenas em ambiente local/controlado, nunca exposto em rede sem autenticação.
- Preferir, sempre que possível, ferramentas específicas (camadas, processing, estilização) em vez de execução de código livre, para reduzir superfície de risco.
- Documentar quais versões de QGIS estão homologadas internamente antes de adotar qualquer uma das referências em fluxo de trabalho real.
