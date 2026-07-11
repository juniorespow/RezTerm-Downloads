# ⚡ RezTerm v2.2.5 (Cyberpunk SOC/NOC & Forensics PCAP Suite - Telecom Edition)

<div align="center">

![.NET Core](https://img.shields.io/badge/.NET%2010.0-512BD4?style=for-the-badge&logo=dotnet&logoColor=white)
![Blazor Hybrid](https://img.shields.io/badge/Blazor%20Hybrid-5C2D91?style=for-the-badge&logo=blazor&logoColor=white)
![WPF](https://img.shields.io/badge/Windows%20WPF-0078D4?style=for-the-badge&logo=windows&logoColor=white)
![C#](https://img.shields.io/badge/C%23%2013-239120?style=for-the-badge&logo=c-sharp&logoColor=white)
![Security](https://img.shields.io/badge/Security-DPAPI%20%2B%20HMAC-00f0ff?style=for-the-badge)
![Hardware Acceleration](https://img.shields.io/badge/HW%20Acceleration-GPU%20%2B%20SIMD-00ff88?style=for-the-badge)
![RF Intelligence](https://img.shields.io/badge/RF%20Fluke%20Engine-CCI%2FACI%20Triage-00f0ff?style=for-the-badge)

**A Suíte Definitiva de Engenharia de Redes, Diagnóstico SOC/NOC, Auditoria Forense e Terminal SSH Multi-Aba.**  
Desenvolvida por **Reginaldo Junior (Razon)** combinando a performance nativa do Windows (.NET 10 WPF / ReadyToRun Native) com uma interface ultramoderna Blazor Hybrid em estética **Cyberpunk Dark Neon**, **Inteligência de Engenharia RF no Wireless Tests (`v2.2.5`)**, **Responsividade Universal Auto-Ajustável (`v2.2.5`)**, **Processo Nativo `RezTerm.exe` no Windows Task Manager (`v2.2.3`)**, **Telemetria Nativa de RAM/GPU (`v2.2.2`)** e motor de **Aceleração de Hardware Híbrida (GPU + SIMD)** com **Inteligência Anti-CoPP 3 Fases**.

---

### 🚨 AVISO DE LICENCIAMENTO E PROPRIEDADE INTELECTUAL
**O RezTerm é um software proprietário corporativo da Diretoria Telecom.**  
O acesso é estritamente restrito e exige autenticação de licença vinculada ao hardware deste computador (HWID). O download ou tentativa de uso não autorizado sem chave criptográfica válida é monitorado e bloqueado pela arquitetura de segurança do sistema.

</div>

---

## 📥 1. Como Baixar e Instalar (Release v2.2.5)

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

## 🛠️ 3. Suíte de Ferramentas Integradas (v2.2.0)

| Módulo | Descrição Principal | Destaques de Engenharia |
| :--- | :--- | :--- |
| **📊 Dashboard & Latência (`v2.2.0`)** | Monitoramento em tempo real da saúde da conexão e dual-stack ISP. | **Responsividade Universal Auto-Ajustável (Flexbox)** sem rolagem externa dupla, **Motor Híbrido Anti-CoPP Rate-Limit (TCP SYN Bypass em portas 80/443)** para evitar alarmes falsos de queda, **Poisson Random Jittering & Exponential Backoff Pacing**, Gateway Dual e Badge de Aceleração GPU/SIMD. |
| **📡 Leitor PCAP Forense (`v2.1.0`)** | Analisador e dissecador forense de pacotes (.pcap/.pcapng) com aceleração SIMD e mapeamento no kernel. | **Motor Gráfico 60 FPS GPU Direct Canvas/WebGL (`pcap-cyberpunk-map.js`)** com luzes pulsantes esmaecendo e brilhando (*Breathing Neon Particles*), **Zoom/Pan com bloqueio nativo de rolagem da janela (`{passive: false}`)** e resiliência a abas; **Heurística de Telecom, NOC e SOC** para 9 protocolos core (`BGP`, `OSPF`, `IS-IS`, `MPLS/VPLS`, `PPPoE`, `DHCP`, `IPv6 RA Guard`), inspeção interativa de quadros com Hex Dump e ASCII, botão de upload personalizado e popup de aviso forense. |
| **💻 Terminal SSH Studio (`v2.2.0`)** | Client SSH multi-aba de alta performance com `xterm.js`. | **Correção do Bug de Travamento Cisco Exit Lock (desconexão instantânea e liberação limpa de PTY/ShellStream)**, **Fluidez Extrema a 60 FPS** via debouncing buffer C# (16ms) e bypass streaming JS para comandos >12KB, **Sincronização Dinâmica SIGWINCH** (`htop`/`btop`), **Syntax Highlighting** e **Copiar Tudo Buffer**. |
| **🏓 Ping & Trace Suite (`v2.2.0`)** | Motores avançados de ICMP, Ping Contínuo, Cadeia Multi-Ping e MTR. | **Motor Inteligente Anti-CoPP Rate-Limit 3 Fases (Heurística de Salto Intermediário vs Destino + Poisson Jittering + TCP SYN Bypass)** com selo azul neon **`⚡ CoPP BYPASS`**, **Cadeia Multi-Ping** com laudo formatado, **Seletor de Pilha IP (IPv4/IPv6/Auto)** e **Cálculo de Jitter RFC 3393** isolado no MTR. |
| **📡 IP Scan & Port Scanner SIMD (`v2.1.1`)** | Varredura minuciosa de sub-redes locais e auditoria forense de portas (`Port Scanner SIMD Pro v2.2`). | **Aceleração SIMD Multi-Core Paralela** (até 1.500 threads com *throttling* adaptativo de rede), **Eliminação de Falsos Positivos UDP via Sondas Ativas de Payload** (DNS, NTP, SNMP, SIP + detecção de ICMP Port Unreachable), **Deep Banner Grabbing & Inspeção TLS Forense** com captura de certificado X.509, **Triage de Risco SOC (`Crítico/Alto/Normal`)** com notas de mitigação e **Hex Dump Preview Raw**, além de exportação de laudos CSV em tempo real via **`rezTermFileSave`**. |
| **⚡ Live TCP/UDP Watcher** | Monitoramento de sockets abertos e conexões ativas no Windows. | Integração nativa com **GeoLite2 MMDB em Memória (MMF)** projetando conexões em **Mapa Mundi interativo**. |
| **🌐 NetOps & Whois/IRR** | Consulta unificada a bases mundiais de registro de IPs e ASNs. | Conectores diretos para RADB, RIPE, LACNIC, ARIN, APNIC e AFRINIC com formatação de blocos BGP. |
| **🔌 Ethernet Tests L2** | Verdadeiro "Fluke de Software" operando na Camada de Enlace (L2). | Escuta passiva LLDP/CDP/MNDP, injeção ativa de **PADI Broadcast (PPPoE Rogue)** e **DHCP Discover**. |
| **📶 Wireless Tests RF** | Analisador de espectro Wi-Fi e qualidade de sinal em tempo real. | **Barras de progresso ao vivo**, **Telemetria Ativa Gateway RF de partida instantânea**, pílulas neon de redes sobrepostas e auditoria IEEE 802.11. |
| **🕵️ Rastreio Forense CGNAT** | Investigação forense em servidores Graylog com geração de relatórios. | **Aceleração Vetorial SIMD AVX2/AVX-512 Paralela** (até 250x mais rápido), **Modo Híbrido Bimodal**, cálculo de blocos **Cisco BPA (RFC 6598)** e exportação em PDF/TXT com cláusulas jurídicas e hash SHA-256. |

---

## 🚀 4. Destaques da Release v2.2.0 (Responsividade Universal, Correção SSH Cisco & Motor Anti-CoPP 3 Fases)

* **Responsividade Universal Auto-Ajustável (`Flexbox & Overflow-Y Engine`)**:
  Padronização total de todos os containers principais e cards do sistema em regime flexível. Ajuste automático para telas de 14" e resoluções menores sem vazamento ou rolagens globais duplas.
* **Correção do Bug de Travamento SSH (`Cisco Exit Thread Lock`)**:
  Solucionado o congelamento de abas ao desconectar via comando `exit` em equipamentos Cisco/Juniper. Liberação limpa de PTY e *ShellStream* sem bloquear a thread principal da UI.
* **Inteligência Anti-Rate-Limit / Anti-CoPP em 3 Fases (`Control vs. Data Plane Verification`)**:
  Por que gigantes globais como **Google (AS15169 / 8.8.8.8)**, **Cloudflare (AS13335 / 1.1.1.1)**, **Amazon AWS** e roteadores core **Cisco**, **Juniper** e **Nokia** limitam o Ping tradicional? A **RFC 1812 (Seção 4.3.2.8)** e **RFC 4443 (Seção 2.4)** instruem que roteadores limitem requisições ICMP para proteger a CPU do Plano de Controle (*Control Plane*) contra ataques DDoS (*Control Plane Policing - CoPP*). O cálculo do Jitter e variação de atraso segue a **RFC 3393**. Ferramentas primitivas interpretam esse descarte no kernel como falha de link, quando na verdade o tráfego na via de dados (*Data Plane / ASIC Hardware Forwarding*) opera a 100 Gbps com 0% de perda! O RezTerm elimina esses alarmes falsos:
  1. **Fase 1 (Heurística CoPP de Salto Intermediário vs. Destino)**: Compara o rastreio MTR. Se um roteador intermediário descarta pacotes mas o destino final tem 0% de perda, a falha é classificada como limitação CoPP e ganha o selo **`⚡ CoPP RATE-LIMIT`**.
  2. **Fase 2 (Poisson Random Jittering & Exponential Backoff Pacing Engine)**: Substitui disparos periódicos repetitivos por variação estocástica baseada em **distribuição de Poisson (`±15% jitter`)**. Em caso de contenção, aplica recuo exponencial (**Backoff `x1.4`**), permitindo a regeneração dos *token buckets* do roteador sem alarmes falsos.
  3. **Fase 3 (Sondagem Híbrida Multi-Protocolo & TCP SYN Bypass)**: Quando o ICMP Echo é descartado por limitação de *Control Plane*, o motor aciona instantaneamente uma sondagem na via de dados via handshake **TCP SYN/ACK (portas 80 ou 443)**. Se responder (`SYN/ACK @ 12 ms`), o sistema atesta 100% de conectividade, exibe **`⚡ CoPP BYPASS (TCP)`** em Azul Neon (`#00f0ff`) com tooltip explicativo, mantendo `Loss = 0%`.

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
