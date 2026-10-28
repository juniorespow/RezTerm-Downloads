# RezTerm v3.4.5 (Cyberpunk Network Engineer Toolkit & Forensics Suite)

<div align="center">

![.NET Core](https://img.shields.io/badge/.NET%2010.0-512BD4?style=for-the-badge&logo=dotnet&logoColor=white)
![Blazor Hybrid](https://img.shields.io/badge/Blazor%20Hybrid-5C2D91?style=for-the-badge&logo=blazor&logoColor=white)
![WPF](https://img.shields.io/badge/Windows%20WPF-0078D4?style=for-the-badge&logo=windows&logoColor=white)
![C#](https://img.shields.io/badge/C%23%2013-239120?style=for-the-badge&logo=c-sharp&logoColor=white)
![Security](https://img.shields.io/badge/Security-DPAPI%20%2B%20HMAC-00f0ff?style=for-the-badge)
![Hardware Acceleration](https://img.shields.io/badge/HW%20Acceleration-GPU%20%2B%20SIMD-00ff88?style=for-the-badge)

Plataforma Unificada de Diagnóstico de Redes, Auditoria Forense NOC/SOC, Triagem L2/L7 e Análise de Tráfego de Alta Performance — Compilada em **.NET 10.0 ReadyToRun WPF / Blazor Hybrid** com **Resiliência Multi-Endpoint & IPv4-First RezServer (`v3.4.5`)**, **Gestão & Ativação Online de Licenças Corporativas via RezServer (`v3.4.4`)**, **Medidor L4 RFC 6349 com Servidor Dedicado (`v3.4.4`)**, **Módulo ICMP Discovery & Path Audit (`v3.4.3`)**, **Live TCP/UDP Watcher Local-First (`v3.4.2`)** e **Suíte de Temas Duplo (Dark Neon & Windows 11 Dark Fluent)**.

</div>

---

## 1. Visão Geral Corporativa & Engenharia

O **RezTerm** é uma suíte integrada de engenharia de redes projetada para atender aos requisitos operacionais do Centro de Gerenciamento de Redes (CGR), Network Operations Center (NOC) e Security Operations Center (SOC). O sistema foi concebido para substituir a fragmentação de ferramentas legadas de mercado (como Wireshark, PuTTY, MTR, SolarWinds, PRTG, Nmap e utilitários auxiliares) por um ambiente unificado de altíssima performance executado diretamente no metal do Windows OS.

A arquitetura combina a capacidade de baixo nível do .NET 10 (acesso a sockets brutos, P/Invoke Win32, contadores de desempenho de kernel e chamadas de API do sistema operacional) com a flexibilidade gráfica do Blazor Hybrid renderizado via WebView2 com aceleração por hardware (GPU DirectComposition).

---

## 2. Novidades & Otimizações — Versão v3.4.5 (Outubro / 2026)

* **Resiliência Multi-Endpoint e Resolução Dual-Stack IPv4/IPv6 no RezServer & RFC 6349 (`v3.4.5`)**:
  - Implementação de ordenação estrita IPv4-First (Happy Eyeballs Invertido) no `RezHttpClientFactory` via `SocketsHttpHandler.ConnectCallback`, prevenindo blackholes e timeouts de 21 segundos de retransmissão SYN em clientes com conexões dual-stack e IPv6 inoperante na borda.
  - Cascata multi-endpoint de alta disponibilidade com fallback transparente em `Rfc6349Service` e `LicensingService` (`https://rezserver.audicomtelecom.com.br`, `https://45.237.201.24`, `http://rezserver...`, `http://45.237.201.24`), com persistência em memória do último endpoint ativo.
  - Elevação do timeout HTTP de 5s para 12s para garantir handshakes TLS e conexões em redes móveis de alta latência.
  - Correção na interface `RezServerConfigSection` sincronizando a porta padrão `443` e flags `UseHttps`.
  - Isenção de redirecionamentos canônicos 301 para endpoints REST `/api/` no daemon Debian `rezserverd.py` e emissão padronizada de cabeçalhos `Content-Length`, `Content-Type: application/json; charset=utf-8` e `Connection: close`, sanando encerramentos abruptos Schannel 56 no Windows.
* **Gestão & Ativação Online de Licenças Corporativas via RezServer (`v3.4.4`)**: Implementação do ciclo automatizado de solicitação e homologação remota de licenças corporativas. O cliente recém-instalado submete diretamente sua requisição informando nome, cargo e empresa. O RezServer armazena o pedido em banco SQLite (`license_requests`) e provê endpoint administrativo com interface Web no CGR para aprovação em 1 clique com vigência configurável (30 a 730 dias) e assinatura HMAC-SHA256 automática. O RezTerm executa polling periódico (3.5s) com animação neon e ativa/persiste a licença de forma transparente no endpoint local.
* **Medidor de Vazão L4 RFC 6349 & Ecossistema RezServer (`v3.4.4`)**: Implementação de teste de vazão de camada de transporte L4 cliente/servidor com auditoria rigorosa de **Throughput Efetivo**, **Baseline RTT**, **Saturated RTT**, **Buffer Delay percentual**, **Transfer Time Ratio (TTR)** e **Eficiência TCP percentual** conforme a norma RFC 6349. Handshake criptográfico Zero-Cleartext com assinatura HMAC-SHA256, Nonces Anti-Replay e emissão de Tickets Efêmeros descartáveis (OTT). Infraestrutura soberana com servidor Linux Debian 12 dedicado em IPv4 público (`45.237.201.24`) e IPv6 estático (`2804:4ee4:ff00:3::11`), SSL ECDSA Let's Encrypt com renovação automática, roteamento canônico 301 para `rezserver.audicomtelecom.com.br`, ofuscação `Server: RezSecure` e geração pericial de laudo em PDF.
* **Resiliência e Prevenção de Falhas de Interface (`v3.4.4`)**: Prevenção de bloqueios e travamentos no WebView2 por meio de `FileDialogHelper` assíncrono em thread STA dedicada para salvamento de laudos periciais, refinamento dos rótulos de latência e suporte dinâmico ao tema Windows 11 Dark Fluent.
* **ICMP Network Discovery & Path Audit (`v3.4.3`)**: Submódulo avançado para varredura massiva paralela em sub-redes IPv4 baseada em `System.Threading.Channels` (suporte a até 256 threads simultâneas sem contenção de memória). Executa auditoria automática de **Path MTU (PMTU)** via varredura com bit DF (*DontFragment*) ativado em amostragem binária (1500 B a 1280 B), calcula o **MSS Estimado** ($\text{MTU} - 40$), estima a distância de saltos (**Hop Count**) via TTL de resposta ($64 - \text{TTL}$, $128 - \text{TTL}$, $255 - \text{TTL}$), realiza validação rigorosa de sintaxe CIDR (`IsValidIpv4Cidr`) com alerta informativo de formatação e permite exportação em 1-clique para laudos Markdown e relatórios CSV.
* **Live TCP/UDP Watcher 100% Local-First (`v3.4.2`)**: Sistema de monitoramento de sockets abertos do Windows OS com resolução geográfica 100% offline via MaxMind GeoLite2 MMDB em memória mapeada (`MemoryMappedFile`), eliminando tráfego de fundo. Classifica automaticamente redes reservadas e privadas conforme as RFCs aplicáveis (RFC 1918, RFC 6598, RFC 3927, RFC 2544, RFC 5737, RFC 4291 e RFC 4193). Medição real de vazão por processo via P/Invoke nativo Kernel Win32 (`GetProcessIoCounters`).
* **Resolução de Nomes & RFCs no NetOps & IRR (`v3.4.2`)**: Otimização no conector de consultas BGP para utilizar o primeiro IP utilizável do bloco (`.1`) em vez do IP de rede (`.0`), garantindo 100% de acurácia na geolocalização MaxMind e APIs remotas. Ocultamento de dados sensíveis de servidores RPKI (Routinator).
* **Mitigação Terrapin Attack SSH.NET (`v2026.0.0`)**: Atualização dos algoritmos de aperto de mão estrito (*Strict Key Exchange*) para neutralizar a vulnerabilidade CVE-2023-48795 (GHSA-q939-rpr3-3284).
* **CGNAT Graylog Forensics Otimizado (`v3.4.1`)**: Otimização de consultas Lucene via pré-cálculo de início de bloco BPA ($\lfloor \text{porta} / 256 \rfloor \times 256$), suporte a eventos NetFlow v9 IPFIX (`nf_field_230`: 1 = CREATE, 2 = RELEASE) e criptografia Windows DPAPI (`DataProtectionScope.CurrentUser`) para armazenamento seguro de credenciais.

---

## 3. Módulos Técnicos e RFCs Aplicadas

### 3.1 ICMP Discovery & Path Audit
* **Especificação Técnica**: Motor de varredura massiva paralelo que dispara pulsos ICMP Echo Request para sub-redes IPv4 (ex: `/24`, `/22`, `/16`). Utiliza `System.Threading.Channels` com concorrência regulável (32 a 256 workers) e renderização de resultados em tabela virtualizada Blazor (`<Virtualize>`).
* **Auditoria PMTU & MSS**: Envio de datagramas com a flag DF (*DontFragment* = 1) conforme a **RFC 1191**. Executa varredura binária para identificar o menor MTU suportado pelo caminho de rede sem fragmentação.
* **RFCs Relacionadas**:
  * **RFC 792**: Internet Control Message Protocol (ICMP Specification).
  * **RFC 1191**: Path MTU Discovery.
  * **RFC 791**: Internet Protocol (IPv4 Specification).

### 3.2 Live TCP/UDP Watcher
* **Especificação Técnica**: Mapeamento em tempo real de conexões ativas e portas em escuta no sistema operacional Windows via chamadas nativas `GetExtendedTcpTable` e `GetExtendedUdpTable` (`IPHlpApi.dll`).
* **Classificação de Endereçamento por RFC**:
  * **RFC 1918**: Address Allocation for Private Internets (`10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`).
  * **RFC 6598**: IANA-Reserved IPv4 Prefix for Shared Address Space / CGNAT (`100.64.0.0/10`).
  * **RFC 3927**: Dynamic Configuration of IPv4 Link-Local Addresses / APIPA (`169.254.0.0/16`).
  * **RFC 2544**: Benchmarking Methodology for Network Interconnect Devices (`198.18.0.0/15`).
  * **RFC 5737**: IPv4 Address Blocks Reserved for Documentation / TEST-NET (`192.0.2.0/24`, `198.51.100.0/24`, `203.0.113.0/24`).
  * **RFC 4291 / RFC 4193**: IPv6 Addressing Architecture e Unique Local IPv6 Unicast Addresses (`fc00::/7`, `fe80::/10`).
* **Medição de Throughput**: Leitura contínua dos contadores de I/O de processos no kernel (`GetProcessIoCounters`) para exibir taxas de transferência reais (Mbps/Kbps) associadas a executáveis como `msedge.exe`, `chrome.exe`, `firefox.exe`.

### 3.3 Web 360° Deep Forensics
* **Especificação Técnica**: Analisador L3-L7 de ativos web. Realiza extração e dissecação de sub-recursos (JavaScript, CSS, Fontes, Imagens e Serviços de Anúncios) no DOM raiz.
* **RFCs Relacionadas**:
  * **RFC 8305**: Happy Eyeballs Version 2: Better Connections Through Dual-Stack-Capable Algorithms (avaliação de conectividade concorrente IPv4 vs IPv6 com cálculo de tempo de penalidade).
  * **RFC 7230 / RFC 7540**: Hypertext Transfer Protocol (HTTP/1.1 e HTTP/2).

### 3.4 Suíte SNMP Walker & MIB Browser AST
* **Especificação Técnica**: Compilador ASN.1 em dois passes para arquivos MIB (SMIv1/SMIv2). Constrói a árvore sintática de OIDs, resolve nomes textuais (ex: `1.3.6.1.2.1.2.2.1.2` $\rightarrow$ `ifDescr`) e executa varreduras resilientes `WalkLoopResilient` com tratamento de falhas em switches/ONUs TP-Link, MikroTik, Cisco, Datacom, FiberHome e ZTE.
* **Observabilidade**: Gerador automático de templates Zabbix 6.0/7.0 com Low-Level Discovery (LLD) e arquivos de configuração Prometheus `snmp_exporter` (`snmp.yml`).
* **RFCs Relacionadas**:
  * **RFC 1157**: Simple Network Management Protocol (SNMPv1).
  * **RFC 1901 / RFC 1908**: Simple Network Management Protocol v2c (SNMPv2c).
  * **RFC 3411 - RFC 3418**: SNMPv3 Framework, User-based Security Model (USM) e View-based Access Control Model (VACM).
  * **RFC 1213 / RFC 2863**: Management Information Base for Network Management of TCP/IP-based internets (MIB-II) e The Interfaces Group MIB (IF-MIB).

### 3.5 Wireless RF Tests (Motor Fluke AirCheck)
* **Especificação Técnica**: Telemetria e análise de espectro Wi-Fi baseada nas APIs nativas do Windows WLAN (`wlanapi.dll`).
* **Inteligência MESH**: Algoritmo que agrupa e distingue nós cooperativos MESH (ex: TP-Link Deco, Google Wifi) de redes concorrentes operando no mesmo canal, prevenindo alarmes falsos de interferência co-canal (CCI).
* **Padrões IEEE**: IEEE 802.11a/b/g/n/ac/ax/be, IEEE 802.11k/v/r (Fast Roaming e BSS Transition Management).

### 3.6 Ping & Trace Suite / MTR Avançado
* **Especificação Técnica**: Utilitário de diagnóstico ICMP contínuo, cadeia multi-ping e MTR com heurística anti-CoPP (Control Plane Policing).
* **RFCs Relacionadas**:
  * **RFC 792**: Internet Control Message Protocol.
  * **RFC 3393**: IP Packet Delay Variation Metric for IP Performance Metrics (Cálculo normalizado de Jitter).

### 3.7 Ethernet Tests L2
* **Especificação Técnica**: Diagnóstico operando na Camada de Enlace de Dados. Escuta passiva de anúncios de infraestrutura (LLDP, CDP, MNDP) e testes ativos.
* **Protocolos e Padrões**: IEEE 802.1Q (VLAN Tagging), IEEE 802.3 (Ethernet), RFC 2516 (PPPoE Specification), RFC 2131 (Dynamic Host Configuration Protocol - DHCP).

### 3.8 Rastreio Forense CGNAT (Graylog)
* **Especificação Técnica**: Motor de busca forense integrado a clusters Graylog (REST API v4/v5) para localização de assinantes em blocos de portas compartilhados (Cisco Bulk Port Allocation - BPA).
* **Conformidade Legal**: Emissão de laudos periciais com hash SHA-256 enquadrados no Marco Civil da Internet (Lei 12.965/2014, Art. 15) e LGPD (Lei 13.709/2018, Art. 7º).
* **RFCs Relacionadas**:
  * **RFC 6598**: IANA-Reserved IPv4 Prefix for Shared Address Space (Carrier-Grade NAT).

---

## 4. Comparativo de Engenharia: RezTerm vs Ferramentas de Mercado

| Recurso / Arquitetura | RezTerm v3.4.5 | Wireshark | PuTTY / WinSCP | SolarWinds / PRTG | MTR / Ping |
| :--- | :--- | :--- | :--- | :--- | :--- |
| **Arquitetura de Execução** | ReadyToRun Native (.NET 10 + Blazor Hybrid) | Aplicação Qt/C++ Célula Única | Aplicação C Win32 Legada | Suíte Baseada em Servidor / Web | Utilitário CLI Monolítico |
| **Varredura ICMP Massiva** | SIMD Parallel Channels (até 256 threads) | Não Aplicável | Não | Polling Agendado Lento | Não (Apenas Salto Único) |
| **Auditoria Path MTU & MSS** | Amostragem Binária Ativa com Bit DF | Análise Passiva | Não | Não | Não |
| **Geolocalização IP** | 100% Local-First (MemoryMappedFile) | Requer Plugins Externos | Não | Consulta Nuvem / Servidor | Não |
| **Terminal SSH** | xterm.js GPU Direct + Debouncing 16ms | Não | Console Texto Padrão | Console Básico | Não |
| **Segurança e Credenciais** | Criptografia Nativa DPAPI + HMAC-SHA256 | Arquivos Texto Claro | Registro Windows sem Criptografia | Banco de Dados Central | Não |
| **Consumo de Memória / CPU** | Reduzido (Garbage Collector Server SIMD) | Elevado em Grandes PCAPs | Baixo | Elevado (Requer Servidor) | Baixo |

---

## 5. Sistema de Licenciamento Criptográfico (HWID & HMAC-SHA256)

O **RezTerm** utiliza um mecanismo de licenciamento offline projetado para garantir o controle corporativo sem depender de servidores de autenticação externos:

1. **Hardware ID (HWID)**: Identificador exclusivo de 12 caracteres derivado do `MachineGuid` do Windows e da assinatura de hardware (CPU e placa-mãe) via hash SHA-256.
2. **Assinatura HMAC-SHA256**: As chaves de ativação são geradas com chave secreta mestre de 256 bits, validando o período de concessão e o titular. Qualquer modificação no arquivo local de licença resulta na invalidação imediata da sessão.

---

## 6. Requisitos de Sistema

* **Sistema Operacional**: Windows 10 (64-bit) versão 1903 ou superior / Windows 11.
* **Componente de Tempo de Execução**: Microsoft Edge WebView2 Runtime (pré-instalado no Windows 10/11).
* **Biblioteca de Captura de Pacotes (Opcional)**: Npcap 1.70 ou superior (necessário apenas para captura bruta no Leitor PCAP e testes L2).
* **Processador**: Intel Core i3 / AMD Ryzen 3 ou superior (com suporte a instruções AVX2 recomendado).
* **Memória RAM**: Mínimo 4 GB RAM (Recomendado 8 GB).

---

## 7. Informações de Lançamento e Suporte

Desenvolvido por **Reginaldo Junior** para otimização das operações de engenharia de redes da **Audicom Telecom**.

* **Repositório Público de Download**: [github.com/juniorespow/RezTerm-Downloads](https://github.com/juniorespow/RezTerm-Downloads)
* **Licenciamento Corporativo**: Sujeito a concessão prévia de chave HWID pela administração de TI/NOC.
