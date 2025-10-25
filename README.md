# Cachy OS

Este repositório documenta problemas e soluções para rodar jogos no Linux usando **Heroic Launcher**, **Proton GE**, **Winetricks** e outras ferramentas de compatibilidade.

---

<details>
<summary>Need for Speed: Most Wanted (2005)</summary>

## Hardware do Sistema

- **CPU:** Intel Core i5-4570 @ 3.20GHz (4 núcleos)  
- **Memória RAM:** 16 GB (usados: 3.6 GB durante o teste)  
- **GPU 0:** NVIDIA GeForce GT 1030  
  - Driver: NVIDIA 580.95.5  
- **GPU 1:** Intel HD Graphics 4600 (integrada)  
- **Sistema Operativo:** CachyOS Linux 6.17.4-4-cachyos (Kernel 6.17.4)  

> Observação: Executado em PC tradicional, não Steam Deck.

---

## Software Utilizado

- **Heroic Launcher:** v2.18.1 "Waterfall Beard"  
- **Legendary:** v0.20.37  
- **Proton GE:** Última versão via Heroic  
- **Winetricks Packages:**  
  - `vcrun2005` → Visual C++ 2005 runtime  
  - `d3dx9` → DirectX 9  
  - `directplay` → Multiplayer antigo (opcional)  
  - `dxvk` → Tradução Direct3D → Vulkan  

- **Outras Ferramentas:**  
  - MangoHud → FPS/GPU monitoring  
  - GameMode → Otimização de desempenho Linux  

---

## Configurações do Jogo

- **Wine/Proton Options:**  
  - `enableEsync: true`  
  - `enableFsync: true`  
  - `useGameMode: true`  
  - `autoInstallDxvkNvapi: true`  
  - `enableWoW64: false`  
  - `preferSystemLibs: false`  

- **Caminho do Executável:**  
`/run/media/veezus/PSP MODDED/Need for Speed - Most Wanted/speed.exe`

---

## Passos Realizados

1. Instalação do Heroic Launcher  
2. Configuração do Proton GE  
3. Criação do prefixo Wine + instalação de dependências (`vcrun2005`, `d3dx9`, `directplay`, `dxvk`)  
4. Ajustes de performance:
   - Esync e Fsync habilitados  
   - GameMode ativado  
   - DXVK via Vulkan configurado  
5. Apontamento correto do executável  
6. Lançamento do jogo e verificação de logs

---

## Observações

- Warnings no log (`libgamemode.so`, `fixme`) não impedem execução  
- DXVK melhora compatibilidade Direct3D9 → Vulkan  
- MangoHud monitora FPS, GPU, CPU  

---

## Resultado

- Jogo inicia normalmente  
- Resolução Full HD (1920x1080) com DX9 via DXVK  
- Todos os recursos gráficos funcionam, limitado ao Proton/Wine  

---

## Créditos

- [Heroic Launcher](https://heroicgameslauncher.com/)  
- [Proton GE](https://github.com/GloriousEggroll/proton-ge-custom)  
- [Winetricks](https://wiki.winehq.org/Winetricks)  
- [DXVK](https://github.com/doitsujin/dxvk)  
- [MangoHud](https://github.com/flightlessmango/MangoHud)  

</details>

PROMPT:

Você é um especialista em Linux e compatibilidade de jogos. Vou te dar:

1. O nome do jogo.
2. Problemas e erros que tive durante a execução.
3. Soluções que funcionaram ou ajustes que apliquei para resolver.

Com base nisso, gere uma **seção completa em markdown** pronta para adicionar ao meu arquivo `.md`, seguindo este padrão:

- Use <details> e <summary> para tornar a seção expansível.  
- Estruture os tópicos: Hardware, Software, Configurações, Passos Realizados, Observações, Resultado, Créditos.  
- Formate caminhos de arquivos entre backticks (`) e opções de Proton/Wine como código.  
- Inclua apenas soluções que **realmente funcionaram** após meus testes.  
- Mantenha bullets, títulos claros e informações objetivas.  

Exemplo de resposta esperada:

<details>
<summary>Nome do Jogo (Ano)</summary>

## Hardware do Sistema
- CPU: ...
- GPU: ...
- RAM: ...

## Software Utilizado
- Heroic Launcher: ...
- Proton GE: ...
- Dependências Winetricks: ...

## Configurações do Jogo
- Proton/Wine Options: ...

## Passos Realizados
1. ...
2. ...
3. ...

## Observações
- ...
- ...

## Resultado
- ...

## Créditos
- ...
</details>
