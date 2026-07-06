# ⚡ RezTerm v2.0.6 (Cyberpunk SOC/NOC Suite - Telecom Edition)

<div align="center">

![.NET Core](https://img.shields.io/badge/.NET%2010.0-512BD4?style=for-the-badge&logo=dotnet&logoColor=white)
![Blazor Hybrid](https://img.shields.io/badge/Blazor%20Hybrid-5C2D91?style=for-the-badge&logo=blazor&logoColor=white)
![WPF](https://img.shields.io/badge/Windows%20WPF-0078D4?style=for-the-badge&logo=windows&logoColor=white)
![C#](https://img.shields.io/badge/C%23%2013-239120?style=for-the-badge&logo=c-sharp&logoColor=white)
![Security](https://img.shields.io/badge/Security-DPAPI%20%2B%20HMAC-00f0ff?style=for-the-badge)

**A Suíte Definitiva de Engenharia de Redes, Diagnóstico SOC/NOC, Auditoria Forense e Terminal SSH Multi-Aba.**  
Desenvolvida por **Reginaldo Junior (Razon)** combinando a performance nativa do Windows (.NET 10 WPF / ReadyToRun Native) com uma interface ultramoderna Blazor Hybrid em estética **Cyberpunk Dark Neon**.

---

### 🚨 AVISO DE LICENCIAMENTO E PROPRIEDADE INTELECTUAL
**O RezTerm é um software proprietário corporativo da Diretoria Telecom.**  
O acesso é estritamente restrito e exige autenticação de licença vinculada ao hardware deste computador (HWID). O download ou tentativa de uso não autorizado sem chave criptográfica válida é monitorado e bloqueado pela arquitetura de segurança do sistema.

</div>

---

## 📥 1. Como Baixar e Instalar (Release v2.0.6)

A distribuição do **RezTerm** é realizada via assistente de instalação blindado que configura o ambiente no perfil do técnico sem exigir privilégios de administrador global (`%LocalAppData%\RezTerm`):

1. **Baixe o Instalador Oficial**: Acesse a aba [Releases](https://github.com/juniorespow/RezTerm-Downloads/releases/latest) deste repositório e faça o download do arquivo **`RezTermSetup.exe`**.
2. **Execute o Assistente**: Abra o `RezTermSetup.exe`. Ele baixará automaticamente o payload blindado e criará os atalhos na Área de Trabalho e Menu Iniciar com o novo ícone Cyberpunk Neon.
3. **Atualização Automática via CDN**: O software possui verificação contínua de novas versões em segundo plano. Sempre que a Diretoria Telecom lançar um patch de segurança ou nova ferramenta, você será notificado no topo do sistema para atualizar em 1 clique.

---

## 🔑 2. Como Ativar sua Licença Corporativa (HWID)

Na primeira execução do **RezTerm v2.0.6**, o sistema iniciará em **Tela Cheia Maximizada** apresentando a tela modal de bloqueio de segurança:

1. **Copie seu Código Único (HWID)**: Clique no botão **`[ Copiar meu HWID e Solicitar Licença ]`**. O sistema gerará um hash de 12 caracteres único da sua placa-mãe e processador (ex: `REZ-8F9A-2B1C-4D5E`).
2. **Envie para a Diretoria Telecom**: Abra chamado ou envie uma mensagem direta ao gestor responsável informando seu Nome, Setor e o código HWID copiado.
3. **Ative o Sistema**: A Diretoria emitirá uma chave criptográfica **HMAC-SHA256** (ex: `REZ-PRO-20270706-XXXX-XXXX-XXXX-SIG16`). Cole essa string no campo da tela de bloqueio e clique em **Ativar e Desbloquear Sistema**.
4. **Verificação de Validade**: Após desbloqueado, o status de sua licença ficará sempre visível no topo do Dashboard através do selo verde `🔒 Licenciado (...)`. Ao clicar no selo, você poderá consultar todos os detalhes da sua concessão corporativa.

---

## 🛠️ 3. Suíte de Ferramentas Integradas (v2.0.6)

| Módulo | Descrição Principal | Destaques de Engenharia |
| :--- | :--- | :--- |
| **📊 Dashboard & Latência** | Monitoramento em tempo real da saúde da conexão e dual-stack ISP. | Gráficos de latência ao vivo, detecção de perda de pacotes e **Gateway Dual (exibição simultânea de saídas IPv4 e IPv6 Neon)**. |
| **💻 Terminal SSH Studio** | Client SSH multi-aba de alta performance com `xterm.js`. | **Sincronização Dinâmica SIGWINCH** (gradação de colunas/linhas em tempo real perfeita para `htop`/`btop`), **Syntax Highlighting** (Cisco & Datacom com `deny` em vermelho crítico), **Copiar Tudo (Buffer SSH)** preservando identação estilo MobaXterm e **12 Fabricantes suportados** com grupos colapsáveis `[+/-]`. |
| **🏓 Ping & Trace Suite** | Motores avançados de ICMP, Ping Contínuo, Cadeia Multi-Ping e MTR. | **Cadeia Multi-Ping** com laudo formatado, **Seletor de Pilha IP (IPv4/IPv6/Auto)** e **Cálculo de Jitter de Destino** isolado no MTR. |
| **📡 IP Scan & APIPA** | Varredura minuciosa de sub-redes locais com ARP/Ping/TCP Sweep. | **Resgate APIPA (RFC 3927)** para resgate de switches e roteadores sem servidor DHCP ativo. |
| **⚡ Live TCP/UDP Watcher** | Monitoramento de sockets abertos e conexões ativas no Windows. | Integração nativa com **GeoLite2 MMDB em Memória (MMF)** projetando conexões em **Mapa Mundi interativo**. |
| **🌐 NetOps & Whois/IRR** | Consulta unificada a bases mundiais de registro de IPs e ASNs. | Conectores diretos para RADB, RIPE, LACNIC, ARIN, APNIC e AFRINIC com formatação de blocos BGP. |
| **🔌 Ethernet Tests L2** | Verdadeiro "Fluke de Software" operando na Camada de Enlace (L2). | Escuta passiva LLDP/CDP/MNDP, injeção ativa de **PADI Broadcast (PPPoE Rogue)** e **DHCP Discover**. |
| **📶 Wireless Tests RF** | Analisador de espectro Wi-Fi e qualidade de sinal em tempo real. | **Barras de progresso ao vivo**, **Telemetria Ativa Gateway RF de partida instantânea**, pílulas neon de redes sobrepostas e auditoria IEEE 802.11. |
| **🕵️ Rastreio Forense CGNAT** | Investigação forense em servidores Graylog com geração de relatórios. | **Modo Híbrido Bimodal (Assistente HelpDesk N1/N2 + Modo Engenharia Avançado)**, cálculo de blocos **Cisco BPA (RFC 6598)** em memória C#, e exportação nativa em PDF e TXT com cláusulas jurídicas obrigatórias (Marco Civil da Internet e LGPD). |

---

## 🛡️ 4. Arquitetura de Segurança & Blindagem

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
