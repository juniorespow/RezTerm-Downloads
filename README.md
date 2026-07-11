# ⚡ RezTerm v2.2.6 (Cyberpunk SOC/NOC & Forensics PCAP Suite - Telecom Edition)

<div align="center">

![.NET Core](https://img.shields.io/badge/.NET%2010.0-512BD4?style=for-the-badge&logo=dotnet&logoColor=white)
![Blazor Hybrid](https://img.shields.io/badge/Blazor%20Hybrid-5C2D91?style=for-the-badge&logo=blazor&logoColor=white)
![WPF](https://img.shields.io/badge/Windows%20WPF-0078D4?style=for-the-badge&logo=windows&logoColor=white)
![C#](https://img.shields.io/badge/C%23%2013-239120?style=for-the-badge&logo=c-sharp&logoColor=white)
![Security](https://img.shields.io/badge/Security-DPAPI%20%2B%20HMAC-00f0ff?style=for-the-badge)
![Hardware Acceleration](https://img.shields.io/badge/HW%20Acceleration-GPU%20%2B%20SIMD-00ff88?style=for-the-badge)
![RF Intelligence](https://img.shields.io/badge/RF%20Fluke%20Engine-MESH%20Triage-00f0ff?style=for-the-badge)

**A Suíte Definitiva de Engenharia de Redes, Diagnóstico SOC/NOC, Auditoria Forense e Terminal SSH Multi-Aba.**  
Desenvolvida por **Reginaldo Junior (Razon)** combinando a performance nativa do Windows (.NET 10 WPF / ReadyToRun Native) com uma interface ultramoderna Blazor Hybrid em estética **Cyberpunk Dark Neon**, **Inteligência RF MESH / Repetidores no Wireless Tests (`v2.2.6`)**, **Responsividade Universal Auto-Ajustável (`v2.2.5`)**, **Processo Nativo `RezTerm.exe` no Windows Task Manager (`v2.2.3`)**, **Telemetria Nativa de RAM/GPU (`v2.2.2`)** e motor de **Aceleração de Hardware Híbrida (GPU + SIMD)** com **Inteligência Anti-CoPP 3 Fases**.

---

### 🚨 AVISO DE LICENCIAMENTO E PROPRIEDADE INTELECTUAL
**O RezTerm é um software proprietário corporativo da Diretoria Telecom.**  
O acesso é estritamente restrito e exige autenticação de licença vinculada ao hardware deste computador (HWID). O download ou tentativa de uso não autorizado sem chave criptográfica válida é monitorado e bloqueado pela arquitetura de segurança do sistema.

</div>

---

## 📥 1. Como Baixar e Instalar (Release v2.2.6)

A distribuição do **RezTerm** é realizada via assistente de instalação blindado que configura o ambiente no perfil do técnico sem exigir privilégios de administrador global (`%LocalAppData%\RezTerm`):

1. **Baixe o Instalador Oficial**: Acesse a aba [Releases](https://github.com/juniorespow/RezTerm-Downloads/releases/latest) deste repositório e faça o download do arquivo **`RezTermSetup.exe`**.
2. **Execute o Assistente**: Abra o `RezTermSetup.exe`. Ele baixará automaticamente o payload blindado e criará os atalhos na Área de Trabalho e Menu Iniciar com o novo ícone Cyberpunk Neon.
3. **Atualização Automática via CDN**: O software possui verificação contínua de novas versões em segundo plano. Sempre que a Diretoria Telecom lançar um patch de segurança ou nova ferramenta, você será notificado no topo do sistema para atualizar em 1 clique.

---

## 🔑 2. Como Ativar sua Licença Corporativa (HWID)

Na primeira execução do **RezTerm v2.2.2**, o sistema iniciará em **Tela Cheia Maximizada** apresentando a tela modal de bloqueio de segurança:

1. **Copie seu Código Único (HWID)**: Clique no botão **`[ Copiar meu HWID e Solicitar Licença ]`**. O sistema gerará um hash de 12 caracteres único da sua placa-mãe e processador (ex: `REZ-8F9A-2B1C-4D5E`).
2. **Envie para a Diretoria Telecom**: Abra chamado ou envie uma mensagem direta ao gestor responsável informando seu Nome, Setor e o código HWID copiado.
3. **Ative o Sistema**: A Diretoria emitirá uma chave criptográfica **HMAC-SHA256** (ex: `REZ-PRO-20270706-XXXX-XXXX-XXXX-SIG16`). Cole essa string no campo da tela de bloqueio e clique em **Ativar e Desbloquear Sistema**.
4. **Verificação de Validade**: Após desbloqueado, o status de sua licença ficará sempre visível no topo do Dashboard através do selo verde `🔒 Licenciado (...)`. Ao clicar no selo, você poderá consultar todos os detalhes da sua concessão corporativa.

---

## 🛠️ 3. Suíte de Ferramentas Integradas (v2.2.6)

| Módulo | Descrição Principal | Destaques de Engenharia |
| :--- | :--- | :--- |
| **📶 Wireless Tests RF (`v2.2.6`)** | Analisador de espectro Wi-Fi e qualidade de sinal em tempo real (Fluke AirCheck RF). | **Inteligência MESH / Zero Falsos Positivos (`v2.2.6`)**: Algoritmo que reconhece automaticamente redes MESH Wi-Fi (ex: TP-Link Deco, Google Wifi) e repetidores operando no mesmo SSID e Canal, excluindo-os da contagem de interferência co-canal (`CCI`) e separando redes concorrentes externas de nós cooperativos (`ConnectedMeshOrSiblingNodes`); **Modal Cyberpunk Interativo (`🚨 ABRIR LAUDO DE MELHORIAS (@conn.Ssid)`)** com tabela dedicada de **Topologia MESH / Multi-AP**, indicação do canal mais limpo do local (`GetBestRecommendedChannel`), recomendações de Band Steering para 5 GHz e auditoria de Fast Roaming 802.11k/v/r; **Auditoria IEEE Priorizada (`⭐ REDE CONECTADA`)** no topo da aba de boas práticas e **Responsividade Inteligente para Notebooks de 14" (`1366x768`)** na tabela de telemetria e no grid de canais. |
| **📊 Dashboard & Latência (`v2.2.2`)** | Monitoramento em tempo real da saúde da conexão e dual-stack ISP. | **Responsividade Universal Auto-Ajustável (Flexbox)** sem rolagem externa dupla, **Telemetria Nativa de RAM (`GlobalMemoryStatusEx`)** sincronizada com o Gerenciador de Tarefas, **HotFix GPU Load Universal (`NVIDIA`, `Intel`, `AMD`)** com `0.0%` sem `N/A`, **Motor Híbrido Anti-CoPP Rate-Limit (TCP SYN Bypass em portas 80/443)** para evitar alarmes falsos de queda, **Poisson Random Jittering & Exponential Backoff Pacing**, Gateway Dual e Badge de Aceleração GPU/SIMD. |
| **📡 Leitor PCAP Forense (`v2.1.0`)** | Analisador e dissecador forense de pacotes (.pcap/.pcapng) com aceleração SIMD e mapeamento no kernel. | **Motor Gráfico 60 FPS GPU Direct Canvas/WebGL (`pcap-cyberpunk-map.js`)** com luzes pulsantes esmaecendo e brilhando (*Breathing Neon Particles*), **Zoom/Pan com bloqueio nativo de rolagem da janela (`{passive: false}`)** e resiliência a abas; **Heurística de Telecom, NOC e SOC** para 9 protocolos core (`BGP`, `OSPF`, `IS-IS`, `MPLS/VPLS`, `PPPoE`, `DHCP`, `IPv6 RA Guard`), inspeção interativa de quadros com Hex Dump e ASCII, botão de upload personalizado e popup de aviso forense. |
| **💻 Terminal SSH Studio (`v2.2.0`)** | Client SSH multi-aba de alta performance com `xterm.js`. | **Correção do Bug de Travamento Cisco Exit Lock (desconexão instantânea e liberação limpa de PTY/ShellStream)**, **Fluidez Extrema a 60 FPS** via debouncing buffer C# (16ms) e bypass streaming JS para comandos >12KB, **Sincronização Dinâmica SIGWINCH** (`htop`/`btop`), **Syntax Highlighting** e **Copiar Tudo Buffer**. |
| **🏓 Ping & Trace Suite (`v2.2.3`)** | Motores avançados de ICMP, Ping Contínuo, Cadeia Multi-Ping e MTR. | **Responsividade no MTR Avançado (`v2.2.3`)**: Painel superior multi-linha com auto-escalonamento (`min-width: 240px`); **Motor Inteligente Anti-CoPP Rate-Limit 3 Fases (Heurística de Salto Intermediário vs Destino + Poisson Jittering + TCP SYN Bypass)** com selo azul neon **`⚡ CoPP BYPASS`**, **Cadeia Multi-Ping** com laudo formatado, **Seletor de Pilha IP (IPv4/IPv6/Auto)** e **Cálculo de Jitter RFC 3393** isolado no MTR. |
| **📡 IP Scan & Port Scanner SIMD (`v2.1.1`)** | Varredura minuciosa de sub-redes locais e auditoria forense de portas (`Port Scanner SIMD Pro v2.2`). | **Aceleração SIMD Multi-Core Paralela** (até 1.500 threads com *throttling* adaptativo de rede), **Eliminação de Falsos Positivos UDP via Sondas Ativas de Payload** (DNS, NTP, SNMP, SIP + detecção de ICMP Port Unreachable), **Deep Banner Grabbing & Inspeção TLS Forense** com captura de certificado X.509, **Triage de Risco SOC (`Crítico/Alto/Normal`)** com notas de mitigação e **Hex Dump Preview Raw**, além de exportação de laudos CSV em tempo real via **`rezTermFileSave`**. |
| **⚡ Live TCP/UDP Watcher** | Monitoramento de sockets abertos e conexões ativas no Windows. | Integração nativa com **GeoLite2 MMDB em Memória (MMF)** projetando conexões em **Mapa Mundi interativo**. |
| **🌐 NetOps & Whois/IRR** | Consulta unificada a bases mundiais de registro de IPs e ASNs. | Conectores diretos para RADB, RIPE, LACNIC, ARIN, APNIC e AFRINIC com formatação de blocos BGP. |
| **🔌 Ethernet Tests L2** | Verdadeiro "Fluke de Software" operando na Camada de Enlace (L2). | Escuta passiva LLDP/CDP/MNDP, injeção ativa de **PADI Broadcast (PPPoE Rogue)** e **DHCP Discover**. |
| **🕵️ Rastreio Forense CGNAT** | Investigação forense em servidores Graylog com geração de relatórios. | **Aceleração Vetorial SIMD AVX2/AVX-512 Paralela** (até 250x mais rápido), **Modo Híbrido Bimodal**, cálculo de blocos **Cisco BPA (RFC 6598)** e exportação em PDF/TXT com cláusulas jurídicas e hash SHA-256. |

---

## 🚀 4. Destaques da Evolução Arquitetural (`v2.2.6`)

### 🔗 Release v2.2.6 (Inteligência RF MESH / Repetidores & Zero Falsos Positivos)
* **Reconhecimento Arquitetural MESH / Multi-AP (`ConnectedMeshOrSiblingNodes`)**: Em redes Wi-Fi em malha (ex: **TP-Link Deco**, **Google Wifi**, **MikroTik Mesh**) e repetidores sem cabo de rede, os satélites compartilham o mesmo SSID, Canal e Frequência para realizar o *Wireless Backhaul*. O motor identifica automaticamente as antenas cooperativas, separando ruído de terceiros do comportamento correto do roteador.
* **Score de Saúde de Canal (`AnalyzeSpectrumAndChannels`)**: Penalização focada em **ESSIDs concorrentes reais (`distinctSsids.Count`)**, exibindo o status: `🟢 Topologia MESH / Multi-AP (Compartilhamento Legítimo de Canal)`.
* **Modal Interativo Enxuto (`🚨 ABRIR LAUDO DE MELHORIAS (@conn.Ssid)`)**: Ação direta com tabela dedicada de **Topologia MESH cooperativa**, listando nó principal (`⭐`) e satélites (`🔗`).

### ⚡ Releases v2.2.5 & v2.2.3 (Triagem RF, Auto-Escala & Processo `RezTerm.exe`)
* **Card Dedicado de Triagem da Conexão Ativa (`⚡ REDE CONECTADA EM AUDITORIA`)**: Consolidado no topo da aba de espectro passivo com contagem exata de interferência **Co-Canal (`CCI`)** e **Adjacente (`ACI`)**.
* **Auditoria IEEE Priorizada (`⭐ REDE CONECTADA`)**: Laudos de conformidade e recomendações da rede conectada gerados em primeiro lugar no topo da lista.
* **Processo Nativo `RezTerm.exe`**: Compilação alinhada em todo o pipeline e assistente de instalação, aparecendo exatamente como **`RezTerm.exe`** no Gerenciador de Tarefas e observabilidade SOC/NOC.

### 🔌 Release v2.2.0 & v2.2.2 (Correção SSH Cisco & Motor Anti-CoPP 3 Fases)
* **Correção do Bug de Travamento SSH (`Cisco Exit Thread Lock`)**: Liberação instantânea de PTY/ShellStream ao executar `exit` em equipamentos Cisco/Juniper.
* **Inteligência Anti-Rate-Limit / Anti-CoPP em 3 Fases**: Conforme **RFC 1812** (Sec 4.3.2.8) e **RFC 4443** (Sec 2.4), roteadores core de telecom limitam disparos ICMP periódicos (`Control Plane Policing - CoPP`). O RezTerm contorna esses alarmes falsos combinando Heurística de Salto Intermediário vs Destino (`⚡ CoPP RATE-LIMIT`), **Poisson Random Jittering & Exponential Backoff Pacing**, e **TCP SYN Bypass em portas 80/443** (`⚡ CoPP BYPASS (TCP)` @ `Loss = 0%`).

---

## 🛡️ 5. Arquitetura de Segurança & Blindagem

1. **Compilação Blindada (*Single-File ReadyToRun Native*)**:
   - Os executáveis são compilados em código de máquina nativo (`win-x64`) com desativação total de símbolos de debug (`DebugSymbols=false`), impedindo ataques de engenharia reversa via ILSpy/dnSpy.
2. **Cofre Criptográfico DPAPI + HMAC-SHA256 (`HostStorageService`)**:
   - Nenhuma senha, chave privada SSH, token de API Graylog ou chave de licença é gravada em texto plano no disco.
   - O sistema utiliza a **DPAPI (Data Protection API) do Windows** acoplada ao perfil do usuário (`DataProtectionScope.CurrentUser`) e reforçada com verificação de integridade **HMAC-SHA256**.
3. **Observabilidade com Mascaramento de Dados**:
   - Logs estruturados em JSON Lines (`.jsonl`) rotativos, que executam mascaramento automático de credenciais (*Data Masking*), substituindo senhas e tokens por `"***MASKED***"`.

---
<div align="center">
<b>Sepulnation Telecom • Diretoria de Engenharia & Segurança Cibernética</b><br>
<i>Reginaldo Junior (Razon) • Todos os Direitos Reservados</i>
</div>
