Cachy Os

# Need for Speed: Most Wanted (2005) no Linux

Este guia/documentação descreve como conseguimos rodar o jogo **Need for Speed: Most Wanted (2005)** no Linux usando o **Heroic Launcher** com **Proton GE** e ajustes específicos de compatibilidade.

---

## Hardware do Sistema

- **CPU:** Intel Core i5-4570 @ 3.20GHz (4 núcleos)  
- **Memória RAM:** 16 GB (usados: 3.6 GB durante o teste)  
- **GPU 0:** NVIDIA GeForce GT 1030  
  - Driver: NVIDIA 580.95.5  
- **GPU 1:** Intel HD Graphics 4600 (integrada)  
- **Sistema Operativo:** CachyOS Linux 6.17.4-4-cachyos (Linux Kernel 6.17.4)  

> Observação: O jogo não está sendo executado em um Steam Deck, e sim em um PC tradicional com Linux.

---

## Software Utilizado

- **Heroic Launcher:** v2.18.1 "Waterfall Beard"  
- **Legendary:** v0.20.37  
- **Proton GE (Glorious Eggroll):** Versão mais recente utilizada via Heroic  
- **Winetricks Packages:**  
  - `vcrun2005` → Visual C++ 2005 runtime  
  - `d3dx9` → Bibliotecas DirectX 9  
  - `directplay` → Suporte a multiplayer antigo (não crítico)  
  - `dxvk` → Tradução de Direct3D para Vulkan, aumentando compatibilidade e performance  

- **Outras Ferramentas:**  
  - MangoHud → Monitoramento de FPS/GPU  
  - GameMode → Otimização de desempenho no Linux  

---

## Configurações do Jogo

- **Wine/Proton Options:**  
  - `enableEsync: true` → Melhor performance e sincronização de threads  
  - `enableFsync: true` → Maior estabilidade em sistemas Linux modernos  
  - `useGameMode: true` → Ativa otimizações do GameMode  
  - `autoInstallDxvkNvapi: true` → Instala automaticamente DXVK e NVAPI  
  - `enableWoW64: false` → Rodando prefixo 32-bit  
  - `preferSystemLibs: false` → Usa bibliotecas do Proton em vez das do sistema  

- **Caminho do Executável:**  
/run/media/veezus/PSP MODDED/Need for Speed - Most Wanted/speed.exe


> Garantir o caminho correto é fundamental para que o Proton consiga inicializar o jogo.

---

## Passos Realizados para Rodar o Jogo

1. **Instalação do Heroic Launcher** no Linux.  
2. **Configuração do Proton GE** (Glorious Eggroll) para compatibilidade com jogos antigos.  
3. **Criação do prefixo Wine** e instalação de dependências via Winetricks (`vcrun2005`, `d3dx9`, `directplay`, `dxvk`).  
4. **Ajustes de performance e compatibilidade**:
 - Habilitação de Esync e Fsync.  
 - Ativação do GameMode para otimizações automáticas.  
 - Configuração do DXVK para rodar via Vulkan.  
5. **Apontamento correto do executável** do jogo no Heroic Launcher.  
6. **Lançamento do jogo**, monitorando logs e confirmando que os warnings (`fixme` e `dlopen`) não impediam a execução.  

---

## Observações

- Os **logs** ainda apresentam warnings sobre `libgamemode.so` e funções não implementadas no Wine (`fixme`), mas **isso não impede o jogo de rodar**.  
- O DXVK traduz o Direct3D9 para Vulkan, garantindo melhor desempenho em GPUs modernas.  
- O MangoHud permite monitorar FPS, uso de GPU e CPU durante a jogabilidade.  

---

## Resultado

- O jogo **inicia normalmente** e é totalmente jogável com as configurações acima.  
- É possível jogar em **resolução Full HD (1920x1080)** com suporte a DX9 via DXVK.  
- Todos os recursos gráficos do jogo funcionam normalmente, dentro das limitações do Proton/Wine.  

---

## Créditos e Referências

- **Heroic Launcher:** https://heroicgameslauncher.com/  
- **Proton GE (Glorious Eggroll):** https://github.com/GloriousEggroll/proton-ge-custom  
- **Winetricks:** https://wiki.winehq.org/Winetricks  
- **DXVK:** https://github.com/doitsujin/dxvk  
- **MangoHud:** https://github.com/flightlessmango/MangoHud  
