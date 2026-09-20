# GEO — Laboratório MCP + QGIS

Repositório de laboratório para estudar e desenvolver a integração entre **MCP (Model Context Protocol)** e **QGIS**, no contexto da minha atuação como Analista de Geoprocessamento e Soluções Geoespaciais na **DAE Jundiaí** (saneamento e recursos hídricos).

> Nota: este repositório também é o repositório de perfil do GitHub (`Geo-Raphael/GEO`), mas passa a ser usado como espaço de trabalho técnico para este projeto.

## Objetivo

Hoje a licença ArcGIS disponível é apenas **Creator** (sem Enterprise/Utility Network liberado), então o trabalho de automação e IA aplicada a GIS precisa começar pelo **QGIS**, que é open source e permite experimentação livre com plugins e integrações.

O MCP (Model Context Protocol) permite que um agente de IA (Claude, por exemplo) opere ferramentas de um software através de um servidor padronizado. Aplicado ao QGIS, isso abre a possibilidade de:

- Automatizar tarefas repetitivas de geoprocessamento via linguagem natural;
- Prototipar assistentes que auxiliem em análises espaciais, cadastro técnico, gestão de redes e ativos de saneamento;
- Testar um caminho de "IA aplicada a GIS" que não depende de licenciamento ArcGIS Enterprise, servindo também de prova de conceito para justificar investimento futuro em uma equipe de SIG mais robusta.

Este repositório serve como **laboratório de estudo e desenvolvimento**: entender implementações existentes de MCP para QGIS, testá-las localmente e, a partir delas, conceber uma integração ou plugin próprio voltado a casos de uso de saneamento.

## Referências de partida

| Referência | O que é |
|---|---|
| [jjsantos01/qgis_mcp](https://github.com/jjsantos01/qgis_mcp) | Implementação original/mais popular (~1.1k stars). Plugin QGIS que sobe um servidor via socket dentro do QGIS + um servidor MCP externo que traduz chamadas do agente de IA (ex.: Claude Desktop) em comandos para o QGIS. Inspirado no projeto BlenderMCP. Expõe comandos como ping, criar/carregar/salvar projeto, manipular camadas, rodar algoritmos de processing, executar código PyQGIS arbitrário, renderizar mapas e consultar features. |
| [nkarasiak/qgis-mcp](https://github.com/nkarasiak/qgis-mcp) | Fork/reimplementação mais recente e ativa (~313 stars), com arquitetura semelhante (Agente de IA ↔ Servidor MCP/FastMCP ↔ socket TCP ↔ Plugin QGIS ↔ PyQGIS), porém com um catálogo de ferramentas muito mais amplo (118 ferramentas granulares, ou 27 agrupadas em "modo compound"): edição de feições, campos, calculadora de campos, estilos (categorizado, graduado, pseudocor, hillshade), layouts/atlas, consultas SQL/expressões, múltiplas instâncias de QGIS, autenticação por token e logging. Licenciamento dual (plugin GPLv2+, servidor MIT). Compatível com múltiplos clientes MCP (Claude Code, Cursor, Windsurf, VS Code, etc.), não só Claude Desktop. |
| [Vídeo: demonstração MCP + QGIS](https://www.youtube.com/watch?v=4CLuPG8xBGg) | Referência em vídeo mostrando a integração em uso — usar como guia de instalação/demo prática. |
| [plugins.qgis.org/plugins/qgis_mcp_plugin](https://plugins.qgis.org/plugins/qgis_mcp_plugin/) | Página do plugin no repositório oficial de plugins do QGIS. **Não verificado ainda** — o acesso a este domínio está bloqueado pela política de rede deste ambiente; conferir manualmente a que implementação (jjsantos01, nkarasiak ou outra) essa listagem corresponde, versão publicada e forma de instalação via QGIS Plugin Manager. |

## Roadmap inicial

1. **Estudar as duas implementações MCP existentes** — ler o código-fonte de `qgis_mcp` (jjsantos01) e `qgis-mcp` (nkarasiak), entender arquitetura, protocolo de mensagens e dependências. Registrar achados em `/docs`.
2. **Rodar localmente** — instalar QGIS + plugin + servidor MCP de cada implementação em ambiente de teste, validar a conexão com um cliente MCP (Claude Desktop/Claude Code) e confirmar comandos básicos funcionando (ping, listar camadas, executar PyQGIS simples).
3. **Mapear ferramentas/comandos expostos ao QGIS** — construir um inventário comparativo completo (não só o resumo inicial) das ferramentas/comandos de cada implementação, avaliando quais são realmente úteis para os fluxos de trabalho da DAE Jundiaí.
4. **Desenvolver caso de uso próprio para saneamento** — a partir do entendimento acumulado, prototipar uma integração/plugin MCP própria (ou uma extensão de uma das referências) aplicada a um problema real de saneamento: por exemplo, consultas espaciais sobre rede de água/esgoto, apoio a cadastro técnico, ou automação de relatórios/mapas para apresentações.

## Estrutura do repositório

- [`/docs`](./docs) — anotações de estudo, comparação entre `jjsantos01/qgis_mcp` e `nkarasiak/qgis-mcp`, e registro de decisões técnicas.
- [`/experiments`](./experiments) — primeiros testes de integração (instalação, execução local, scripts de prova de conceito).

## Contexto profissional

Atuação como Analista de Geoprocessamento e Soluções Geoespaciais na DAE Jundiaí, cobrindo análise geoespacial, desenvolvimento de soluções (Python, automação, ferramentas GIS), engenharia aplicada (redes de água/esgoto, cadastro técnico, ativos) e arquitetura/gestão GIS. Este laboratório de MCP + QGIS é parte da dimensão de desenvolvimento de soluções e inovação tecnológica desse perfil.
