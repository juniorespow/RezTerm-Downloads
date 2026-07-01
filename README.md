# ⚡ RezTerm v2.0+ (Cyberpunk SOC/NOC Suite)

<div align="center">

![.NET Core](https://img.shields.io/badge/.NET%2010.0-512BD4?style=for-the-badge&logo=dotnet&logoColor=white)
![Blazor Hybrid](https://img.shields.io/badge/Blazor%20Hybrid-5C2D91?style=for-the-badge&logo=blazor&logoColor=white)
![WPF](https://img.shields.io/badge/Windows%20WPF-0078D4?style=for-the-badge&logo=windows&logoColor=white)
![C#](https://img.shields.io/badge/C%23%2013-239120?style=for-the-badge&logo=c-sharp&logoColor=white)
![Security](https://img.shields.io/badge/Security-DPAPI%20%2B%20HMAC-00f0ff?style=for-the-badge)

**A Suíte Definitiva de Engenharia de Redes, Diagnóstico SOC/NOC, Auditoria Forense e Terminal SSH Multi-Aba.**  
Desenvolvida por **Reginaldo Junior (Razon)** combinando a performance nativa do Windows (.NET 10 WPF / ReadyToRun Native) com uma interface ultramoderna Blazor Hybrid em estética **Cyberpunk Dark Neon**.

</div>

---

## 🌌 1. Identidade Visual Cyberpunk Dark Neon
O **RezTerm** foi projetado para longas jornadas de operação cibernética em ambientes críticos (Datacenters, ISPs, provedores de telecom e salas de controle NOC/SOC):
* **Ditadura do Tema Dark**: Superfícies profundas (`#0D1117`), cards estruturados (`#161B22`) e bordas de alta precisão (`#30363D`), eliminando a fadiga ocular.
* **Acentos em Ciano Neon (`#00f0ff`)**: Toda interatividade visual, radares, gráficos interativos, badges de protocolo e botões ativos utilizam a luminescência azul neon para leitura imediata e feedback tátil.
* **Renderização DWM Nativa**: A janela do sistema é blindada contra travamentos e integra renderização escura na própria barra de título do Windows 11/10 (`DwmSetWindowAttribute`).

---

## 🛠️ 2. Suíte de Ferramentas Integradas

| Módulo | Descrição Principal | Destaques de Engenharia |
| :--- | :--- | :--- |
| **📊 Dashboard & Latência** | Monitoramento em tempo real da saúde da conexão e dual-stack ISP. | Gráficos de latência em tempo real, detecção de perda de pacotes e status de pilha nativa. |
| **💻 Terminal SSH Studio** | Client SSH multi-aba de alta performance com `xterm.js`. | Cofre de senhas criptografado DPAPI + HMAC-SHA256, barra de snippets rápidos e SFTP integrado. |
| **🏓 Ping & Trace Suite** | Motores avançados de ICMP, Ping Contínuo e MTR visual. | **Seletor de Pilha IP (IPv4/IPv6/Auto)** com filtragem estrita por família DNS e **Cálculo de Jitter de Destino** isolado no MTR. |
| **📡 IP Scan & APIPA** | Varredura minuciosa de sub-redes locais com ARP/Ping/TCP Sweep. | **Resgate APIPA (RFC 3927)** para resgate de switches e roteadores sem servidor DHCP ativo. |
| **⚡ Live TCP/UDP Watcher** | Monitoramento de sockets abertos e conexões ativas no Windows. | Integração nativa com **GeoLite2 MMDB em Memória (MMF)** projetando conexões em **Mapa Mundi interativo**. |
| **🌐 NetOps & Whois/IRR** | Consulta unificada a bases mundiais de registro de IPs e ASNs. | Conectores diretos para RADB, RIPE, LACNIC, ARIN, APNIC e AFRINIC com formatação de blocos BGP. |
| **🔌 Ethernet Tests L2** | Verdadeiro "Fluke de Software" operando na Camada de Enlace (L2). | Escuta passiva LLDP/CDP/MNDP, injeção ativa de **PADI Broadcast (PPPoE Rogue)** e **DHCP Discover**. |
| **📶 Wireless Tests RF** | Analisador de espectro Wi-Fi e qualidade de sinal em tempo real. | Gráficos de sinal de redes vizinhas 2.4 GHz, 5 GHz e 6 GHz (Wi-Fi 6E/7) com cálculo de SNR. |
| **🕵️ Rastreio Forense CGNAT** | Investigação forense em servidores Graylog com geração de relatórios. | Exportação nativa em PDF e TXT com cláusulas jurídicas obrigatórias (Marco Civil da Internet e LGPD). |

---

## 🕵️ 3. Módulo Forense & Rastreio CGNAT (Graylog)

O **RezTerm** integra um motor de busca forense desenvolvido especificamente para analistas de segurança investigarem conexões criminosas ou incidentes cibernéticos através de logs de CGNAT centralizados em clusters **Graylog**.

### 📋 Passo a Passo: Como Configurar o Graylog no RezTerm

1. **Acessar o Módulo**: No menu lateral esquerdão do RezTerm, clique na aba **"🕵️ Graylog (CGNAT Forense)"**.
2. **Gerenciamento de Servidores**: No topo da tela, clique no botão **"⚙️ Gerenciar Servidores Graylog"**.
3. **Cadastrar Novo Cluster**: Clique em **"➕ Novo Servidor"** e preencha os parâmetros do nó Graylog:
   * **Nome Identificador**: Ex: `Cluster Graylog - Core Datacenter SP`.
   * **Hostname ou IP**: Ex: `graylog.provedor.intranet` ou `10.10.50.15`.
   * **Porta REST API**: Padrão `9000` (ou `443` se estiver atrás de reverse proxy HTTPS).
   * **API Key / Token**: Gere uma API Key com permissão de leitura (`read:messages`) no painel web do Graylog (*System -> Users -> Create API Token*) e cole no RezTerm. A chave será armazenada de forma criptografada pelo sistema.
   * **Compatibilidade de Versão**: Selecione o motor correspondente ao seu parque:
     * `v4.x Legado`: Para servidores Graylog nas séries 4.0, 4.1 e 4.2.
     * `v5.x Moderno`: Para versões Graylog 5.0+ e Opensearch 2.x.
4. **Testar & Ativar**: Clique em **Salvar**. O RezTerm validará a conectividade. Se bem-sucedido, selecione o servidor na lista para iniciar as investigações.

### 🔍 Executando Rastreios Forenses com Conformidade Jurídica
* **Busca Cirúrgica por IP/Porta**: Informe o IP Público, Porta de Origem (opcional) e a Data/Hora exata do fato. O motor compõe automaticamente a query Lucene estrita (`nf_proto: "6" AND nf_xlate_src_addr_ipv4: "..." AND nf_postnatportblockstart: "..."`).
* **Extração Jurídica (PDF & TXT)**: Ao clicar em **"📄 Exportar Laudo Forense PDF"** ou **"📋 Exportar TXT"**, o sistema abre a janela de escolha de pastas do Windows (`SaveFileDialog`) e gera um laudo forense profissional contendo:
  * Cabeçalho institucional do provedor/empresa e dados do analista responsável.
  * **Cláusula de Conformidade com o Marco Civil da Internet (Lei nº 12.965/2014 - Art. 15)** justificando a preservação e extração legal de dados de conexão.
  * **Cláusula de Proteção de Dados (LGPD - Lei nº 13.709/2018 - Art. 7º, VI e IX)** assegurando o tratamento para exercício regular de direitos em processo judicial ou legítimo interesse na segurança da rede.
  * **Hash Criptográfico de Integridade (SHA-256)** gerado a partir do conteúdo exato dos logs extraídos para blindagem probatória em tribunais.

---

## 🛡️ 4. Arquitetura de Segurança & Blindagem

O RezTerm adota uma postura de segurança defensiva (*Security by Design*) em cada camada de software:

1. **Compilação Blindada (*Single-File ReadyToRun Native*)**:
   - Os executáveis de distribuição (`SepulnationTerm.exe` e `RezTermSetup.exe`) são compilados no modo `PublishSingleFile` + `PublishReadyToRun`, gerando instruções de máquina pré-compiladas nativas (`win-x64`) com desativação total de símbolos de debug (`DebugSymbols=false`), dificultando ataques de engenharia reversa e decompilação via ILSpy/dnSpy.
2. **Cofre Criptográfico DPAPI + HMAC-SHA256 (`HostStorageService`)**:
   - Nenhuma senha de roteador, chave privada SSH ou token de API Graylog é gravada em texto plano.
   - O sistema utiliza a **DPAPI (Data Protection API) do Windows** acoplada à conta do usuário de domínio em execução (`DataProtectionScope.CurrentUser`), reforçada com um código de autenticação de mensagem hash **HMAC-SHA256** para prevenir adulterações de arquivo no diretório local.
3. **Observabilidade Blindada com Mascaramento (`RezLogger.cs`)**:
   - Sistema de logging estruturado em JSON Lines (`.jsonl`) rotativo com expurgo automático após 14 dias.
   - Antes de persistir qualquer exceção ou evento de auditoria no disco local, o logger executa varredura profunda de mascaramento (*Data Masking*), substituindo automaticamente senhas, tokens e chaves por `"***MASKED***"`.

---

## 🚀 5. Instalação & Atualizações CDN Automáticas

O RezTerm possui um assistente bootstrapper nativo (`RezTermSetup.exe`) que garante a instalação limpa, sem dependências externas de administração, diretamente no perfil do técnico (`%LocalAppData%\RezTerm`):
* **Sincronização de Cache de Ícone**: O instalador força a atualização do cache gráfico do Shell do Windows (`SHChangeNotify`) garantindo que o novo ícone Cyberpunk seja exibido imediatamente na barra de tarefas e área de trabalho.
* **Auto-Updater via GitHub CDN**: Ao abrir a ferramenta, o serviço `UpdateService` consulta anonimamente a API pública de lançamentos (`juniorespow/RezTerm-Downloads`). Caso uma nova versão esteja disponível, o analista recebe um alerta no topo da tela podendo baixar e aplicar a atualização em 1 clique sem interromper suas sessões.

---
<div align="center">
<b>RezTerm SOC/NOC Suite</b> • Engenharia Cibernética de Alta Performance • Reginaldo Junior (Razon)
</div>
