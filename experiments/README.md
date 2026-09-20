# /experiments

Primeiros testes de integração MCP + QGIS. Cada experimento fica em sua própria subpasta, numerada e com um nome curto descritivo.

## Convenção

```
experiments/
  001-jjsantos01-setup/     # instalação e teste local de jjsantos01/qgis_mcp
  002-nkarasiak-setup/      # instalação e teste local de nkarasiak/qgis-mcp
  003-caso-de-uso-saneamento/  # primeiro protótipo de caso de uso próprio
```

Cada subpasta de experimento deve conter, quando aplicável:

- `README.md` — o que o experimento testa, passos de instalação/execução, resultado observado (incluindo prints ou logs relevantes) e conclusão (funcionou / não funcionou / observações).
- Scripts, arquivos de configuração (`claude_desktop_config.json` de exemplo sem credenciais, etc.) e código de prova de conceito.
- **Nunca** commitar credenciais, tokens de API ou caminhos absolutos sensíveis do ambiente local/corporativo.

## Próximos experimentos (ligados ao roadmap)

1. **001 — Rodar `jjsantos01/qgis_mcp` localmente**: instalar plugin no QGIS, subir o servidor MCP, conectar a um cliente MCP e validar comandos básicos (ping, listar camadas, executar PyQGIS simples).
2. **002 — Rodar `nkarasiak/qgis-mcp` localmente**: mesma validação básica, além de explorar recursos extras (edição de feições, campos, estilos, consultas).
3. **003 — Caso de uso de saneamento**: protótipo de um fluxo real (ex.: consulta espacial sobre rede de água/esgoto, apoio a cadastro técnico, ou automação de mapa/relatório) usando a implementação escolhida como base.

Os resultados e aprendizados de cada experimento devem alimentar `/docs/comparacao-mcp-qgis.md` e `/docs/decisoes.md`.
