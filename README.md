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

<details>
<summary>Need for Speed Most Wanted (2012)</summary>

## Hardware do Sistema
- **CPU**: Intel Core i5-4570 (4 cores, 3.2-3.6 GHz)
- **GPU**: NVIDIA GeForce GT 1030 (2GB VRAM)
- **GPU Integrada**: Intel HD Graphics 4600
- **RAM**: Não especificada
- **Armazenamento**: SSD Externo USB 500GB
- **Sistema**: Dual GPU (Optimus/PRIME)

## Software Utilizado
- **Distribuição**: CachyOS
- **Ambiente Gráfico**: KDE Plasma (Wayland)
- **Launcher**: Heroic Games Launcher
- **Camada de Compatibilidade**: Wine/Proton (versão não especificada)
- **Drivers GPU**: NVIDIA 580.95.05 (Driver proprietário)
- **Pacotes Necessários**:
  - `nvidia-dkms`
  - `nvidia-utils`
  - `nvidia-prime`
  - `ntfs-3g` (para partições NTFS)

## Problema Inicial
- **FPS travados em 20-30 FPS** independentemente das configurações gráficas
- Ao diminuir resolução: FPS fixos em 60
- Ao aumentar resolução: FPS fixos em 30
- GPU operando a apenas 50-63% de utilização
- Comportamento indicava limitador de frame rate ativo

## Configurações Aplicadas

### 1. Configuração PRIME (Forçar uso da NVIDIA GT 1030)
```bash
# Instalar suporte PRIME
sudo pacman -S nvidia-prime

# Lançar Heroic com NVIDIA
prime-run heroic
```

**Ou adicionar variáveis de ambiente no Heroic** (Settings → Environment Variables):
```
__NV_PRIME_RENDER_OFFLOAD=1
__VK_LAYER_NV_optimus=NVIDIA_only
__GLX_VENDOR_LIBRARY_NAME=nvidia
```

### 2. Configuração do MangoHud/GOverlay
Editar `~/.config/MangoHud/MangoHud.conf`:
```ini
# Mudar de Intel (0:00:02.0) para NVIDIA
pci_dev=0:01:00.0
```

### 3. Edição do Ficheiro de Configuração do Jogo
**Localização do ficheiro** (com Heroic):
```
~/.local/share/heroic/prefixes/NOME_DO_PREFIXO/drive_c/users/steamuser/Documents/Criterion Games/Need for Speed Most Wanted/config
```

**Alterações necessárias** na seção `[Display]`:
```ini
LockTo30=false          # Era: true
VsyncInterval=0         # Era: 1
```

**Configurações opcionais para melhor desempenho**:
```ini
Width=1280              # Ajustar conforme preferência
Height=720
SSAOLevel=0
HiResTextures=false
ParticleShadows=true
HeadlightShadows=false
Scattering=false
MotionBlurLevel=1
ReflectionDetailLevel=0
```

## Passos Realizados

1. **Verificação de GPU ativa**:
   ```bash
   lspci | grep VGA
   nvidia-smi
   ```
   Confirmado que o jogo usava a NVIDIA GT 1030 (1098-1180MB VRAM em uso).

2. **Tentativas iniciais** (não resolveram):
   - Desativação do compositor KDE (Alt+Shift+F12)
   - Alteração de configurações gráficas in-game
   - Teste de diferentes resoluções

3. **Diagnóstico do problema**:
   - Comportamento de FPS "escalonados" (20→30→60) indicou limitadores programados
   - GPU com utilização abaixo do esperado confirmou limitação por software

4. **Solução aplicada**:
   - Localização e edição do ficheiro `config`
   - Desativação de `LockTo30` e `VsyncInterval`
   - Reinício completo do jogo

## Observações

- **Sistema Dual GPU**: O i5-4570 possui gráficos integrados Intel, necessitando configuração PRIME para garantir uso da NVIDIA
- **Partição NTFS**: Jogos instalados em partição NTFS funcionam normalmente, com impacto mínimo de performance (~0-5%) para este nível de hardware
- **SSD Externo USB**: Não apresentou problemas de performance notáveis para este jogo
- **KDE Wayland**: Não causou problemas após configuração correta da GPU
- **Hardcoded FPS Cap**: O jogo tem limite de 60 FPS no motor gráfico, mas isso é adequado para a GT 1030
- **MangoHud**: Requer configuração manual do `pci_dev` para mostrar estatísticas corretas da GPU NVIDIA

## Monitorização Durante o Jogo

```bash
# Verificar uso da GPU NVIDIA
nvidia-smi -l 1

# Ou usar ferramenta visual
sudo pacman -S nvtop
nvtop
```

**Valores esperados durante gameplay**:
- GPU Utilization: 60-90%
- VRAM Usage: ~1100-1200MB
- Temperature: 45-70°C
- Power: Próximo de 30W

## Resultado

✅ **Problema resolvido completamente**  
✅ FPS desbloqueados e funcionando corretamente  
✅ GPU NVIDIA sendo utilizada adequadamente  
✅ Performance adequada para o hardware disponível  

## Créditos

- Diagnóstico e solução: Assistente Claude (Anthropic)
- Usuário: veezus (CachyOS)
- Data: 25 de Outubro de 2025

</details>

PROMPT:

<details>

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
