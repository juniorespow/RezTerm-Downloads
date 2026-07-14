# ⚡ RezTerm v2.2.9 (Network Engineer Toolkit)

<div align="center">

![.NET Core](https://img.shields.io/badge/.NET%2010.0-512BD4?style=for-the-badge&logo=dotnet&logoColor=white)
![Blazor Hybrid](https://img.shields.io/badge/Blazor%20Hybrid-5C2D91?style=for-the-badge&logo=blazor&logoColor=white)
![WPF](https://img.shields.io/badge/Windows%20WPF-0078D4?style=for-the-badge&logo=windows&logoColor=white)
![C#](https://img.shields.io/badge/C%23%2013-239120?style=for-the-badge&logo=c-sharp&logoColor=white)
![Security](https://img.shields.io/badge/Security-DPAPI%20%2B%20HMAC-00f0ff?style=for-the-badge)
![Hardware Acceleration](https://img.shields.io/badge/HW%20Acceleration-GPU%20%2B%20SIMD-00ff88?style=for-the-badge)
![RF Intelligence](https://img.shields.io/badge/RF%20Fluke%20Engine-MESH%20Triage-00f0ff?style=for-the-badge)

**A Suíte Definitiva de Engenharia de Redes, Diagnóstico SOC/NOC, Auditoria Forense, Leitura PCAP SIMD e Terminal SSH Multi-Aba.**  
Desenvolvido na marra por **Reginaldo Junior**, um Engenheiro de Redes cansado de ver analistas pagando fortunas de licenças anuais por softwares fechados, lentos, cheios de burocracia e paywalls. O **RezTerm** nasceu da necessidade de enxugar custos em ambientes que é apenas disponibilizado máquinas com Windows para se trabalhar: uma suíte  de diagnóstico e monitoramento, rodando direto no metal do Windows (.NET 10 WPF / ReadyToRun Native) com uma interface ultramoderna Blazor Hybrid em estética **Cyberpunk Dark Neon**.

---

### 🚨 AVISO DE LICENCIAMENTO E PROPRIEDADE INTELECTUAL
**O RezTerm é um software proprietário com controle de licença criptográfica.**  
O acesso é restrito e exige autenticação vinculada ao hardware deste computador (HWID). O download ou tentativa de uso não autorizado sem chave criptográfica válida é monitorado e bloqueado pela arquitetura de segurança do sistema.

</div>

---

## 📥 1. Como Baixar e Instalar (Release v2.2.9)

A distribuição do **RezTerm** é realizada via assistente de instalação blindado que configura o ambiente no perfil do técnico sem exigir privilégios de administrador global (`%LocalAppData%\RezTerm`):

1. **Baixe o Instalador Oficial**: Acesse a aba [Releases](https://github.com/juniorespow/RezTerm-Downloads/releases/latest) deste repositório e faça o download do arquivo **`RezTermSetup.exe`**.
2. **Execute o Assistente**: Abra o `RezTermSetup.exe`. Ele baixará automaticamente o payload blindado e criará os atalhos na Área de Trabalho e Menu Iniciar com o novo ícone Cyberpunk Neon.
3. **Atualização Automática via CDN**: O software possui verificação contínua de novas versões em segundo plano. Sempre que a equipe de engenharia lançar um patch de segurança ou nova ferramenta, você será notificado no topo do sistema para atualizar em 1 clique.

---

## 🔑 2. Como Ativar sua Licença Corporativa (HWID)

Na primeira execução do **RezTerm**, o sistema iniciará em **Tela Cheia Maximizada** apresentando a tela modal de bloqueio de segurança:

1. **Copie seu Código Único (HWID)**: Clique no botão **`[ Copiar meu HWID e Solicitar Licença ]`**. O sistema gerará um hash de 12 caracteres único da sua placa-mãe e processador (ex: `REZ-8F9A-2B1C-4D5E`).
2. **Envie para a Gestão do Sistema**: Abra chamado ou envie uma mensagem direta ao administrador/gestor responsável informando seu Nome, Setor e o código HWID copiado.
3. **Ative o Sistema**: O administrador emitirá uma chave criptográfica **HMAC-SHA256** (ex: `REZ-PRO-20270706-XXXX-XXXX-XXXX-SIG16`). Cole essa string no campo da tela de bloqueio e clique em **Ativar e Desbloquear Sistema**.
4. **Verificação de Validade**: Após desbloqueado, o status de sua licença ficará sempre visível no topo do Dashboard através do selo verde `🔒 Licenciado (...)`. Ao clicar no selo, você poderá consultar todos os detalhes da sua concessão corporativa.

---

## 🛠️ 3. Suíte de Ferramentas Integradas (v2.2.9)

| Módulo | Descrição Principal | Destaques de Engenharia |
| :--- | :--- | :--- |
| **📶 Wireless Tests RF (`v2.2.6`)** | Analisador de espectro Wi-Fi e qualidade de sinal em tempo real (Fluke AirCheck RF). | **Inteligência MESH / Zero Falsos Positivos (`v2.2.6`)**: Algoritmo que reconhece automaticamente redes MESH Wi-Fi (ex: TP-Link Deco, Google Wifi) e repetidores operando no mesmo SSID e Canal, excluindo-os da contagem de interferência co-canal (`CCI`) e separando redes concorrentes externas de nós cooperativos (`ConnectedMeshOrSiblingNodes`); **Modal Cyberpunk Interativo (`🚨 ABRIR LAUDO DE MELHORIAS (@conn.Ssid)`)** com tabela dedicada de **Topologia MESH / Multi-AP**, indicação do canal mais limpo do local (`GetBestRecommendedChannel`), recomendações de Band Steering para 5 GHz e auditoria de Fast Roaming 802.11k/v/r; **Auditoria IEEE Priorizada (`⭐ REDE CONECTADA`)** no topo da aba de boas práticas e **Responsividade Inteligente para Notebooks de 14" (`1366x768`)** na tabela de telemetria e no grid de canais. |
| **📊 Dashboard & Latência (`v2.2.9`)** | Monitoramento em tempo real da saúde da conexão e dual-stack ISP. | **Responsividade Inteligente Universal (`v2.2.9`)** no menu lateral 14" (`scrollbar zero`) e sub-blocos (*Download & Upload*, *Top Talkers*, *Radar de Latência*, *Operational Network* e *Engine Health*), **HUD de Boot Atualizado** com legenda `NETWORK ENGINEER TOOLKIT // CYBERPUNK CORE`, **HotFix GPU Load (`v2.2.2`)** com suporte universal NVIDIA/Intel/AMD e exibição `0.0%` sem `N/A`, **Precisão Absoluta em Memória RAM (`GlobalMemoryStatusEx`)**, **Motor Híbrido Anti-CoPP Rate-Limit (TCP SYN Bypass em portas 80/443)** para evitar alarmes falsos de queda, Gateway Dual e Badge de Aceleração GPU/SIMD. |
| **📡 Leitor PCAP Forense (`v2.1.0`)** | Analisador e dissecador forense de pacotes (.pcap/.pcapng) com aceleração SIMD e mapeamento no kernel. | **Motor Gráfico 60 FPS GPU Direct Canvas/WebGL (`pcap-cyberpunk-map.js`)** com luzes pulsantes esmaecendo e brilhando (*Breathing Neon Particles*), **Zoom/Pan com bloqueio nativo de rolagem da janela (`{passive: false}`)** e resiliência a abas; **Heurística de Redes, NOC e SOC** para 9 protocolos core (`BGP`, `OSPF`, `IS-IS`, `MPLS/VPLS`, `PPPoE`, `DHCP`, `IPv6 RA Guard`), inspeção interativa de quadros com Hex Dump e ASCII, botão de upload personalizado e popup de aviso forense. |
| **💻 Terminal SSH Studio (`v2.2.9`)** | Client SSH multi-aba de alta performance com `xterm.js`. | **Correção do Bug de Travamento Cisco Exit Lock (`v2.2.9`)**: Desconexão instantânea e liberação limpa de PTY/ShellStream ao digitar `exit` em equipamentos Cisco, Huawei ou Datacom sem prender a aba; **Fluidez Extrema a 60 FPS** via debouncing buffer C# (16ms) e bypass streaming JS para comandos >12KB, **Sincronização Dinâmica SIGWINCH** (`htop`/`btop`), **Syntax Highlighting** e **Copiar Tudo Buffer**. |
| **🏓 Ping & Trace Suite (`v2.2.3`)** | Motores avançados de ICMP, Ping Contínuo, Cadeia Multi-Ping e MTR. | **Responsividade no MTR Avançado (`v2.2.3`)**: Painel superior multi-linha com auto-escalonamento (`min-width: 240px`); **Motor Inteligente Anti-CoPP Rate-Limit 3 Fases (Heurística de Salto Intermediário vs Destino + Poisson Jittering + TCP SYN Bypass)** com selo azul neon **`⚡ CoPP BYPASS`**, **Cadeia Multi-Ping** com laudo formatado, **Seletor de Pilha IP (IPv4/IPv6/Auto)** e **Cálculo de Jitter RFC 3393** isolado no MTR. |
| **📡 IP Scan & Port Scanner SIMD (`v2.1.1`)** | Varredura minuciosa de sub-redes locais e auditoria forense de portas (`Port Scanner SIMD Pro v2.2`). | **Aceleração SIMD Multi-Core Paralela** (até 1.500 threads com *throttling* adaptativo de rede), **Eliminação de Falsos Positivos UDP via Sondas Ativas de Payload** (DNS, NTP, SNMP, SIP + detecção de ICMP Port Unreachable), **Deep Banner Grabbing & Inspeção TLS Forense** com captura de certificado X.509, **Triage de Risco SOC (`Crítico/Alto/Normal`)** com notas de mitigação e **Hex Dump Preview Raw**, além de exportação de laudos CSV em tempo real via **`rezTermFileSave`**. |
| **⚡ Live TCP/UDP Watcher** | Monitoramento de sockets abertos e conexões ativas no Windows. | Integração nativa com **GeoLite2 MMDB em Memória (MMF)** projetando conexões em **Mapa Mundi interativo**. |
| **🌐 NetOps & Whois/IRR** | Consulta unificada a bases mundiais de registro de IPs e ASNs. | Conectores diretos para RADB, RIPE, LACNIC, ARIN, APNIC e AFRINIC com formatação de blocos BGP. |
| **🔌 Ethernet Tests L2** | Verdadeiro "Fluke de Software" operando na Camada de Enlace (L2). | Escuta passiva LLDP/CDP/MNDP, injeção ativa de **PADI Broadcast (PPPoE Rogue)** e **DHCP Discover**. |
| **🕵️ Rastreio Forense CGNAT** | Investigação forense em servidores Graylog com geração de relatórios. | **Aceleração Vetorial SIMD AVX2/AVX-512 Paralela** (até 250x mais rápido), **Modo Híbrido Bimodal**, cálculo de blocos **Cisco BPA (RFC 6598)** e exportação em PDF/TXT com cláusulas jurídicas e hash SHA-256. |

---

## 🚀 4. Destaques da Evolução Arquitetural (`v2.2.9`)

### ⚡ Release v2.2.9 (Cisco Exit Lock Async Fix, Responsividade Menu 14" & Manifesto Nerd Toolkit)
* **Resolução do Travamento SSH ao Sair (`Cisco Exit Lock`)**: Reestruturação da leitura do stream assíncrono (`SshConnectionManager` e `SshTerminalService`) sem travas no buffer `DataAvailable`. Deteção imediata de EOF (`ReadAsync == 0 bytes`) acoplada a heurística de encerramento de sessão com *debounce* de 250ms, garantindo fechamento instantâneo da sessão com aviso visual `🛑 SESSION STOPPED - Sessão Encerrada [ Desconectado ]` em roteadores/switches Cisco, Huawei, Datacom e MikroTik.
* **Responsividade Universal no Menu Lateral para Notebooks 14" (`1366x768`)**: Compressão autônoma via media queries (`@media max-height: 860px` e `720px`) com auto-escala CSS do flex-shrink e espaçamento entre botões (`gap: 1px`), permitindo que 100% dos 13 itens da suíte e o card de IP Público fiquem acomodados sem nenhuma barra de rolagem vertical (`scrollbar zero`).
* **HUD de Inicialização Cyberpunk**: Atualização da legenda de carregamento para `NETWORK ENGINEER TOOLKIT // CYBERPUNK CORE`.

### 🚀 Release v2.2.8 (Padronização da Identidade Visual & Boot HUD)
* **Padronização Global do Ícone da Marca (`app_icon.jpg`)**: Sincronização da logo oficial entre a inicialização WebView (`wwwroot/app_icon.jpg`), ícone nativo da janela WPF (`MainWindow.xaml`) e centro do reator ciano no HUD da tela de loading.
* **Prolongamento do Boot HUD no Dashboard (`DashboardTab.razor`)**: O motor de interface estende a exibição do HUD Cyberpunk de inicialização até que todas as 3 fases fundamentais de coleta (`Placas L2 / Status Conectado`, `Radares de Ping` e `IP Público Externo`) estejam completas.

### 🎯 Release v2.2.7 (Cálculo de Perda de Rota por Destino Final & Anti-CoPP Efetivo no MTR)
* **Cálculo da Rota Exclusivo pelo Destino Final (`IcmpMenuTab.razor`)**: O cálculo de **Perda de Rota** e os contadores globais de **Enviados / Recebidos** no MTR Avançado passaram a ser 100% baseados na conectividade com o nó destino da rota (`destHop`). Se não houve perda de pacotes no destino final (`0.0%`), a rota inteira é classificada como saudável com `0.0% LOSS`.
* **Neutralização de Falsos Positivos de Drops Intermediários (CoPP Rate-Limit)**: Descartados intermediários por limitação de processador exibem **`⚡ CoPP RATE-LIMIT`** (`0.0% (CoPP XX%)`) na tabela e no relatório exportado sem contaminar a telemetria geral.

### 🔗 Release v2.2.6 (Inteligência RF MESH / Repetidores & Zero Falsos Positivos)
* **Reconhecimento Arquitetural MESH / Multi-AP (`ConnectedMeshOrSiblingNodes`)**: Em redes Wi-Fi em malha e repetidores sem cabo de rede, os satélites compartilham o mesmo SSID, Canal e Frequência para realizar o *Wireless Backhaul*. O motor identifica automaticamente as antenas cooperativas, separando ruído de terceiros do comportamento correto do roteador.
* **Score de Saúde de Canal (`AnalyzeSpectrumAndChannels`)**: Penalização focada em **ESSIDs concorrentes reais (`distinctSsids.Count`)**, exibindo o status: `🟢 Topologia MESH / Multi-AP (Compartilhamento Legítimo de Canal)`.
* **Modal Interativo Enxuto (`🚨 ABRIR LAUDO DE MELHORIAS (@conn.Ssid)`)**: Ação direta com tabela dedicada de **Topologia MESH cooperativa**, listando nó principal (`⭐`) e satélites (`🔗`).

---

## 🛡️ 5. Arquitetura de Segurança & Blindagem

1. **Compilação Blindada (*Single-File ReadyToRun Native*)**:
   - Os executáveis são compilados em código de máquina nativo (`win-x64`) com desativação total de símbolos de debug (`DebugSymbols=false`), impedindo ataques de engenharia reversa via ILSpy/dnSpy.
2. **Cofre Criptográfico DPAPI + HMAC-SHA256 (`HostStorageService`)**:
   - Nenhuma senha, chave privada SSH, token de API ou chave de licença é gravada em texto plano no disco.
   - O sistema utiliza a **DPAPI (Data Protection API) do Windows** acoplada ao perfil do usuário (`DataProtectionScope.CurrentUser`) e reforçada com verificação de integridade **HMAC-SHA256**.
3. **Observabilidade com Mascaramento de Dados**:
   - Logs estruturados em JSON Lines (`.jsonl`) rotativos, que executam mascaramento automático de credenciais (*Data Masking*), substituindo senhas e tokens por `"***MASKED***"`.

---
<div align="center">
<b>RezTerm Network Engineer Toolkit</b> • Engenharia Cibernética de Alta Performance<br>
<i>Reginaldo Junior • Todos os Direitos Reservados</i>
</div>

