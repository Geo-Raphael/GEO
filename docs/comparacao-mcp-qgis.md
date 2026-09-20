# Comparação: jjsantos01/qgis_mcp vs nkarasiak/qgis-mcp

Status: **rascunho inicial**, baseado na leitura das páginas dos repositórios (README/descrição geral). Ainda **não** inclui leitura linha a linha do código-fonte — isso é o próximo passo do roadmap (item 1).

## Visão geral

| | [jjsantos01/qgis_mcp](https://github.com/jjsantos01/qgis_mcp) | [nkarasiak/qgis-mcp](https://github.com/nkarasiak/qgis-mcp) |
|---|---|---|
| Popularidade (na data desta nota) | ~1.1k stars, 172 forks | ~313 stars, 77 forks |
| Origem | Inspirado no projeto BlenderMCP | Reimplementação/fork mais recente, com escopo bem ampliado |
| Cliente MCP alvo | Claude Desktop (config via `claude_desktop_config.json`) | Agnóstico de cliente: Claude Code, Codex CLI, Gemini CLI, GitHub Copilot CLI, VS Code, Cursor, Windsurf, Zed, LM Studio, opencode, Hermes, etc. |
| Requisito de QGIS | 3.X (testado em 3.22+) | 3.28+ |
| Gerenciador de dependências | `uv` | `uv` |
| Licença | Não especificada claramente na página (verificar no repositório) | Dual: plugin QGIS em GPLv2+, servidor MCP em MIT |

## Arquitetura

Ambos seguem o mesmo padrão geral (também usado pelo BlenderMCP):

```
Agente de IA (Claude etc.) ⇄ Servidor MCP (processo externo) ⇄ Socket TCP ⇄ Plugin QGIS (servidor socket dentro do QGIS) ⇄ API PyQGIS
```

- O **plugin QGIS** roda dentro do próprio QGIS e abre um servidor de socket (não bloqueante, no caso do nkarasiak) para receber comandos.
- O **servidor MCP** roda como processo externo, implementa o protocolo MCP e traduz chamadas de ferramentas em mensagens enviadas ao socket do plugin.
- nkarasiak/qgis-mcp explicita o uso de **FastMCP** para implementar o servidor MCP.

## Ferramentas / comandos expostos

### jjsantos01/qgis_mcp

- Verificação de conectividade (ping)
- Gerenciamento de projetos (criar, carregar, salvar)
- Manipulação de camadas (adicionar, remover, obter informações)
- Execução de algoritmos de processing
- Execução de código PyQGIS arbitrário
- Renderização de mapas
- Zoom e consulta de features

### nkarasiak/qgis-mcp

Conjunto bem mais amplo — **118 ferramentas granulares** (ou 27 agrupadas em "modo compound"):

| Categoria | Exemplos |
|---|---|
| Projeto | carregar, criar, salvar projetos |
| Camadas | adicionar, remover, visibilidade, CRS |
| Feições | consultar, adicionar, atualizar, deletar, selecionar |
| Campos | adicionar, deletar, renomear, calculadora de campos |
| Edição | iniciar, confirmar, desfazer edições |
| Estilos | categorizado, graduado, pseudocor, hillshade |
| Processamento | executar algoritmos, lotes, modelos |
| Renderização | gerar mapas, capturas de tela, 2D/3D |
| Layouts/Atlas | criar, exportar composições |
| Consultas | SQL, expressões, identificar feições |

Recursos adicionais do nkarasiak/qgis-mcp:
- Modo multi-instância (controlar várias janelas QGIS a partir de um único servidor);
- Autenticação por token (relevante para máquinas/servidores compartilhados — pode importar para um ambiente corporativo como o da DAE);
- Logging e modo "offline-first" com caching.

## Primeira leitura para o contexto DAE Jundiaí

- O **execução de código PyQGIS arbitrário** (presente em ambos, mas explícito no jjsantos01) é o recurso de maior risco e maior flexibilidade — precisa de atenção a segurança/sandboxing antes de qualquer uso além do laboratório local.
- O catálogo amplo do nkarasiak (edição de feições/campos, estilos, consultas SQL/expressões) parece mais alinhado a fluxos reais de cadastro técnico e gestão de redes/ativos do que o conjunto mais enxuto do jjsantos01.
- A autenticação por token do nkarasiak é relevante se algum dia isso rodar em uma máquina compartilhada da equipe, e não só na estação local.
- Como a licença ArcGIS Enterprise/Utility Network ainda não está liberada, este laboratório QGIS é também uma forma de gerar uma prova de conceito visualmente convincente (dashboards, automações) para apoiar o convencimento interno sobre a necessidade de uma equipe de SIG mais robusta.

## Pendências

- [ ] Clonar os dois repositórios e ler o código-fonte do plugin e do servidor MCP de cada um.
- [ ] Instalar e rodar as duas implementações localmente (ver `/experiments`).
- [ ] Verificar a página oficial do plugin QGIS (`plugins.qgis.org/plugins/qgis_mcp_plugin`) — não foi possível acessar este domínio a partir deste ambiente (bloqueado pela política de rede/proxy de saída). Conferir manualmente qual implementação está publicada ali, versão e forma de instalação via QGIS Plugin Manager.
- [ ] Assistir ao vídeo de referência e extrair passo a passo prático de instalação/uso: https://www.youtube.com/watch?v=4CLuPG8xBGg
- [ ] Definir critérios objetivos de escolha (segurança, cobertura de ferramentas, manutenção ativa, licença) para decidir se seguimos com uma das duas implementações como base ou desenvolvemos algo próprio do zero.
