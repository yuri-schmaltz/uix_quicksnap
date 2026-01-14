# UIX – Quick Interface Tweaks (Blender Add-on)

## Proposta
O **UIX – Quick Interface Tweaks** é um add-on para Blender focado em **reduzir cliques** e **acelerar o acesso** às opções mais usadas da interface, expondo controles essenciais **diretamente no Header** (lado direito) da Viewport 3D.

A primeira entrega do projeto é a **barra rápida de Snap**, que traz os principais toggles e seletores sem a necessidade de abrir menus e popovers repetidamente. O objetivo é manter o fluxo de modelagem/edição mais contínuo, especialmente em sessões longas de trabalho.

---

## Objetivos
- **Acesso rápido** a configurações comuns (menos camadas de UI).
- **Consistência visual** com a interface do Blender (sem “re-inventar” o estilo).
- **Modularidade**: cada conjunto de ajustes (Snap, Gizmos, Overlays etc.) deve ser um módulo ativável.
- **Compatibilidade**: funcionar em Blender 3.x e 4.x, com fallbacks quando propriedades mudam entre versões.

---

## Escopo da Fase 1 (Snap Quick Bar)
A barra rápida de Snap adiciona ao Header da Viewport 3D:
- **Snap ON/OFF**
- **Snap Base** (Closest / Center / Median / Active) em botões compactos
- **Snap Target / Elements** em botões (Increment, Vertex, Edge, Face… configuráveis)
- **Popover** opcional com as opções completas (para manter o Header limpo)

Também inclui **Preferências do Add-on** para habilitar/desabilitar botões e controlar o nível de exposição de opções.

---

## Como instalar
1. `Edit > Preferences > Add-ons > Install…`
2. Selecione o `.zip` do add-on
3. Ative o add-on em **Interface**
4. Ajuste os botões em **Preferences do add-on** (se necessário)

---

## Princípios de Design (UI/UX)
- **Atalhos visuais**: botões com ícones e estados “depress” para indicar seleção ativa.
- **Sem poluir o Header**: o “poder completo” fica no popover; o Header mostra só o essencial.
- **Não quebrar o Blender**: o add-on **não substitui** o Snap nativo; ele **complementa** com uma camada de acesso rápido.
- **Configuração por perfil** (futuro): permitir presets de layout por atividade (Modeling, Sculpt, CAD-like, etc.).

---

## Arquitetura (visão geral)
- **Draw handler no Header** (`VIEW3D_HT_header.append`): injeta a barra rápida no lado direito.
- **Operators leves**: toggles para elementos do Snap e seletor de Snap Base.
- **Popover Panel**: concentra opções completas para evitar excesso de botões no Header.
- **Addon Preferences**: controla quais botões aparecem e quais módulos ficam ativos.

---

## Roadmap (Próximas fases)

### Fase 2 – Snap “Pro” (Refino de comportamento)
**Meta:** tornar a barra de Snap mais inteligente e completa sem aumentar a complexidade visual.
Entregas sugeridas:
- Expor *Snap Affect* (Move/Rotate/Scale) em botões compactos.
- Expor *Rotation Increment* (quando disponível) com um seletor rápido (ex.: 1°, 5°, 15°).
- Detectar contexto (Object/Edit) e ajustar quais opções aparecem.
- Ajustar compatibilidade por versão (3.6 / 4.x), incluindo propriedades que mudam de nome.

### Fase 3 – Overlays e Gizmos (Acesso rápido)
**Meta:** controles de visibilidade e ferramentas comuns sem abrir o popover de Overlays.
Entregas sugeridas:
- Overlays ON/OFF + toggles de Wireframe, Face Orientation, Grid/Floor, Normals (modo Edit).
- Gizmos ON/OFF + toggles por tipo (Move/Rotate/Scale/Transform).
- Presets rápidos (ex.: “Clean View”, “Modeling”, “Checking Normals”).

### Fase 4 – Layout Modular e Presets
**Meta:** permitir que o usuário componha a UI conforme o fluxo de trabalho.
Entregas sugeridas:
- Sistema de **módulos** (Snap, Overlays, Gizmos, Shading/Viewport, etc.) ativáveis.
- **Presets** exportáveis/importáveis (JSON) para compartilhar configurações.
- Ordenação e espaçamento configuráveis dos grupos no Header.

### Fase 5 – Ações avançadas e “One-Click Workflows”
**Meta:** pequenas automações e ações contextuais para tarefas repetitivas.
Entregas sugeridas:
- Botões contextuais (ex.: “Apply Scale”, “Set Origin”, “Shade Smooth/Auto Smooth” conforme versão).
- Macros simples (sequências de operadores) com UI mínima.
- Integração opcional com keymaps (atalhos para abrir/alternar presets e módulos).

---

## Critérios de Qualidade (para cada fase)
- **Sem regressões**: se uma propriedade não existir na versão do Blender, o botão não aparece (fallback).
- **Sem duplicar UI desnecessariamente**: expor só o que dá ganho real de velocidade.
- **Performance**: draw handlers enxutos; evitar lógica pesada em `draw()`.
- **Testes manuais mínimos**: checar Object/Edit modes, diferentes temas e resolução de tela.

---

## Status do projeto
- [x] Fase 1 – Snap Quick Bar (base)
- [ ] Fase 2 – Snap “Pro”
- [ ] Fase 3 – Overlays e Gizmos
- [ ] Fase 4 – Layout Modular e Presets
- [ ] Fase 5 – Workflows avançados

---

## Licença
GPL-2.0-or-later (compatível com a política de add-ons do Blender).

---

## Contribuição (sugestão)
- Issues: descrever o fluxo de trabalho e qual clique/tempo pretende reduzir.
- Pull Requests: manter módulos independentes e evitar mudanças invasivas no draw do Blender.
