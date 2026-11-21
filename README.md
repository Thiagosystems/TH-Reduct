<p align="center">
  <img src="docs/logo.png" alt="TH Reduct" width="420">
</p>

<p align="center">
  Limpador de memória RAM leve e moderno para Windows, com modo jogo e interface personalizável.
</p>

<p align="center">
  <img src="https://img.shields.io/badge/Windows-10%20%7C%2011-0078D6?logo=windows" alt="Windows">
  <img src="https://img.shields.io/badge/.NET-8-512BD4?logo=dotnet" alt=".NET 8">
  <img src="https://img.shields.io/badge/licen%C3%A7a-MIT-green" alt="Licença MIT">
</p>

---

## ✨ Recursos

**Memória**
- Monitor de RAM em tempo real com medidor animado e **gráfico dos últimos 5 minutos**
- Uso da **memória virtual** (RAM + arquivo de paginação)
- Limpeza com um clique: working set, cache do sistema, páginas modificadas e lista standby
- **Atalho global** para limpar (padrão `Ctrl+Shift+L`, configurável)
- Limpeza automática por % de uso ou por intervalo
- **Histórico de limpezas** (quanto liberou e quando)

**🎮 Modo jogo**
- **Vários jogos salvos**, cada um com sua configuração
- **Detecção automática** de jogos da Steam, Epic Games e Riot Games
- Prioridade alta para o jogo, e o Windows passa a tirar RAM dos outros apps primeiro
- Liberação periódica da RAM dos outros programas
- **Pausar ou fechar apps pesados** (navegador, Discord...) ao abrir o jogo; os pausados voltam quando ele fecha
- **Plano de energia Alto desempenho** durante o jogo
- Tudo é desfeito automaticamente quando o jogo fecha

**📊 Monitor**
- **Lista dos apps que mais usam RAM**, com botão para limpar só um deles
- **Widget flutuante** (overlay) com RAM, CPU, GPU e temperatura, que pode aparecer só durante o jogo
- **Avisos**: RAM quase cheia, ou um app consumindo memória demais (clique no aviso para limpar)

**🎨 Personalização**
- Temas escuro, preto (AMOLED) e claro
- 8 combinações de cores prontas ou cores próprias
- Cor da logo ajustável
- Tamanho da janela, opacidade e "sempre no topo"
- **Idiomas: Português, English, Español**

**Sistema**
- Ícone na bandeja com a % de uso
- Iniciar com o Windows (já com permissão de administrador)

> ℹ️ O widget não mostra FPS: medir FPS exige injetar código no jogo, o que pode causar ban por anti-cheat.

## 📥 Download

Baixe a versão mais recente na aba [**Releases**](https://github.com/Thiagosystems/THReduct/releases).

> Requer o [.NET 8 Desktop Runtime](https://dotnet.microsoft.com/download/dotnet/8.0) (x64).
> O programa pede permissão de **administrador**, que é necessária para limpar a lista standby e o cache do sistema.

## 🛠️ Compilar a partir do código

Pré-requisito: [.NET 8 SDK](https://dotnet.microsoft.com/download/dotnet/8.0)

```bat
git clone https://github.com/Thiagosystems/THReduct.git
cd THReduct
build.bat
```

Ou manualmente:

```bat
dotnet publish -c Release -r win-x64 --self-contained false -p:PublishSingleFile=true -o publish
```

O executável fica em `publish\THReduct.exe`.

## 📁 Estrutura

| Arquivo | Função |
|---|---|
| `MemoryCleaner.cs` | Limpeza de memória (APIs nativas do Windows) |
| `GameBooster.cs` | Modo jogo (prioridades, apps pesados, plano de energia) |
| `GameLibrary.cs` | Detecção de jogos Steam/Epic/Riot |
| `OverlayWindow.xaml` | Widget flutuante |
| `SystemStats.cs` | CPU, GPU e temperatura |
| `HotkeyManager.cs` | Atalho global |
| `Loc.cs` | Traduções (PT/EN/ES) |
| `ThemeManager.cs` | Temas e cores |
| `LogoView.cs` | Logo com cores ajustáveis |
| `StartupManager.cs` | Iniciar com o Windows |
| `Settings.cs` | Configurações (`%AppData%\THReduct\settings.json`) |
| `MainWindow.xaml` | Interface |

## ⚙️ Como funciona

O TH Reduct usa as mesmas APIs do Windows que ferramentas como o Mem Reduct:

- `NtSetSystemInformation` (`SystemMemoryListInformation`): esvazia os working sets, grava as páginas modificadas e limpa a lista standby
- `SetSystemFileCacheSize`: esvazia o cache de arquivos do sistema
- `SetProcessInformation` (`ProcessMemoryPriority`): ajusta a prioridade de memória dos processos no modo jogo

> ⚠️ Limpar a memória não aumenta a RAM do computador. O ganho aparece quando o sistema está com pouca memória livre ou quando um jogo disputa RAM com outros programas.

## ❓ Perguntas frequentes

**O antivírus acusou o programa. É vírus?**
Não. Alguns antivírus marcam por heurística programas que mexem na memória do sistema e pedem administrador. O código é aberto e você pode compilar por conta própria.

**Onde ficam as configurações?**
Em `%AppData%\THReduct\settings.json`. Para restaurar tudo, apague esse arquivo.

**Como desinstalar?**
Desative "Iniciar com o Windows" nas configurações, feche pelo ícone da bandeja (botão direito → Sair) e apague o executável.

## 📄 Licença

Distribuído sob a licença MIT. Veja [LICENSE](LICENSE).
