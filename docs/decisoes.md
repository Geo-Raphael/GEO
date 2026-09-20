# Registro de decisões

Formato ADR-lite: **Contexto** → **Decisão** → **Consequências**. Cada entrada é datada e numerada. Novas decisões são adicionadas ao final do arquivo.

---

## 0001 — Início do laboratório MCP + QGIS neste repositório

**Data:** 2026-09-20

**Contexto:** A licença ArcGIS disponível atualmente é apenas Creator, sem Enterprise/Utility Network liberado. Isso limita a exploração de automação/IA aplicada a GIS no ecossistema Esri. QGIS é open source e permite testar plugins e integrações livremente, incluindo integrações com agentes de IA via MCP (Model Context Protocol).

**Decisão:** Usar o repositório `Geo-Raphael/GEO` como laboratório para estudar duas implementações existentes de MCP para QGIS (`jjsantos01/qgis_mcp` e `nkarasiak/qgis-mcp`), compará-las, rodá-las localmente e, a partir disso, desenvolver um caso de uso próprio voltado a saneamento.

**Consequências:**
- O repositório, que antes era apenas o README de perfil do GitHub, passa a ter estrutura de projeto técnico (`/docs`, `/experiments`).
- O trabalho inicial fica centrado em QGIS (não ArcGIS), o que deve ser revisitado quando o licenciamento ArcGIS Enterprise/Utility Network for destravado.
- Toda decisão técnica relevante tomada ao longo do laboratório deve ser registrada neste arquivo.

---

<!-- Próxima decisão: adicionar como "## 0002 — <título>" -->
