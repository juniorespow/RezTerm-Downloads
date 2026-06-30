# ⚡ RezTerm (SepulnationTerm) • Central Oficial de Downloads & Atualizações

<div align="center">

![.NET Core](https://img.shields.io/badge/.NET%2010.0%20Windows-512BD4?style=for-the-badge&logo=dotnet&logoColor=white)
![Security Verified](https://img.shields.io/badge/Security-AES--256--GCM%20DPAPI-0078D4?style=for-the-badge&logo=windows&logoColor=white)
![Architecture](https://img.shields.io/badge/Architecture-Windows%20x64-239120?style=for-the-badge)
![Distribution](https://img.shields.io/badge/Channel-Official%20Releases-blue?style=for-the-badge&logo=github)

**A suíte definitiva de Engenharia de Redes, Operações SOC e Terminal SSH.**  
Canal público de distribuição comercial e atualizações automáticas (*Zero-Code Repository*).

</div>

---

## 🌟 Sobre este Canal de Distribuição (Segurança Cibernética)

Este repositório atua estritamente como o **Ponto de Distribuição Oficial e CDN Mundial** para o software **RezTerm** (codinome de engenharia *SepulnationTerm*), desenvolvido por **Reginaldo Junior (Razon)**.

Em alinhamento às nossas diretrizes de **Segurança Militar e Proteção de Propriedade Intelectual (IP)**:
1. **Código-Fonte Confidencial**: Todo o código C#, algoritmos de detecção de gargalos de rede, motores assíncronos de MTR e lógicas do *Cofre MobaVault* residem em um repositório 100% privado e isolado.
2. **Blindagem Anti-Decompilação**: Os binários distribuídos aqui são compilados via `.NET 10 Single-File Publish`, com otimizações nativas de montagem assembly (*Trim / ReadyToRun*) e ofuscação estrutural.
3. **Zero Tokens Internos**: O aplicativo cliente consulta as Releases públicas deste canal de forma transparente via requisições HTTP anônimas, garantindo que nenhum token de acesso ou segredo corporativo trafegue ou fique armazenado nos executáveis instalados nos computadores dos técnicos.

---

## 🚀 Guia Rápido de Instalação

### 1. Download do Assistente Blindado
Acesse a barra lateral direita na seção [**Releases**](https://github.com/juniorespow/RezTerm-Downloads/releases) e baixe o arquivo oficial:
* 📦 **`RezTermSetup.exe`** (Validador e Bootstrapper Nativo)

### 2. Validação Diagnóstica Inteligente & Escolha de Pasta
Ao executar o `RezTermSetup.exe`, o assistente realiza inspeções instantâneas no seu sistema operacional e permite personalização completa:
* 📁 **Seletor de Pasta Personalizada**: Opção nativa para o usuário escolher exatamente onde o sistema será instalado (padrão em `%LocalAppData%\RezTerm`).
* 📌 **Atalhos Inteligentes**: Criação de ícones de acesso tanto na **Área de Trabalho** quanto no **Menu Iniciar** do Windows.
* 🗑️ **Desinstalador Completo**: Opção integrada de desinstalação total para limpeza profunda de binários, cache e atalhos sem deixar resíduos no sistema.
* ✔️ **Arquitetura x64 & Espaço**: Checagem de compatibilidade com instruções 64 bits e alocação segura em disco.
* ✔️ **Runtime de UI Isolado**: Checagem de disponibilidade do motor *Microsoft Edge WebView2* com criação automática de cache isolado anti-travamento.
* ✔️ **Instalação Anti-Travamento (Auto-Kill & Safe Extract)**: Detecção e encerramento automático de instâncias abertas em memória do RezTerm/WebView2 e liberação de atributos read-only/locks antes de atualizar, eliminando por completo o erro `Access to the path is denied`.
* ✔️ **Pacote Completo (Web Assets)**: Extração integral dos arquivos `.exe` e da pasta web `wwwroot`, eliminando telas pretas e erros de navegação.

### 3. Conclusão Silenciosa & Atalho Nativo
O software instala seus binários isolados, cria atalhos nativos `.lnk` com o diretório de trabalho (*WorkingDirectory*) travado na pasta raiz e inicializa instantaneamente sem exigir privilégios administrativos (*Elevation / UAC*).

---

## 🛡️ Destaques da Plataforma RezTerm

* **⚡ Ethernet Tests (Analisador L2 / Fluke de Software)**: Diagnóstico profundo de portas Ethernet (Camada 2) em switches Datacom, Cisco e MikroTik via SharpPcap/WinPcap! Escuta passiva de vizinhança (**LLDP, CDP, MNDP**), verificação de segurança anti-loop (**STP/RSTP/MSTP BPDUs**), detecção de vazamento de VLANs (**802.1Q / QinQ Trunk Leakage**) e medidor em tempo real de tempestades de broadcast (**Broadcast Storm pps**). Inclui injeção ativa de pacotes para varredura de concentradores **PPPoE Server / Rogue BRAS** (RFC 2516), radar de servidores **Rogue DHCP** (RFC 2131) e varredura progressiva de gargalo **MTU L2 (bit Do Not Fragment - DF)**!
* **⚡ Live TCP/UDP Watcher (DPI Leve & GeoIP)**: Monitor de tráfego de rede em tempo real com motor orientado a eventos sem travamento de interface! Detecta conexões **TCP/UDP**, identifica protocolos modernos como **HTTP/3 QUIC** e rastrea diagnósticos **ICMP** (Ping/Traceroute) com resolução geográfica offline instantânea (Bandeira do País, Cidade e Provedor/ASN) via bases *MaxMind GeoLite2 MemoryMappedFile*.
* **🗺️ MTR Traceroute Avançado**: O motor mais preciso do mercado, com cálculo dinâmico por salto de *Jitter*, Desvio Padrão e gráficos animadíssimos em tempo real.
* **🔐 Cofre SSH MobaVault**: Armazenamento criptografado via **AES-256-GCM** amarrado à sessão do usuário (*Windows DPAPI Anti-Memory Scraper*), com derivação **PBKDF2 SHA-256** para exportação e auto-login inteligente na Conexão Rápida.
* **🌌 Design 100% Dark Cyberpunk (Neon Blue)**: Ditadura visual do modo escuro absoluto vibrando em Ciano Ciber (`#00f0ff`) com barra lateral retrátil fluida e monitor ISP Dual Stack (IPv4/IPv6).
* **🧮 NetOps & IRR Whois Enterprise**: Motor de busca avançada para ASN, IP e Prefixos CIDR com extração automática de Razão Social completa do titular (`fn` vCard) e execução assíncrona concorrente à prova de timeouts.
* **📡 Advanced IP & Service Scanner 2.0**: Varredura multi-protocolo assíncrona com sondagem TCP paralela de portas (HTTP, HTTPS, SSH, RDP, SMB), raspagem automática de títulos HTML/Banners de equipamentos (ex: *Ubiquiti airOS*, *MikroTik RouterOS*, *HP LaserJet*), decodificação IEEE de fabricante MAC e botões de atalho de 1 clique direto para o navegador e terminal!

---

<div align="center">
  <b>RezTerm • Engenharia de Software e Redes por Reginaldo Junior (Razon)</b>
</div>
