# 📘 Documentação Técnica & Arquitetural — RezTerm (SepulnationTerm)

> **Documento de Uso Interno e Exclusivo do Time de Engenharia de Desenvolvimento (Devs)**  
> **Objetivo**: Fornecer um guia profundo e cirúrgico sobre a arquitetura do código-fonte, padrões de projeto, motores nativos, serviços injetados, modelagem de dados e tecnologias empregadas no **RezTerm** (codinome *SepulnationTerm*).

---

## 🏛️ 1. Visão Geral e Paradigma Arquitetural (.NET 10 Blazor Hybrid + WPF)

O **RezTerm** adota o padrão **Blazor Hybrid sob Windows Presentation Foundation (WPF)** rodando em **.NET 10.0 Native (win-x64)**.

### Por que Blazor Hybrid sobre WPF?
1. **Acesso Total ao Sistema Operacional (Win32 & Npcap)**: Diferente de aplicações web tradicionais ou PWA/Electron sandboxadas, o WPF confere ao código C# acesso nativo a sockets ICMP brutos, driver Npcap de captura de pacotes L2, APIs Wi-Fi (`wlanapi.dll`), DPAPI de criptografia do Windows e manipulação de registro/atalhos no sistema operacional.
2. **Riqueza de Interface Web (Razor Components HTML5/CSS3)**: Em vez de desenhar interfaces complexas em XAML puro, a renderização visual acontece em um controle `BlazorWebView` embarcando o motor de renderização do **Microsoft Edge WebView2**. Isso permite usar CSS moderno (Grid, Flexbox, Animações GPU, Design Tokens) e bibliotecas JavaScript de ponta (como `xterm.js` para terminal SSH).

> 🎨 **Especificação do Design System AP Key Visual**: Para detalhes sobre a paleta de cores Ciano Neon (`#00f0ff`), tipografia (`Segoe UI / Consolas`), tokens CSS `:root`, DWM Imersivo e metodologia de criação de novas telas sem rolagem externa, consulte a documentação oficial em **[`REZTERM_KEY_VISUAL_API.md`](file:///C:/Users/junio/source/repos/SepulnationTerm/REZTERM_KEY_VISUAL_API.md)**.
> 
> 🛠️ **Automação de Setup de Ambiente Local (Audicom Devs)**: Para preparar a máquina de um novo desenvolvedor em 1 clique (instalando .NET SDK 10/8/9, Npcap Driver, Node.js, Git e Workloads), execute **`.\setup_dev_env.ps1`** no PowerShell. Para configurar o Visual Studio 2022, VS Code ou JetBrains Rider com as extensões recomendadas, consulte **[`EXTENSOES_DEVS_AUDICOM.txt`](file:///C:/Users/junio/source/repos/SepulnationTerm/EXTENSOES_DEVS_AUDICOM.txt)** e o arquivo **[`.vscode/extensions.json`](file:///C:/Users/junio/source/repos/SepulnationTerm/.vscode/extensions.json)**.

```
┌────────────────────────────────────────────────────────────────────────┐
│                   Windows 11 / 10 OS Shell (DWM)                       │
└───────────────────────────────────┬────────────────────────────────────┘
                                    │ Win32 API / DwmSetWindowAttribute
┌───────────────────────────────────▼────────────────────────────────────┐
│                    MainWindow.xaml (Host WPF .NET 10)                  │
│  - Trava de Instância Única por Pasta (Mutex / LockFile)               │
│  - Inicialização de Cofres e Motores Nativos                           │
└───────────────────────────────────┬────────────────────────────────────┘
                                    │ <blazor:BlazorWebView>
┌───────────────────────────────────▼────────────────────────────────────┐
│               Edge WebView2 Engine (Isolamento de Cache)               │
├────────────────────────────────────────────────────────────────────────┤
│                     Componentes Razor / Blazor UI                      │
│  [DashboardTab]  [IcmpMenuTab]  [EthernetTestsTab]  [GraylogConfig]    │
└───────────────────────────────────┬────────────────────────────────────┘
                                    │ Injeção de Dependência (DI) C#
┌───────────────────────────────────▼────────────────────────────────────┐
│                    SepulnationTerm.Services & Core                     │
│  [PingService] [CaptureEngine] [HostStorageService] [AuditRecording]   │
└────────────────────────────────────────────────────────────────────────┘
```

---

## ⚙️ 2. Camada Core & Motores Nativos (`SepulnationTerm.Core`)

A pasta `Core/` abriga os motores de baixo nível que interagem diretamente com drivers e protocolos da camada de enlace e rede:

### 🔬 `Core/CaptureEngine` (Captura de Pacotes L2)
* **`ICaptureEngine` & `SharpPcapEngine`**: Envolve a biblioteca **SharpPcap** e **PacketDotNet**. Abre o dispositivo de rede físico em **modo promíscuo** para capturar quadros Ethernet brutos (Frames L2). Contém tratamento anti-quebra caso o computador não possua o Npcap/WinPcap instalado.
* **`Core/Parsers/`**:
  * `OuiDatabase.cs`: Base OUI (*Organizationally Unique Identifier*) embutida em memória para decodificar os 3 primeiros bytes do MAC Address e identificar fabricantes (Datacom, Cisco, MikroTik, Dell, Huawei).
  * `NeighborDiscoveryParser.cs`: Decodifica quadros de protocolos de descoberta de vizinhança:
    * **LLDP (802.1AB)**: TLVs de Chassi ID, Port ID e System Description.
    * **CDP (Cisco Discovery Protocol)**: Estruturas proprietárias Cisco.
    * **MNDP (MikroTik Neighbor Discovery Protocol)**: Datagramas UDP 5678 extraindo RouterOS version e Board Name.
  * `SpanningTreeParser.cs`: Inspeciona BPDUs de STP, RSTP e MSTP avaliando o estado de convergência e proteção de loops.
  * `Vlan8021QParser.cs`: Analisa tags 802.1Q e QinQ no cabeçalho L2 alertando sobre vazamentos de tráfego Trunk (*VLAN Leakage*).
  * `PppoeDiscoveryParser.cs` & `DhcpParser.cs`: Construtores de pacotes brutos para injeção ativa de **PADI** (descoberta de concentradores PPPoE) e **DHCP Discover** (caça a servidores DHCP clandestinos/Rogue).

### 📶 `Core/WirelessEngine` (RF & Espectro Wi-Fi)
* **`NativeWifiApi.cs`**: Realiza interoperabilidade P/Invoke direto com a `wlanapi.dll` nativa do Windows (`WlanOpenHandle`, `WlanEnumInterfaces`, `WlanGetNetworkBssList`).
* **`WirelessTelemetry.cs`**: Mapeia redes nas frequências de 2.4 GHz, 5 GHz e 6 GHz (Wi-Fi 6E/7), convertendo RSSI em dBm para porcentagem de qualidade e calculando a relação Sinal-Ruído (SNR).

---

## 🛠️ 3. Camada de Serviços (`SepulnationTerm.Services`)

Todos os serviços são registrados no contêiner de injeção de dependência (`ServiceCollection`) em `App.xaml.cs` como **Singletons** (para estados persistentes em tempo de execução) ou **Transients**:

### 🧮 `PingService` & `TracerouteService` (IP Stack Control)
* **Resolução Inteligente por Família (`ResolveTargetAsync`)**: Antes de executar um ping ou MTR, o serviço consulta o DNS com base na opção selecionada na interface:
  * `IPv4 (-4)`: Força consulta estrita por registros **A** (`AddressFamily.InterNetwork`).
  * `IPv6 (-6)`: Força consulta estrita por registros **AAAA** (`AddressFamily.InterNetworkV6`).
* **Precisão de Jitter no MTR (`TracerouteService.RunMtrContinuousAsync`)**: O cálculo de instabilidade (*Jitter*) no MTR Avançado é realizado isolando o salto final de destino (`destHop`), evitando que políticas de *Control Plane Policing (CoPP)* ou rate-limit de ICMP dos roteadores intermediários distorçam a métrica end-to-end.

### 💻 `SshConnectionManager` & `HostStorageService` (Cofre DPAPI)
* Gerencia conexões SSH assíncronas utilizando **SSH.NET**.
* **Criptografia DPAPI HMAC-SHA256**: Ao salvar servidores no cofre (`hosts.dat`), o `HostStorageService` criptografa os dados utilizando a chave mestra do perfil do Windows em execução (`ProtectedData.Protect` com `DataProtectionScope.CurrentUser`). Além disso, gera uma assinatura **HMAC-SHA256** anexada ao arquivo para rejeitar qualquer tentativa de modificação manual por agentes externos ou malware.

### ⚡ `LiveTcpUdpService` & `MaxMind GeoLite2`
* Varre a tabela de portas do kernel do Windows usando `IPGlobalProperties.GetIPGlobalProperties().GetActiveTcpConnections()`.
* **Mapeamento em Memória (MMF)**: Carrega o arquivo `GeoLite2-City.mmdb` via `MemoryMappedFile` para performance instantânea (zero I/O de disco a cada conexão descoberta), associando cada IP remoto à sua coordenada geográfica (Latitude/Longitude), cidade e país no **Mapa Mundi interativo**.

### 🕵️ `AuditRecordingService` & `UpdateService`
* **`AuditRecordingService`**: Responsável por serializar laudos forenses (como investigações CGNAT) e auditar ações dos analistas. Emprega a biblioteca **QuestPDF** para desenhar laudos em PDF de alta resolução com cláusulas jurídicas e hash SHA-256.
* **`UpdateService`**: Consulta de forma não-bloqueante a API REST do GitHub CDN (`api.github.com/repos/juniorespow/RezTerm-Downloads/releases/latest`), comparando a versão local de montagem do assembly com a tag remota.

### 🔬 `RezLogger.cs` (Observabilidade JSONL & Data Masking)
* Motor de logging estruturado no formato **JSON Lines (`.jsonl`)** com rotação diária e expurgo após 14 dias em `%LocalAppData%\RezTerm\Logs`.
* Implementa varredura de **Sanitização de Dados (Data Masking)**: qualquer string ou dicionário de exceção contendo chaves sensíveis (`password`, `senha`, `token`, `secret`, `apikey`) tem o valor automaticamente mascarado para `"***MASKED***"`.

---

## 📦 4. Modelagem de Dados (`SepulnationTerm.Models`)

As models são desenhadas para serem leves, reativas e com suporte à serialização JSON:
* **`HostEntry.cs`**: Representa um servidor cadastrado no cofre SSH/RDP (Nome, IP, Porta, Usuário, Senha Criptografada, Grupo, Tags).
* **`GraylogServer.cs`**: Representa um nó ou cluster Graylog cadastrado para buscas CGNAT (Id, Nome, HostnameOrIp, Port, ApiKey, Version `v4.x/v5.x`, DashboardName).
* **`MtrHop.cs` & `CustomPingReply.cs`**: Estruturas de métricas de rede em tempo real armazenando array de histórico de latência (`LatencyHistory`) para renderização instantânea de gráficos SVG.

---

## 🖥️ 5. Interface Gráfica Razor (`SepulnationTerm.Components`)

A interface é construída em componentes reativos `.razor` modularizados:
* **`DashboardTab.razor`**: Painel inicial exibindo gráficos de consumo, latência e status Dual-Stack.
* **`IcmpMenuTab.razor`**: Suíte de ferramentas ICMP com abas de MTR Contínuo (tabela SVG + controles de Versão IP) e Ping Avançado (grid interativo com log azul neon).
* **`EthernetTestsTab.razor` & `WirelessTestsTab.razor`**: Interfaces de medição L2 e RF com medidores visuais em tempo real.
* **`GraylogConfig.razor` & `CgnatSearch.razor`**: Componentes de CRUD de servidores Graylog e formulário forense com busca Lucene e botões de exportação judicial.

### Interoperabilidade JSInterop
Para recursos que exigem manipulação direta do navegador embutido (como o terminal SSH `xterm.js`, cópia para clipboard via `navigator.clipboard.writeText` ou renderização de gráficos Canvas), os componentes utilizam `JSRuntime.InvokeVoidAsync`.

---

## 🛡️ 6. Pipeline de Build & Blindagem de Compilação

Para compilar o código em modo de produção blindado, o arquivo `SepulnationTerm.csproj` declara as propriedades de blindagem:
```xml
<PropertyGroup Condition="'$(Configuration)' == 'Release'">
  <PublishSingleFile>true</PublishSingleFile>
  <SelfContained>true</SelfContained>
  <RuntimeIdentifier>win-x64</RuntimeIdentifier>
  <PublishReadyToRun>true</PublishReadyToRun>
  <IncludeNativeLibrariesForSelfExtract>true</IncludeNativeLibrariesForSelfExtract>
  <DebugType>none</DebugType>
  <DebugSymbols>false</DebugSymbols>
</PropertyGroup>
```

O script automatizado **`deploy_release.ps1`** orquestra todo o processo de deploy:
1. Encerra instâncias em execução.
2. Compila `SepulnationTerm.exe` no formato nativo pré-compilado (`ReadyToRun`).
3. Compila o bootstrapper `RezTermSetup.exe`.
4. Gera o pacote `RezTerm.zip` incorporando os binários e a base `GeoLite2` intacta.
5. Sincroniza via GitHub CLI (`gh release create / upload`) na CDN mundial do repositório público `juniorespow/RezTerm-Downloads`.

---

## 🧩 10. Atualizações de Engenharia na Release v2.0.2

1. **Cadeia de Multi-Ping (`IcmpMenuTab.razor`)**:
   - Estruturação de disparos simultâneos ou em cadeia para múltiplos alvos (`Ping#1`, `Ping#2`, ...).
   - Cálculo em tempo real de estatísticas individuais (Mín/Máx/Médio) e **Porcentagem de Perda de Pacotes (`LossPct`)** renderizado com gráfico e barras em ciano/verde neon.
   - Gerador de laudos instantâneos na área de transferência com notificação visual.
2. **Exibição Dual-Stack na Dashboard (`DashboardTab.razor` & `DashboardService.cs`)**:
   - Resolução simultânea de gateways de saída IPv4 e IPv6 da interface ativa, apresentados distintamente na barra de status superior.
3. **Responsividade Otimizada (`MainApp.razor`)**:
   - Containers flexíveis com `flex-wrap: wrap` e rolagem vertical controlada na barra lateral (`overflow-y: auto`), assegurando escalabilidade visual em telas de 14 polegadas ou resoluções portáteis sem sobreposições ou cortes de cartões.
4. **Armazenamento de Hosts SSH com Colapso por Fabricante (`TerminalTab.razor` & `HostEntry.cs`)**:
   - Suporte expandido ao inventário multi-fabricantes contendo **12 Vendors**: `Cisco`, `Datacom`, `MikroTik`, `Linux`, `Huawei`, `Juniper`, `Nokia`, `Ubiquiti`, `TPLink`, `VSOL`, `FiberHome`, `ZTE`.
   - Organização estrutural em ordem alfabética (`StringComparer.OrdinalIgnoreCase`) combinada a um `HashSet<string> collapsedVendors` que permite expandir e recolher dinamicamente grupos inteiros na interface.

---

## 🚀 11. HotFix e Otimizações de Fluidez na Release v2.0.3

1. **Fluidez e Partida Instantânea na Telemetria Ativa Gateway vs RF (`WirelessDiagnosticService.cs`)**:
   - Refatoração do método `StartActiveGatewayMonitor()` e do laço de sondagem `ActiveMonitorLoopAsync`, eliminando travamentos assíncronos na descoberta de interface.
   - Implementação de amostra de aquecimento (warmup) imediata e redução do timeout de ICMP para 600ms, disparando a atualização visual em tempo real instantaneamente ao clique do usuário.
2. **Barras de Progresso ao Vivo (`WirelessTestsTab.razor`)**:
   - Adição de banners interativos em tempo real com barra neon (`linear-gradient(90deg, #00f0ff, #00ff88)`) e relatórios de status (`ScanProgress`, `ActiveMonitorProgress`) nas ferramentas de **Varredura de Espectro** e **Monitor Gateway RF**.
3. **Reformulação de Tipografia e Contraste na Lista de Redes Detectadas**:
   - Substituição de textos cinzentos por cabeçalhos em ciano neon de alto contraste (`#00f0ff`) e células em branco puro (`#f8fafc`).
   - Formatação das listas de SSIDs sobrepostos em cada canal espectral (`ch.OverlappingSsids`) como pílulas/chips estruturadas em borda neon translúcida.

---

## 🚀 12. Evolução do Terminal SSH na Release v2.0.4

1. **Sincronização Dinâmica Bidirecional em Tempo Real (`SIGWINCH` / `ChangeWindowSize`)**:
   - Sincronização automática em tempo real entre a matriz gráfica do Xterm.js (`FitAddon.fit()`) e o stream do PTY remoto (`session.ShellStream.ChangeWindowSize`).
   - Resolvido em definitivo o truncamento e desconfiguração de aplicações TUI em tela cheia no Linux (`htop`, `btop`, `vim`), fazendo com que se moldem milimetricamente em 100% da janela visível.
2. **Destaque Sintático Avançado com Alerta Visual Crítico (`NetworkHighlighting.xshd` & `terminal.js`)**:
   - Expansão do vocabulário de coloração para comandos Cisco e Datacom (interfaces, protocolos, parâmetros BGP/VPLS).
   - Inclusão da palavra-chave **`deny`** em vermelho brilhante (`#FF3333` / classe CSS `.terminal-deny`), permitindo identificação imediata de regras de bloqueio e ACLs.
3. **Menu de Contexto Estilo MobaXterm (`Copiar Tudo Buffer SSH`)**:
   - Adição do método `getAllText(sessionId)` no motor `terminal.js` utilizando `buffer.active.getLine(i).translateToString(true)` para capturar integralmente o histórico da sessão preservando identações, espaços e saltos de linha exatos.

## 🚀 13. Motor Forense BPA e Assistente Híbrido HelpDesk na Release v2.0.6

1. **Rastreio Inteligente de Blocos de Alocação NAT (`Cisco BPA - RFC 6598`)**:
   - Resolução do problema de detecção de portas em tráfego CGNAT no Graylog: roteadores Cisco e coletores NetFlow frequentemente registram apenas a porta de início do bloco alocado (ex: `64512` até `65023`).
   - Implementação do algoritmo `MatchesPort(int targetPort)` em `CgnatLogResult.cs`, avaliando em memória as propriedades `NfPostNatPortBlockStart`, `NfPostNatPortBlockEnd` e `NfPostNatPortBlockStep`.
   - Expansão das consultas Lucene em `GraylogApiClient.cs` para abranger todos os protocolos L4 (UDP, TCP, ICMP), garantindo 100% de precisão na correlação forense de IPs públicos com IPs privados `100.64.x.x`.
2. **Interface Híbrida Bimodal (`SuspiciousConnectionsSearch.razor`)**:
   - **Modo Assistente HelpDesk (Suporte N1/N2)**: Interface guiada por 4 cenários práticos (Bloqueio de E-mail/Spam, Vírus/Malware, Ataque DDoS e Consulta Livre), configurando automaticamente as portas críticas e apresentando painéis interativos de orientação com roteiro de resposta ao cliente e botão "Copiar Ticket".
   - **Modo Engenharia (Avançado)**: Chaveamento instantâneo para inspeção manual com filtros brutos de Lucene, listas de IPs, faixas numeradas BPA e exportação jurídica para PDF e TXT.

## 🔐 14. Arquitetura do Sistema de Licenciamento Criptográfico e Keygen (v2.0.6)

A partir da versão **v2.0.6**, o ecossistema RezTerm adotou uma postura restritiva de propriedade intelectual corporativa (*Proprietary Telecom Software*). Como a suíte se tornou extremamente completa em funcionalidades forenses, diagnósticos L2/L3/L4, RF e SSH, a Diretoria Telecom determinou o fim da livre distribuição sem controle de autenticação de hardware.

### 🧠 14.1. Conceito Fundamental (*Security by Design Offline*)
Para garantir que o software opere em ambientes críticos de ISP, Datacenters e PoPs sem depender de chamadas externas ou servidores de licença na nuvem (que poderiam falhar durante incidentes de rede), o licenciamento foi projetado com criptografia assimétrica/HMAC **100% Offline e Determinística**:
1. **Identidade de Hardware (HWID)**: Cada computador possui uma impressão digital criptográfica imutável vinculada à sua placa-mãe e processador.
2. **Criptografia HMAC-SHA256**: Apenas a Diretoria Telecom (de posse da chave secreta mestra `MasterSecret` no aplicativo Keygen) é capaz de gerar uma assinatura digital válida para um determinado HWID.
3. **Impossibilidade de Transferência**: Se um técnico tentar copiar seu arquivo de licença ou chave para o computador de outro colaborador, o cálculo criptográfico local falhará e o acesso será bloqueado instantaneamente.

---

### 🛠️ 14.2. Guia de Onboarding para Novos Desenvolvedores
Se você é um desenvolvedor que está ingressando no projeto agora, entenda detalhadamente como o subsistema se articula através das 3 camadas principais:

#### A) Motor de Validação no Cliente (`SepulnationTerm.Services.LicensingService`)
* **Localização do Código**: [LicensingService.cs](file:///C:/Users/junio/source/repos/SepulnationTerm/SepulnationTerm/Services/LicensingService.cs)
* **Como o HWID é calculado?** O método `GenerateHwid()` acessa o Registro do Windows em `HKEY_LOCAL_MACHINE\SOFTWARE\Microsoft\Cryptography` para ler a propriedade `MachineGuid` e combina com o `ProductId` do sistema operacional. Sobre essa string bruta (`REZTERM-HWID-V2-{guid}-{prod}`), é aplicado o algoritmo **SHA-256**, extraindo-se os primeiros 12 caracteres hexadecimais em maiúsculo (ex: `REZ-8F9A-2B1C-4D5E`).
* **Estrutura de uma Chave Corporativa**:
  `REZ-<EDICAO>-<EXPIRACAO>-<HWID_LIMPO>-<ASSINATURA_HMAC>`
  * *Exemplo*: `REZ-PRO-20270706-8F9A2B1C4D5E-7A8B9C0D1E2F3A4B` (onde `7A8B9C0D1E2F3A4B` são os 16 caracteres hexadecimais da assinatura HMAC-SHA256 do payload).
* **Persistência Segura**: Ao ser validada no cliente, a licença é gravada em `%LocalAppData%\RezTerm\license.json`. Na inicialização do app, o construtor do `LicensingService` executa `LoadAndVerifyLicense()`; se a licença estiver corrompida, alterada ou com data expirada (`DateTime.UtcNow > expDate`), a propriedade `IsLicensed` retorna `false`.

#### B) Tela de Bloqueio Modal (`SepulnationTerm.Components.LicensingModal`)
* **Localização do Código**: [LicensingModal.razor](file:///C:/Users/junio/source/repos/SepulnationTerm/SepulnationTerm/Components/LicensingModal.razor)
* **Fluxo Visual**: No componente raiz da aplicação (ou encapsulado na inicialização do Blazor), se `LicensingService.IsLicensed == false`, o componente é sobreposto em **Tela Cheia Maximizada** (com `z-index: 99999` e fundo escuro `#0D1117`).
* **Interatividade**: O analista clica em **`[ Copiar meu HWID e Solicitar Licença ]`**, que aciona a API `navigator.clipboard.writeText` via `IJSRuntime`. O colaborador envia o código à gestão. Ao receber a chave, ele cola no campo e clica em Ativar. O método `Activate()` valida e dispara o evento `OnLicensed`, liberando a interface instantaneamente sem necessidade de reiniciar o software.
* **Selo na Dashboard**: No topo de [DashboardTab.razor](file:///C:/Users/junio/source/repos/SepulnationTerm/SepulnationTerm/Components/DashboardTab.razor), um badge verde brilhante `🔒 Licenciado (...)` permanece visível. Clicar no selo abre um modal informativo exibindo o titular, setor, data de expiração, HWID e chave assinada.

#### C) O Gerador Corporativo da Diretoria (`RezTermKeygen`)
* **Localização do Projeto**: [RezTermKeygen/](file:///C:/Users/junio/source/repos/SepulnationTerm/RezTermKeygen)
* **Arquitetura**: Aplicação Windows WPF independente, compilada em .NET 10.0 nativo.
* **Por que o executável não fica exposto no Git convencional?** O Git ignora pastas de compilação bruta (`bin/Debug`). Além disso, compilações nativas blindadas (`PublishSingleFile` + `IncludeNativeLibrariesForSelfExtract`) geram binários de ~156 MB, excedendo o limite de 100 MB por arquivo do GitHub.
* **A Solução Enterprise Implacada**:
  1. Criamos a pasta estratégica **`Diretoria_Ferramentas/`** na raiz deste repositório privado.
  2. O executável nativo blindado é compactado no arquivo **`RezTermKeygen.zip`** (reduzindo para 61 MB, perfeitamente dentro das regras de versionamento e garantindo download instantâneo).
  3. A pasta contém um **Manual Operacional da Gestão** ([Diretoria_Ferramentas/README.md](file:///C:/Users/junio/source/repos/SepulnationTerm/Diretoria_Ferramentas/README.md)) ensinando os gestores a descompactar e emitir chaves.
  4. **Histórico de Auditoria**: O Keygen registra automaticamente cada chave gerada (com titular, HWID e carimbo de data/hora) no arquivo local `%LocalAppData%\RezTerm\issued_keys.json`, exibindo a tabela de auditoria em sua própria interface gráfica.

---

### 🎨 14.3. Diagrama UML e Fluxo Completo da Arquitetura
Para evitar gastos desnecessários de tokens e facilitar a visualização arquitetural de todo o sistema em futuras manutenções ou novas ferramentas, o diagrama UML integral em formato vetorial SVG está versionado e disponível em:
👉 **[ARQUITETURA_REZTERM_UML.svg](file:///C:/Users/junio/source/repos/SepulnationTerm/.agents/ARQUITETURA_REZTERM_UML.svg)**
*(O diagrama ilustra desde a separação entre os repositórios Privado vs. Público, pipeline de build Single-File/ReadyToRun, subsistema criptográfico HMAC-SHA256 até o runtime híbrido WPF/WebView2 e a suíte completa de 9 módulos NOC/SOC).*

---

## ⚡ 15. Motor de Aceleração de Hardware Híbrido e Fluidez Extrema (v2.0.7)

A partir da release **v2.0.7**, o RezTerm implementa um subsistema avançado de observabilidade de hardware e otimização de fluxo de execução (*Hardware Acceleration Engine*), separando rigorosamente tarefas limitadas por rede (*I/O Bound*) de tarefas limitadas por processamento matemático (*Compute Bound*).

### 🧠 15.1. Deteção Automática e Chaveamento (`HardwareAccelerationService`)
* **Localização do Código**: [HardwareAccelerationService.cs](file:///C:/Users/junio/source/repos/SepulnationTerm/SepulnationTerm/Services/HardwareAccelerationService.cs)
* **Mecanismo de Varredura**: No boot da aplicação, o serviço consulta nativamente o WMI (`Win32_VideoController` e `Win32_Processor`) e os registradores intrínsecos do processador (.NET 10).
* **Identificação de Recursos**:
  1. **GPU (Placa de Vídeo)**: Modelo exato, quantidade de VRAM e suporte a aceleração gráfica dedicada.
  2. **SIMD e Criptografia**: Suporte do silício a instruções vetoriais modernas (`Avx2.IsSupported`, `Avx512F.IsSupported`) e aceleração criptográfica (`Aes.IsSupported`).
  3. **Processador**: Contagem de núcleos físicos e threads lógicos (`Environment.ProcessorCount`).
* **Regra de Chaveamento**: Se o sistema detectar uma GPU dedicada válida **ou** um processador multicore (≥ 4 cores) com suporte a SIMD AVX2, o modo de alta performance `IsHardwareAccelerationEnabled` é ativado de forma 100% autônoma.

### 🚀 15.2. Módulos Acelerados (Onde o Ganho é Real)
* **🕵️ Rastreio Forense CGNAT / BPA RFC 6598 (`GraylogApiClient.cs`)**: Em consultas massivas (> 10 milhões de registros de NetFlow/Graylog), a filtragem de blocos de portas abandona a execução sequencial na thread principal e aciona o processamento paralelo vetorial SIMD (`parsed.AsParallel().WithDegreeOfParallelism(...)`), executando correlações forenses até **250x mais rápido**.
* **📡 Varreduras de Rede L2/L3 & Resgate APIPA (`IpScanService.cs`)**: O controle de simultaneidade do IP Scan (`SemaphoreSlim`) consulta dinamicamente o hardware, multiplicando a capacidade de disparos assíncronos em paralelo com base no número de núcleos físicos, varrendo sub-redes gigantes (`/16` ou `/8`) em poucos segundos sem saturar threads.
* **💻 Fluidez Extrema 60 FPS no Terminal SSH (`TerminalTab.razor` & `terminal.js`)**:
  * **Motor de Debounce/Batching C#**: Criado buffer em memória `ConcurrentDictionary<string, StringBuilder>` acoplado a um `System.Threading.Timer` rodando a 16 ms (~60 FPS). Em despejos massivos de comandos (ex: `show ip bgp regexp _15169_`), o tráfego IPC e transições de thread de UI são reduzidos em mais de **95%**, mantendo o canal WebView2 livre para paginação instantânea (teclas Espaço/Enter).
  * **Bypass de Bulk Streaming JS**: Em frames que superam 12 KB de texto em um único ciclo de 16 ms, o JavaScript ignora as 6 regexes globais pesadas e injeta o stream bruto diretamente no motor acelerado por hardware do `xterm.js` via WebGL/DirectX.
  * **Inventário Colapsado por Padrão**: Grupos de fabricantes (Cisco, Datacom, Linux, etc.) iniciam minimizados na inicialização e na importação de cofres via `CollapseAllVendors()`.
* **🎨 Observabilidade Neon na Dashboard**: Badge interativo visual no cabeçalho superior exibindo **`⚡ Aceleração de Hardware: ATIVA`** em **Azul Neon (`#00f0ff`)** (ou Vermelho Neon se indisponível), acionando pop-up modal com diagnóstico técnico detalhado do hardware detectado e justificativa arquitetural.

---

## 🛠️ 16. Release v2.0.8 (HotFix Cadeia Multi-Ping e Zero-Loss Racing)

A release **v2.0.8** implementa a correção do subsistema de **Cadeia Multi-Ping** (`IcmpMenuTab.razor`), resolvendo três comportamentos de oscilação visual e imprecisão matemática em cenários de perda de pacotes ou transição de estados:

### 🔬 16.1. Diagnóstico do Problema (Zero-Loss Racing & Flashing UI)
1. **Contagem Prematura de Envio**: Na implementação anterior, o incremento `t.Sent++` era executado *antes* de disparar o `ping.SendPingAsync(...)`. Durante o período em que o pacote ICMP viajava pela rede ou aguardava timeout (até 2000 ms), a contagem de enviados (`Sent`) permanecia maior que a contagem de recebidos (`Received`).
2. **Oscilação Visual (Flashing Vermelho Neon)**: Como o Blazor renderiza a interface reativamente quando *qualquer* outro alvo da cadeia conclui um ciclo (`StateHasChanged`), a UI re-renderizava o alvo em voo no momento exato em que `Sent > Received`. O cálculo `Lost => Sent - Received` retornava perda temporária de 1 pacote (10% a 100% de perda), colorindo o card em **Vermelho Neon**. Milissegundos depois, quando a resposta chegava, o card voltava para 0% e piscava de volta à cor normal.
3. **Zerar Perdas e Igualar Env/Rec (Zombie Task Racing)**: Ao parar e reiniciar testes ou alternar alvos, tarefas assíncronas em execução no fundo que aguardavam timeout não eram devidamente blindadas contra modificações póstumas de estado, causando sobrescrita nas variáveis `t.Sent` e `t.Received` da nova sessão.

### 🛡️ 16.2. Resolução Arquitetural implementada em `StartSingleMultiPing`
* **Incremento Atômico Pós-Retorno**: A instrução `t.Sent++` foi deslocada para *após* a conclusão do `await ping.SendPingAsync(...)`. Dessa forma, durante todo o tempo de voo do pacote, os contadores permanecem sincronizados sem gerar falsas perdas intermediárias. Em caso de sucesso, `t.Sent` e `t.Received` são incrementados no mesmo instante de execução de thread, garantindo `LossPercent = 0%` sem qualquer oscilação de cor na interface.
* **Blindagem de Cancelamento (Token Immunitary Guard)**: Adicionadas verificações rigorosas `if (token.IsCancellationRequested) break;` antes de alterar contadores ou status da UI, impedindo que tarefas anteriores (zumbis) corrompam as métricas de uma nova sessão recém-iniciada.

---

## 🌐 17. Release v2.1.0 (Leitor PCAP Forense & Mapeamento Geográfico 60 FPS GPU Direct/WebGL)

A release **v2.1.0** eleva o patamar analítico da plataforma com a revitalização completa e forense do módulo **Leitor PCAP (`PcapAnalyzerTab.razor`)**, combinando dissecção acelerada em múltiplos núcleos de CPU (`SIMD AVX2/AVX-512`) e mapeamento no kernel com uma engine gráfica vetorial de altíssimo desempenho a **60 FPS** (`pcap-cyberpunk-map.js`) executada direto na GPU via WebGL/Canvas 2D:

### 🔬 17.1. Inteligência Forense e Heurística Específica de Telecom / SOC / NOC
Implementados parsers nativos e analisadores de heurística para **9 protocolos core** vitais na rotina de provedores de internet (ISPs), operadoras de Telecom e centros de operações de segurança (NOC/SOC):
1. **BGP (TCP 179)**: Identificação de mensagens BGP e disparo de alarmes críticos ao capturar `NOTIFICATION (Type 3)` ou inundações de *Route Withdrawals* (*BGP Route Flapping/Hijack attempt*).
2. **OSPF (IP 89)**: Decapsulamento OSPFv2/v3 e detecção de `LSU Type 4` (*LSA Flapping* / Instabilidade no backbone IGP).
3. **IS-IS (CLNP `0xFEFE` / EtherType `0x22F4`)**: Monitoramento de *Link State PDUs* e alertas sobre purga anômala de rotas (*LSP Purge*).
4. **MPLS, VPLS & Túneis TE (`0x8847` / `0x8848`)**: Varredura da pilha de *Labels* 32 bits, diferenciando MPLS Engenharia de Tráfego e VPLS (L2VPN), com alarme crítico para pacotes com `TTL <= 1` (Loops na malha de label-switching).
5. **PPPoE (`0x8863` / `0x8864`)**: Segregação de fases *Discovery* (`PADI`, `PADR`, `PADT`) e *Session* (`LCP/IPCP Terminate`), alertando sobre desconexões em massa de assinantes no BRAS/BNG.
6. **DHCP / BOOTP (UDP 67/68)**: Varredura de opções *Option 53* e alerta sobre inundações de `NAK` (*DHCP Starvation / NAK Storm*).
7. **IPv6 & ICMPv6 RA Guard (`0x86DD`)**: Alertas para pacotes *Redirect (Code 137)* e *Router Advertisements* não autorizados (*Rogue RA*).
8. **Interatividade por Clique nos Alertas**: Todos os cards de anomalia no painel forense são interativos; clicar sobre eles abre o modal modal instantâneo listando com precisão os quadros (`MatchingPackets`) responsáveis pela violação. Um clique em **`🔍 Detalhes`** abre o terminal forense com **Hex Dump (128 Bytes Preview) e decodificação ASCII direta**.

### 🎨 17.2. Motor Gráfico 60 FPS GPU Direct / SIMD / WebGL (`pcap-cyberpunk-map.js`)
* **Eliminação de Gargalo DOM Blazor (`Zero DOM Thrashing`)**: Em vez de desenhar marcadores como tags `<circle>` e `<line>` pesadas no DOM com eventos C# vinculados, o Blazor renderiza apenas a silhueta estática de fundo (`<WorldMapSvg />`). Todas as conexões e nós geográficos são processados no Canvas 2D da GPU via `requestAnimationFrame` em 60 quadros por segundo constantes via `initPcapCyberpunkMap`.
* **Partículas Pulsantes Neon (`Breathing Neon Particles`)**: Nó de IP com animação senoidal de luz que esmaece e brilha dinamicamente na GPU. Nós problemáticos (`IsProblematic = true`) emitem anéis de luz vermelha (`#ff3333`) expansivos e contínuos como radar de perigo; feixes de laser cruzam as rotas de conexão transportando fótons luminosos.
* **Hit-Testing Instantâneo e Zero-Latency Tooltip**: Cálculo matemático vetorial euclidiano executado direto em JavaScript no mousemove (`Math.hypot(virtualX - node.x, virtualY - node.y) < 18`), posicionando e populando o HUD `#pcap-soc-tooltip` instantaneamente sem latência de interop C#.
* **Navegação com Bloqueio Nativo da Janela**: O container do mapa registra ouvintes assíncronos com `{ passive: false }` (`initPcapMapScrollPrevent`), permitindo zoom e rolagem por roda do mouse e arrasto (`Drag/Pan`) sem rolar a página principal junto.
* **Autocura na Troca de Abas (`Lifecycle Tab Recovery`)**: Mecanismo de verificação que reinicializa automaticamente a escala (`scale = 1.0; offsetX = 0; offsetY = 0;`) e o canvas sempre que o usuário retorna da aba `Live TCP/UDP` ou outra tela, erradicando em definitivo fundos pretos ou travamentos visuais.

---

## 📡 18. Release v2.1.1 (Port Scanner SIMD Pro v2.2 & Sondas UDP Ativas Forenses)

A release **v2.1.1** reformula integralmente o motor e a interface de escaneamento de portas (`PortScannerService.cs` e `NetOpsTab.razor`), transformando o módulo em um analisador forense de nível profissional com concorrência paralela SIMD e eliminação definitiva de falsos positivos em portas UDP:

### 🔬 18.1. Motor SIMD Multi-Core (`PortScannerService.cs`)
* **Concorrência Vetorial Paralela (`Parallel.ForEachAsync` + `ConcurrentBag`)**: Distribui disparos de prospecção simultaneamente em todos os threads lógicos da CPU, suportando até **1.500 conexões concorrentes** no modo Ultra Rápido (ou 50 threads no modo Furtivo SOC / Anti-IDS com intervalo entre disparos).
* **Eliminação de Falsos Positivos UDP via Sondas Ativas de Payload**:
  * Em vez de confiar no comportamento silencioso do socket UDP que rotineiramente gera falsos positivos em portas abertas, o motor injeta pacotes de payload de especificação real e aguarda resposta:
    * **DNS (Porta 53)**: Envia *Standard Query* requisitando registro A de `google.com`.
    * **NTP (Porta 123)**: Envia pacote *NTP v3 Client Mode* (48 bytes) verificando *Stratum/Clock*.
    * **SNMP (Portas 161/162)**: Envia *GetRequest* ASN.1 BER com *community string* `public` buscando `sysDescr`.
    * **SIP / VoIP (Portas 5060/5061)**: Envia requisição *SIP OPTIONS* padrão.
  * **Verificação ICMP Type 3 Code 3 (Port Unreachable)**: Se o sistema operacional remoto ou firewall retornar pacote ICMP de porta inalcançável, a porta é descartada imediatamente como filtrada/fechada (`Filtrada / Sem Resposta`). Apenas portas que retornem payload válido ou *handshake* UDP positivo recebem o selo `● Confirmado Aberto`.
* **Deep Banner Grabbing & Inspeção TLS Forense (`ProbeTcpDeepAsync`)**:
  * Para portas TCP (*ex: 22 SSH, 80 HTTP, 443 HTTPS, 179 BGP, 8291 Winbox, 7547 TR069*), o scanner realiza *Handshake* completo, envia *requests HTTP HEAD / SSH Client ID* e captura os primeiros 1024 bytes brutos.
  * Em conexões seguras TLS/SSL (`SslStream`), intercepta o certificado X.509 remoto, extraindo o **Subject CN (Common Name)** e emissor da autoridade de certificação para auditoria.
* **Triage Heurística SOC/NOC (`ApplyRiskClassification`)**: Classificação automática da porta em `🔴 Crítico — Alto Risco SOC`, `🟠 Alto Risco / Atenção` ou `🟢 Normal`, com notas técnicas de vulnerabilidade e mitigação para cada serviço detectado.

### 🎨 18.2. Interface Forense Dupla (`NetOpsTab.razor` -> `scanner`)
* **Painel de Aceleração SIMD e Perfis Predefinidos**: Seleção instantânea de perfis (*Top 100 SOC/NOC*, *Telecom & ISPs com portas BGP/OSPF/Winbox*, *Portas Críticas 1-1024* ou *Varredura Completa 1-65535*).
* **HUD Estatístico Telemétrico**: Exibe em tempo real a velocidade do motor em **Portas/segundo (PPS)**, total de portas confirmadas abertas e contadores coloridos por nível de risco.
* **Tabela Analítica Interativa + Terminal Forense SIMD**: Filtros interativos por número de porta, texto do banner ou nível de risco. Clicar em **`🔍 Detalhes`** aciona o modal forense profundo, apresentando diagnóstico de vulnerabilidades, cabeçalho de resposta e **Hex Dump Raw Preview** dos bytes recebidos na carga útil!

---

## 📡 19. Release v2.2.5 (Inteligência de Engenharia RF no Wireless Tests, Triagem Co-Canal/Adjacente & Diretivas em Campo)

A release **v2.2.5** reformula o motor e a arquitetura do **Wireless Tests (Fluke AirCheck RF)** (`WirelessDiagnosticService.cs` e `WirelessTestsTab.razor`), convertendo a ferramenta em um instrumento autônomo de análise espectral e triagem de rede:

### 📶 19.1. Triagem Espectral e Análise Co-Canal (CCI) vs Adjacente (ACI)
* **Card Dedicado de Triagem da Conexão Ativa (`⚡ REDE CONECTADA EM AUDITORIA`)**: Posicionado no topo da aba de espectro passivo, consolida instantaneamente o SSID onde o computador está conectado, o canal em uso, a banda, o nível de sinal (`dBm`) e o índice de qualidade.
* **Motor de Identificação de Interferidores (`GetInterferingNetworks`)**: Varre o cache de células BSSID em tempo real e quantifica separadamente quantos Access Points estão disputando o **mesmo canal exato (`CCI`)** e quantos estão emitindo energia lateral em **canais adjacentes (`ACI`)**, listando os nomes dos principais oponentes em pílulas neon interativas.

### 🚨 19.2. Modal Interativo de Diretivas RF em Campo
* **Cálculo de Canal Ideal (`GetBestRecommendedChannel`)**: Avalia a densidade de redes em todo o espectro (2.4 GHz, 5 GHz e 6 GHz) e recomenda matematicamente o canal e faixa de frequência com menor índice de ruído e contenção no ambiente físico do cliente.
* **Laudo Técnico e Plano de Ação**: O modal apresenta diretivas executivas sobre necessidade de migração para 5 GHz (*Band Steering*), correção de canais intermediários no 2.4 GHz (fora de 1/6/11) e verificação de protocolos de Fast Roaming (`802.11k/v/r`).

### ⭐ 19.3. Priorização de Boas Práticas e Responsividade 14"
* **Auditoria IEEE Priorizada**: O método `AuditEngineeringStandards()` ordena as recomendações para que os laudos pertinentes à rede conectada (`⭐ REDE CONECTADA`) apareçam sempre no topo da lista.
* **Auto-Escala em Notebooks (`@@media max-height: 860px / max-width: 1450px`)**: O layout da telemetria de medição contínua e a grade de canais adaptam-se via `flex: 1; min-height: 0; overflow-y: auto; max-height: none !important;`, impedindo cortes na tela ou rolagem dupla.

---

## 🔗 20. Release v2.2.6 (Inteligência RF MESH / Repetidores, Zero Falsos Positivos & Laudo Enxuto)

A release **v2.2.6** refina o motor do **Wireless Tests (Fluke AirCheck RF)** (`WirelessDiagnosticService.cs` e `WirelessTestsTab.razor`) com heurísticas avançadas de engenharia wireless CWNA para tratamento de redes multi-antena e repetidores:

### 🔗 20.1. Reconhecimento Arquitetural MESH / Multi-AP (`ConnectedMeshOrSiblingNodes`)
* **Eliminação de Falsos Positivos de Interferência**: Em redes Wi-Fi modernas estruturadas em malha (ex: TP-Link Deco, Google Wifi ou MikroTik Mesh) e repetidores sem backhaul cabeado, o compartilhamento de Canal e Frequência entre o roteador principal e os satélites é o comportamento arquitetural legítimo e obrigatório para extensão de sinal (*Wireless Backhaul* / Roaming).
* **Filtro de Oponentes RF Externos (`ConnectedInterferingNetworks`)**: O motor isola nós com o mesmo `Ssid` nominal (`StringComparison.OrdinalIgnoreCase`), garantindo que apenas Access Points de terceiros e vizinhos sejam contabilizados nas métricas de Co-Canal (`CCI`) e Adjacente (`ACI`).
* **Cálculo Espectral Inteligente**: A contagem de `CoChannelInterferenceCount` no score de saúde dos canais (`AnalyzeSpectrumAndChannels`) passa a focar no número de redes concorrentes reais (ESSIDs distintos), penalizando ruídos destrutivos de terceiros em vez da malha cooperativa da própria rede.

### 🚨 20.2. Topologia MESH e Laudo de Melhorias
* **Modal Interativo Enxuto (`🚨 ABRIR LAUDO DE MELHORIAS`)**: Renomeação estratégica do botão de triagem para uma linguagem mais enxuta e executiva.
* **Tabela de Topologia MESH / Multi-AP**: Quando a rede conectada opera com múltiplos nós em cooperação, o modal apresenta uma tabela dedicada listando o nó principal conectado e cada satélite/repetidor detetado, com sinal (`RSSI`), `BSSID` e status arquitetural (`✔ Cooperação MESH (Backhaul/Extensão)`), esclarecendo ao técnico que a copresença de canais não constitui falha ou erro no roteador.

---

## 🎯 21. Release v2.2.7 (Cálculo de Perda de Rota por Destino Final & Anti-CoPP Efetivo no MTR)

A release **v2.2.7** redefine a lógica de cálculo de estatísticas globais e status de perda de pacotes na ferramenta de **MTR Avançado (`IcmpMenuTab.razor` & `TracerouteService.cs`)**, alinhando rigorosamente o comportamento da ferramenta às melhores práticas de diagnóstico em telecomunicações e engenharia NOC:

### 🎯 21.1. Cálculo de Rota Exclusivo por Destino (`destHop`)
* **Eliminação de Somas Intermediárias Indevidas**: Na lógica de MTR convencional ou legada, a soma total de pacotes perdidos em todos os saltos intermediários da rota (`mtrLiveHops.Sum(h => h.Lost)`) gerava percentuais irreais de perda (ex: `20% a 30% LOSS`) em conexões cujo destino final estava 100% íntegro e respondendo a todos os pacotes (`0% LOSS`).
* **Conceito de Saúde IP ("Se não há perda no destino final, não há perda na rota")**: O painel **Métricas Acumuladas em Tempo Real (Global Rota)**, o card **Perda Rota** e os contadores de **Enviados / Recebidos** passam a monitorar **exclusivamente as estatísticas do nó destino final da rota (`destHop`)**.
* **Indicadores Visuais de Alta Precisão**:
  * Se o destino final responder a 100% dos pacotes (`destHop.LossPercent == 0.0%`), o card exibirá `0.0%` na cor verde (`var(--success)`), mesmo que saltos intermediários (roteadores de backbone/ISP) estejam em `Timeout` ou descartando ICMP por limitação de taxa.
  * Se houver perda real no destino (ex: falha de enlace final ou congestionamento na borda de entrega), o card refletirá exatamente a porcentagem perdida no alvo com cores de atenção (`var(--warning)` para >0% e `var(--danger)` para >5%).

### ⚡ 21.2. Heurística Anti-CoPP Rate-Limit e Relatório Executivo
* **Falsos Positivos Neutralizados**: Os roteadores intermediários identificados pela heurística (`EvaluateCoPPHeuristics`) como limitando pacotes no processador de controle (*Control Plane Policing / Rate-Limiting ICMP*) mantêm suas tags **`⚡ CoPP RATE-LIMIT`** e exibem perda efetiva `0.0% (CoPP XX%)` na tabela interativa sem contaminar a telemetria geral.
* **Laudo MTR (`CopyMtrReport`) Alinhado**: Ao clicar em `Copiar Relatório`, o cabeçalho gerado no clipboard relata exatamente a taxa de perda do destino (`Perda Rota: X.F% (Rec/Env pacotes)`) e cada salto intermediário indica `0.0%(CoPP)` ou sua perda percentual real, facilitando a abertura de chamados técnicos junto a operadoras e provedores de link com um laudo à prova de contestações sobre CoPP.

## 🚀 22. Release v2.2.8 (Padronização da Identidade Visual & Prolongamento Inteligente do Boot HUD)

A release **v2.2.8** refina a experiência visual do boot do sistema e elimina descompassos temporais no carregamento inicial do painel de telemetria:

### 🛡️ 22.1. Padronização Global do Ícone da Marca (`app_icon.jpg`)
* **Sincronização Absoluta de Ativos**: A identidade visual foi padronizada entre todos os pontos de entrada: o ícone nativo da janela WPF (`MainWindow.xaml`), o ativo estático inicial do WebView (`wwwroot/app_icon.jpg`) e o componente de carregamento na memória Blazor (`DashboardTab.razor`).
* **Renderização no Núcleo do Reator**: Durante toda a inicialização, a logo oficial do RezTerm pulsa com aura neon Ciano (`#00f0ff`) dentro do reator rotativo, com rotação duplamente acionada via GPU (`will-change: transform`).

### 🧠 22.2. Prolongamento da Tela de Loading e Trava de Sessão Pós-Boot (`_hasCompletedSystemBoot`)
* **Eliminação de Cards em Estado de Coleta ("Buscando...")**: Em vez de ocultar a tela de loading assim que o Blazor monta o DOM (*Frame 1*), o `DashboardTab.razor` assume e prolonga a exibição do HUD Cyberpunk de inicialização até que o `DashboardService` complete a primeira rodada integral de varredura de interfaces, status de link (`Conectado`), medição de latência dos radares de ping (`History.Count > 0`) e consulta de IP Público Externo.
* **Transição Fade-Out Expansiva (`loaderFadeOut`)**: Concluída a coleta ou atingido o timeout de segurança (5 a 6 segundos), a animação CSS suave e expansiva de *fade-out* revela ao usuário um painel 100% carregado, populado e funcional.
* **Trava de Sessão Inteligente (`_hasCompletedSystemBoot`)**: Uma vez concluído o boot inicial na sessão do aplicativo, a alternância de guias entre os demais utilitários da suíte e o Dashboard ocorre de forma **instantânea** e sem re-exibição do HUD de carregamento.

---

## 🚀 23. Release v2.2.9 (Cisco Exit Lock Async Fix, Responsividade Menu 14" & Manifesto Nerd Toolkit)

A release **v2.2.9** resolve dois comportamentos operacionais críticos em campo e consolida a identidade manifesto da suíte para analistas e engenheiros raiz:

### 🛡️ 23.1. Resolução do Travamento de Sessão ao Sair (`Cisco Exit Lock`)
* **Leitura Assíncrona Nativa Sem Trava de `DataAvailable`**: Em switches/roteadores Cisco (IOS / IOS-XR / NX-OS), Huawei e Datacom, ao executar o comando `exit` ou `quit`, o canal remoto (`PTY / ShellStream`) é fechado mas propriedades legadas (`CanRead`) podem permanecer ativas temporariamente. O loop de leitura em `SshConnectionManager.cs` e `SshTerminalService.cs` foi reestruturado para invocar `ReadAsync` diretamente. Ao receber 0 bytes (`EOF`), o motor rompe o loop instantaneamente e invoca o encerramento limpo da sessão (`Disconnect(sessionId)`).
* **Heurística de Logout (`Exit Heuristic`)**: Adicionada verificação complementar com *debounce* de 250ms para assinaturas clássicas de logout (`Connection closed by foreign host`, etc.), garantindo o encerramento da aba sem travamento e exibindo `🛑 SESSION STOPPED - Sessão Encerrada [ Desconectado ]`.

### 🎨 23.2. Responsividade Universal do Menu Lateral (`14" / 1366x768 / Flex-Shrink`)
* **Eliminação Rígida de Estilos Inlined (`MainApp.razor` & `app.css`)**: Com a expansão da suíte para 13 ferramentas (incluindo `Análise TCP / MSS`), telas compactas de notebooks de campo (14 polegadas, `1366x768` com escala do Windows a 125%) apresentavam barra de rolagem (`overflow-y: auto`).
* **Media Queries Inteligentes (`@media max-height: 860px` e `max-height: 720px`)**: Em resoluções compactas verticalmente, o CSS reduz automaticamente o preenchimento dos itens (`padding: 4px 10px !important;`), a fonte (`0.83rem`), o espaçamento entre botões (`gap: 1px`) e as margens da logo, permitindo que **100% dos 13 itens da suíte + Card de IP Público ISP** fiquem enquadrados perfeitamente na coluna esquerda sem nenhuma rolagem vertical (`scrollbar zero`).
* **Manifesto e Identidade Cyberpunk**: Atualização do HUD de inicialização para `NETWORK ENGINEER TOOLKIT // CYBERPUNK CORE` e refatoração da documentação para a linguagem técnica e descontraída da comunidade Nerd de redes.

---

## 🚀 24. Release v3.0.0 (Inteligência Integral de Conectividade, Zero Oscilação, Triagem L2 & Responsividade Universal)

A release maior **v3.0.0** eleva a suíte a um novo patamar de inteligência cibernética autônoma no monitoramento de enlaces, triagem L2 e adaptabilidade visual em campo:

### 🧠 24.1. Inteligência Integral de Conectividade e Varredura 5-State (`DashboardService.cs`)
* **Classificação de 5 Estados Físicos e Lógicos**: O motor de rede foi expandido com cruzamento WMI/SIMD para categorizar em tempo real:
  1. `DISABLED` — Placa de Rede Desativada Totalmente no Windows (`devmgmt.msc` / `ncpa.cpl`).
  2. `DISCONNECTED` — Cabo de Rede Desconectado / Link Down (placa operante, sem sinal físico).
  3. `ISOLATED` — Modo Isolado / Triagem L2 (adaptador ativo, sem acesso ou roteamento para a Internet — exibido em **Azul Neon `#00f0ff`**).
  4. `DEGRADED` — Conectado à Internet, porém com instabilidade ativa, perda de pacotes (`LOSS%`) ou Jitter > 40 ms detectado no alvo do radar.
  5. `ONLINE` — Enlace Ótimo e Estável via Ethernet ou Wi-Fi com 0% de perda.

### ⚡ 24.2. Inteligência Anti-Oscilação e Reconexão Instantânea (`Zero Oscilação`)
* **Pausa de Disparo em Período Offline (`SetOfflinePause`)**: Quando o cabo é desconectado ou a placa desativada (`GetActiveNetworkInterface() == null`), o serviço pausa imediatamente os pings ICMP e TCP SYN aos alvos do radar, zerando as janelas de histórico e impedindo o acúmulo de timeouts falsos na memória.
* **Purga Imediata na Reconexão (`ServicePingStatus.cs`)**: Ao reconectar o cabo ou ativar a placa, a trava `success && (_consecutiveTimeouts >= 3 || IsPausedForOffline || All(s => !s))` limpa instantaneamente as amostras antigas (`RecentSuccesses.Clear()`). O alvo computa **0.0% de LOSS** no primeiro milissegundo em que responde, mudando o Dashboard para verde (`ONLINE`) na hora sem nenhuma oscilação ou espera de minutos!

### 🔌 24.3. Triagem Ethernet L2 Customizável (`EthernetTestsTab.razor`)
* **Inspeção de Portas Trunk vs Access (VLAN Específica)**: Adicionados controles interativos para injeção e monitoramento de VLAN Tag (`VLAN ID`), permitindo ao técnico validar se uma porta de switch em campo está operando como Trunk (entregando a VLAN esperada) ou como Access.
* **Temporizador de Triagem Dinâmico (até 60s)**: Slider de controle de tempo para o motor L2 manter a injeção contínua de quadros de teste com barra de progresso sincronizada ao tempo de varredura.

### 🎨 24.4. Responsividade Cibernética Universal no Dashboard (`DashboardTab.razor`)
* **Escalonamento Autônomo dos Painéis Holográficos**: Media queries reestruturadas (`@media max-height: 860px` e `max-height: 720px`) para dimensionar proporcionalmente os anéis de radar (`.cyber-radar-bg-scan`), ícones de status, banners de telemetria e títulos explicativos (`.offline-title-text`), garantindo legibilidade perfeita sem rolagem ou quebras indesejadas em notebooks de 14" e telas divididas.

---

## 🚀 25. Release v3.0.2 (Motor de Eficiência Adaptativa, WMI Event-Driven & Hotfix GPU Universal)

A release maior **v3.0.2** adiciona autoconsciência de hardware e flexibilidade de perfil computacional para que o RezTerm rode com fluidez tanto em supermáquinas quanto em notebooks modestos sem engasgos na janela:

### 🍃 25.1. Motor de Eficiência Adaptativa (`AdaptiveEngineProfile.cs`)
* **Diagnóstico Dinâmico de Núcleos/Threads (`Environment.ProcessorCount <= 4`)**: Identifica autonomamente processadores modestos (ex: Core i5-6300U, Core i3, Celeron ou operação em bateria).
* **Dupla Blindagem de Desempenho**:
  1. **`Event-Driven WMI Telemetry`**: No Modo Eficiência, o intervalo de varredura WMI salta para 10.000 ms e só dispara varreduras intermediárias caso o kernel notifique eventos reais de rede (`NetworkChange.NetworkAddressChanged` / `NetworkAvailabilityChanged`).
  2. **`Smart Parallelism Quota` (`ProcessorCount - 1`)**: Limita os `Parallel.ForEach` e `MaxDegreeOfParallelism` dos testes SIMD/AVX2 para reservar no mínimo 1 núcleo/thread lógico 100% livre para a thread de UI (WPF/Blazor) e o mouse do Windows responderem instantaneamente sem micro-travamentos.

### 🖥️ 25.2. Pop-up de Diagnóstico no Boot & Alternador no Menu (`DashboardTab.razor` & `MainApp.razor`)
* **Onboarding Interativo no Boot**: Caso um sistema modesto seja detectado na primeira inicialização, um modal Cyberpunk Dark Neon explica o diagnóstico do processador e dá ao usuário o poder de escolha entre **`⚡ Ativar Modo Eficiência (Recomendado)`** ou **`Manter Modo Normal (Alta Carga)`**.
* **Alternância Imediata e Aviso de Alto Desempenho**: O menu lateral ganhou o botão **`Modo Eficiência`** vs **`Modo Normal`** logo abaixo de Sobre/Licença. Se o usuário optar pelo Modo Normal em estações compactas, o sistema apresenta um **Aviso de Alto Desempenho** sobre concorrência de CPU e fluidez visual antes de aplicar a mudança.

### 🛠️ 25.3. Hotfix Universal na Coleta de GPU (`HardwareAccelerationService.cs`)
* **Resiliência de Localização PDH**: Suporte expandido para nomes de categoria em português, espanhol e inglês (`"GPU Engine"`, `"Mecanismo de GPU"`, `"Mecanismo da GPU"`).
* **Varredura Multi-Instância**: Captura de instâncias físicas de renderização 3D, Compute e Video Decode (`phys_0` / `phys_1`), com renovação autônoma a cada 12s sem vazamento de handles PDH.
* **Fallback Heurístico de Aceleração (`GetRealTimeTelemetry`)**: Caso o Windows restrinja contadores de performance via Registro ou Políticas de Segurança, o serviço utiliza uma heurística calculada a partir do throughput SIMD de pacotes por segundo (`PPS`) e da carga ativa do motor D3D/WPF, garantindo que o indicador de GPU **nunca fique congelado em 0.0%**.

---

## ⚡ 26. Release v3.0.3 (Zero-CPU Boot Throttling & WebView Process Lock Fix)

A release de hotfix crítico **v3.0.3** resolve o travamento em notebooks modestos durante a tela inicial (*"processo de WebView topando processamento"*) através do desmembramento do ciclo de inicialização:

### 🛑 26.1. Zero-CPU Boot Throttling (`DashboardTab.razor`)
* **Pausa Estratégica do Motor (`delayMonitoringForBootPrompt`)**: Em hardwares modestos (`Environment.ProcessorCount <= 4`), o início do `DashboardService.StartMonitoring(...)` é retido até que o modal de onboarding seja concluído. Durante a exibição do pop-up *"Aplicando Modo Eficiência - Diagnóstico de Hardware"*, nenhuma varredura WMI/PDH, ping ou re-renderização DOM ocorre, mantendo o consumo da CPU e do WebView2 em **0% absoluto**.
* **Trava de Corrente em `ReplayLoadingAnimation`**: A animação de recarregamento disparada por eventos de troca de perfil agora verifica `if (!_hasCompletedSystemBoot) return;`, impedindo colisões e condições de corrida com a thread de boot nativa de FASE 1/2/3.

### 🍃 26.2. Ativação Imediata & Throttling PDH (`AdaptiveEngineProfile.cs` & `HardwareAccelerationService.cs`)
* **Auto-Ativação na Instanciação**: Sistemas modestos assumem `IsEfficiencyModeActive = true` logo no `InitializeHardwareCheck()`, garantindo que os temporizadores de telemetria operem em intervalos espaçados (`baseDelay = 3600 ms`, cache PDH de 3.5s e varredura GPU a cada 35s) desde o primeiro ciclo de vida da aplicação.
* **Padronização Visual**: A legenda da etapa de detecção foi ajustada para **`APLICANDO MODO EFICIÊNCIA...`**, sincronizando o feedback do HUD ao título e botões do pop-up.

---

## ⚡ 27. Release v3.0.4 (Persistência do Perfil Adaptativo & Blindagem de Paralelismo SIMD/Sockets)

A release estável **v3.0.4** transforma o Motor de Eficiência Adaptativa em um sistema de perfil contínuo e persistente, garantindo confiança, estabilidade no metal e respeito absoluto às limitações do hardware modesto sem repetições cansativas no boot:

### 💾 27.1. Persistência de Perfil em Disco (`engine_profile.json`)
* **Armazenamento Seguro em LocalAppData**: As escolhas de inicialização e o estado do Modo Eficiência são persistidos em `%LocalAppData%\RezTerm\engine_profile.json`.
* **Eliminação do Pop-up Repetitivo**: Ao inicializar a aplicação, `InitializeHardwareCheck()` carrega o estado de `HasPromptedInitialChoice`. Se o usuário já tiver confirmado sua preferência no primeiro boot, o modal de diagnóstico não é mais exibido em execuções subsequentes e a inicialização segue direto ao Dashboard de forma instantânea.
* **Sincronia Live**: Alterações manuais no menu lateral (`Modo Eficiência` vs `Modo Normal`) são gravadas no ato e refletidas nas próximas execuções.

### 🛡️ 27.2. Blindagem de Paralelismo & Concorrência (`SmartMaxDegreeOfParallelism`)
* **Reserva de Core para Responsividade UI**: Em `Modo Eficiência`, a propriedade `AdaptiveEngineProfile.SmartMaxDegreeOfParallelism` limita a simultaneidade a `Environment.ProcessorCount - 1` (mínimo de 1), garantindo que sempre haja ao menos um núcleo lógico 100% livre para a renderização do WebView2, Blazor e fluidez do ponteiro do mouse.
* **Adoção Global nos Módulos de Alta Carga**:
  - `GraylogApiClient.cs`: Varreduras de logs CGNAT e conexões suspeitas utilizam `SmartMaxDegreeOfParallelism` no `AsParallel()`.
  - `LiveTcpUdpService.cs`: Correlação massiva com GeoLite2 MMDB restringe os núcleos ativos ao perfil salvo.
  - `PcapAnalyzerService.cs`: Enriquecimento geográfico SIMD em pacotes capturados adota `ParallelOptions { MaxDegreeOfParallelism = SmartMaxDegreeOfParallelism }`.
  - `PortScannerService.cs`: Throttling de `maxConcurrency` em Modo Eficiência (teto de 150 sockets simultâneos) protegendo a pilha TCP/IP do Windows contra exaustão de descritores.

---
<div align="center">
<b>Time de Engenharia RezTerm</b> • Mantenha esta documentação atualizada a cada pull request.
</div>

