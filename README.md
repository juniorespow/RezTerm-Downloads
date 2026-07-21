# ⚡ RezTerm v3.2.2 (Cyberpunk Network Engineer Toolkit & Forensics Suite)

<div align="center">

![.NET Core](https://img.shields.io/badge/.NET%2010.0-512BD4?style=for-the-badge&logo=dotnet&logoColor=white)
![Blazor Hybrid](https://img.shields.io/badge/Blazor%20Hybrid-5C2D91?style=for-the-badge&logo=blazor&logoColor=white)
![WPF](https://img.shields.io/badge/Windows%20WPF-0078D4?style=for-the-badge&logo=windows&logoColor=white)
![C#](https://img.shields.io/badge/C%23%2013-239120?style=for-the-badge&logo=c-sharp&logoColor=white)
![Security](https://img.shields.io/badge/Security-DPAPI%20%2B%20HMAC-00f0ff?style=for-the-badge)
![Hardware Acceleration](https://img.shields.io/badge/HW%20Acceleration-GPU%20%2B%20SIMD-00ff88?style=for-the-badge)
![RF Intelligence](https://img.shields.io/badge/RF%20Fluke%20Engine-MESH%20Triage-00f0ff?style=for-the-badge)

Suíte Definitiva de Diagnóstico de Redes, Auditoria Forense NOC/SOC, Triagem L2/L3 e Análise de Tráfego de Alta Performance — Otimizada em **.NET 10.0 Native/ReadyToRun WPF/Blazor Hybrid** com **Arquitetura AOT/PGO Nativa e Zero-Alloc (`v3.1.0`)**, **Motor Inteligente de Agressividade &amp; Autonomia de Bateria (`v3.1.0`)**, **Aceleração Hardware (GPU/AVX2/AVX-512) Universal (`v3.0.2`)**, **Gateway Dual IPv4/IPv6 Simultâneo (`v3.0.0`)**, **Terminal SSH Studio Ultra Fluido (`v2.2.9`)** e muito mais.

</div>

---

## 🚀 Sobre o Projeto

Desenvolvido por **Reginaldo Junior**, um Engenheiro de Redes com ampla experiência operacional que buscou criar uma alternativa moderna e acessível aos softwares tradicionais de mercado que costumam exigir modelos complexos de contratação. O **RezTerm** surge como uma plataforma autônoma e de alta performance para diagnóstico de conectividade, monitoramento e triagem forense, rodando diretamente no metal do Windows (.NET 10 WPF / ReadyToRun Native) com uma interface corporativa de última geração em tecnologia Blazor Hybrid no padrão **Cyberpunk Dark Neon**, **Arquitetura AOT/PGO Nativa e Zero-Alloc (`v3.1.0`)**, **Controle de Agressividade &amp; Autonomia de Bateria (`v3.1.0`)**, **Hotfix GPU Universal (`v3.0.2`)**, **Inteligência Integral de Conectividade &amp; Anti-Oscilação (`v3.0.0`)**, **Triagem Ethernet L2 Customizável (`v3.0.0`)**, **Correção do Travamento Cisco Exit Lock no SSH (`v2.2.9`)**, **Responsividade Universal (`v3.0.0`)**, **Inteligência RF MESH / Repetidores (`v2.2.6`)** e o revolucionário **Motor Inteligente Anti-CoPP Rate-Limit 3 Fases**.

---

## 🔥 Novidades &amp; Otimizações — Versão `v3.1.0` (Julho / 2026)

A versão **`v3.1.0`** coroa uma revolução de engenharia no ecossistema RezTerm. O projeto foi integralmente otimizado para extrair o máximo poder do **.NET 10** através de um plano de ação em 4 Fases focadas em velocidade instantânea, baixo consumo de memória, concorrência extrema e segurança corporativa:

* **⚡ Abertura e Carregamento Instantâneo (Source Generators AOT)**: O motor de serialização abandonou mecanismos legados baseados em *Reflection* e adotou o gerador nativo `[JsonSerializable]` do .NET 10 (`RezTermJsonContext`). O tempo de inicialização (*cold start*) despencou de ~3.2s para **~1.0s**, abrindo cofres, perfis e históricos no ato sem alocações extras de memória.
* **🛡️ Blindagem de Senhas &amp; Auditoria Forense Inviolável (SHA-256 / DPAPI)**: Implementada sanitização automática (`[GeneratedRegex]`) que identifica e censura senhas, tokens e chaves privadas em logs antes de tocarem no disco (`[DATA MASKED]`). Além disso, os relatórios técnicos em PDF exportados após manutenções agora recebem um **Selo Criptográfico SHA-256** no rodapé, assegurando validade forense contra adulteração posterior.
* **💻 Concorrência Zero-Alloc &amp; Baixo Consumo (`Span<T>` &amp; `FrozenDictionary`)**: Reescrita profunda de algoritmos quentes do sistema (geração de HWID de licença, resoluções MAC/OUI e processamento PCAP) utilizando `ReadOnlySpan<char>`, buffers `stackalloc` e estruturas congeladas `FrozenDictionary`. O uso médio de RAM caiu para a faixa de **~105 MB**, permitindo operação contínua 24/7 sem sobrecarregar laptops ou servidores.
* **🏁 Terminal SSH 60 FPS &amp; Timers Sem Desvio (*Zero Drift*)**: A recepção de dados no terminal e na UI de varredura migrou de travas antigas (`lock(object)`) para a primitiva moderna **`System.Threading.Lock`** e canais assíncronos (`Channel<string>`), eliminando congelamentos da tela sob enxurrada de pacotes. Os diagnósticos de rede ao vivo adotaram `PeriodicTimer`, mantendo o tempo real milimetricamente preciso sem acúmulo de desvio com o passar das horas.
* **🍃 Evolução de Agressividade &amp; Autonomia de Bateria**: Como o software se tornou extremamente leve para a CPU do computador, a comutação de perfis foi ressignificada e evoluída na interface:
  - **`🚀 Alta Performance (Antigo Modo Normal)`**: Aloca 100% dos núcleos lógicos do sistema em até 2.500 threads simultâneas e sondagens de 1,2s. Ideal para operação no NOC via cabo Gigabit/10G e diagnósticos profundos em tempo real.
  - **`🍃 Economia de Energia (Antigo Modo Eficiente)`**: Limita a varredura a um teto de 150 threads e sonda os adaptadores de 3,6s em 3,6s. Especialmente desenhado para técnicos em campo no notebook operando na bateria (estendendo horas de autonomia) ou ao varrer switches legados sem causar picos de processamento nos equipamentos da rede.
* **Motor de Eficiência Adaptativa Persistente (`v3.0.4`)**: Deteção autônoma de processadores modestos ou notebooks (`<= 4` núcleos/threads como i5-6300U, i3, Celeron). Persistência automática das escolhas de perfil em JSON (`%LocalAppData%\RezTerm\engine_profile.json`), eliminando a repetição do pop-up de diagnóstico a cada inicialização! Ativação de **WMI Orientado a Eventos**, **Zero-CPU Boot Throttling**, e **Blindagem de Paralelismo (`SmartMaxDegreeOfParallelism`)**, garantindo que todas as varreduras pesadas reservem sempre um núcleo dedicado para que o mouse e a janela permaneçam 100% fluidos! Alternância entre os perfis a qualquer momento pelo menu lateral!
* **Hotfix GPU Universal (`v3.0.2`)**: Coleta de carga de GPU resgatada e blindada para sistemas Windows localizados (PT-BR, ES, EN). Suporte completo às categorias `"GPU Engine"` / `"Mecanismo de GPU"`, capturando instâncias 3D, Compute e Video Decode com heurística de fallback em tempo real.
* **Inteligência Integral de Conectividade & Anti-Oscilação (`v3.0.0`)**: Varredura multi-camada que categoriza com precisão cirúrgica 5 estados reais da interface (`ONLINE`, `DEGRADED`, `ISOLATED // Azul Neon`, `DISCONNECTED` e `DISABLED`). Trava de purga instantânea no motor SIMD/WMI que zera os timeouts do período offline no primeiro milissegundo em que o cabo é reconectado, eliminando 100% das oscilações e demoras na estabilização do Dashboard (`Zero Oscilação`).
* **Triagem Ethernet L2 Customizável (`v3.0.0`)**: Parâmetros interativos no teste de Camada de Enlace permitindo inspecionar portas **Trunk vs Access (VLAN Específica ou Taggeada)** e personalizar a duração do motor de injeção contínua (até 60 segundos) com barra de progresso sincronizada.
* **Correção do Travamento de Sessão Cisco Exit Lock (`v2.2.9`)**: Fim do congelamento ou travamento de aba ao executar comandos `exit` / `quit` em switches e roteadores Cisco (IOS / IOS-XR / NX-OS), Huawei e Datacom. Leitura assíncrona limpa (`ReadAsync` identificando 0 bytes / EOF) sincronizada com heurística de encerramento de sessão e notificação visual instantânea `🛑 SESSION STOPPED - Sessão Encerrada [ Desconectado ]`.
* **Responsividade Absoluta no Dashboard & Menu Lateral 14" (`v3.0.0`)**: Adaptação autônoma via media queries (`@media max-height: 860px` e `720px`), garantindo que 100% dos painéis holográficos offline, cards de telemetria, títulos longos e os 13 itens da suíte caibam com perfeição na tela sem quebras indesejadas ou barras de rolagem (`scrollbar zero`).
* **Nome de Processo Oficial `RezTerm.exe` (`v2.2.3`)**: O executável nativo compilado no Windows foi integralmente alinhado para aparecer como **`RezTerm.exe`** no Gerenciador de Tarefas e em monitoramentos de processos SOC/NOC.
* **Motor de Aceleração de Hardware & GPU Engine (`v2.2.2`)**: Deteção automática de GPU dedicada ou integrada (NVIDIA RTX, Intel HD Graphics, AMD Radeon) com varredura robusta de instâncias 3D/Compute/phys_0 e exibição precisa de `0.0%` em repouso absoluto.

---

## 🛠️ 2. Suíte de Ferramentas Integradas (v3.0.0)

| Módulo | Descrição Principal | Destaques de Engenharia |
| :--- | :--- | :--- |
| **📶 Wireless Tests RF (`v2.2.6`)** | Analisador de espectro Wi-Fi e qualidade de sinal em tempo real (Fluke AirCheck RF). | **Inteligência MESH / Zero Falsos Positivos (`v2.2.6`)**: Algoritmo que reconhece automaticamente redes MESH Wi-Fi (ex: TP-Link Deco, Google Wifi) e repetidores operando no mesmo SSID e Canal, excluindo-os da contagem de interferência co-canal (`CCI`) e separando redes concorrentes externas de nós cooperativos (`ConnectedMeshOrSiblingNodes`); **Modal Cyberpunk Interativo (`🚨 ABRIR LAUDO DE MELHORIAS`)** com tabela dedicada de **Topologia MESH / Multi-AP**, indicação do canal mais limpo do local (`GetBestRecommendedChannel`), recomendações de Band Steering para 5 GHz e auditoria de Fast Roaming 802.11k/v/r; **Auditoria IEEE Priorizada (`⭐ REDE CONECTADA`)** no topo da aba de boas práticas e **Responsividade Inteligente para Notebooks de 14" (`1366x768`)** na tabela de telemetria e no grid de canais. |
| **📊 Dashboard & Latência (`v3.0.0`)** | Monitoramento em tempo real da saúde da conexão, dual-stack ISP e telemetria de Hardware. | **Inteligência Integral de Conectividade & Anti-Oscilação (`v3.0.0`)**: Varredura WMI/SIMD em 5 estados com purga instantânea na reconexão (`Zero Oscilação`), **Responsividade Cibernética Universal (`v3.0.0`)** no painel holográfico offline e sub-blocos, **HUD de Boot Atualizado** com legenda `NETWORK ENGINEER TOOLKIT // CYBERPUNK CORE`, **HotFix GPU Load (`v2.2.2`)** com suporte universal NVIDIA/Intel/AMD e exibição `0.0%` sem `N/A`, **Precisão Absoluta em Memória RAM (`GlobalMemoryStatusEx`)**, **Motor Híbrido Anti-CoPP Rate-Limit (TCP SYN Bypass em portas 80/443)** para evitar alarmes falsos de queda, Gateway Dual e Badge de Aceleração GPU/SIMD. |
| **📡 Leitor PCAP Forense (`v2.1.0`)** | Analisador e dissecador forense de pacotes (.pcap/.pcapng) com aceleração SIMD e mapeamento no kernel. | **Motor Gráfico 60 FPS GPU Direct Canvas/WebGL (`pcap-cyberpunk-map.js`)** com luzes pulsantes esmaecendo e brilhando (*Breathing Neon Particles*), **Zoom/Pan com bloqueio nativo de rolagem da janela (`{passive: false}`)** e resiliência a abas; **Heurística de Redes, NOC e SOC** para 9 protocolos core (`BGP`, `OSPF`, `IS-IS`, `MPLS/VPLS`, `PPPoE`, `DHCP`, `IPv6 RA Guard`), inspeção interativa de quadros com Hex Dump e ASCII, botão de upload personalizado e popup de aviso forense. |
| **💻 Terminal SSH Studio (`v2.2.9`)** | Client SSH multi-aba de alta performance com `xterm.js`. | **Correção do Bug de Travamento Cisco Exit Lock (`v2.2.9`)**: Desconexão instantânea e liberação limpa de PTY/ShellStream ao digitar `exit` em equipamentos Cisco, Huawei ou Datacom sem prender a aba; **Fluidez Extrema a 60 FPS** via debouncing buffer C# (16ms) e bypass streaming JS para comandos >12KB, **Sincronização Dinâmica SIGWINCH** (`htop`/`btop`), **Syntax Highlighting** e **Copiar Tudo Buffer**. |
| **🏓 Ping & Trace Suite (`v2.2.3`)** | Motores avançados de ICMP, Ping Contínuo, Cadeia Multi-Ping e MTR. | **Responsividade Inteligente no MTR Avançado (`v2.2.3`)**: Painel superior de controles reestruturado em grid flexível multi-linha com auto-escalonamento, garantindo que o campo **Destino (Host / IP / Domínio)** tenha largura generosa (`min-width: 240px`) e nunca fique cortado em telas de 14" (`1366x768`); **Motor Inteligente Anti-CoPP Rate-Limit 3 Fases (Heurística de Salto Intermediário vs Destino + Poisson Jittering + TCP SYN Bypass)** com selo azul neon **`⚡ CoPP BYPASS`**, **Cadeia Multi-Ping** com laudo formatado, **Seletor de Pilha IP (IPv4/IPv6/Auto)** e **Cálculo de Jitter RFC 3393** isolado no MTR. |
| **📡 IP Scan & Port Scanner SIMD (`v2.1.1`)** | Varredura minuciosa de sub-redes locais e auditoria forense de portas (`Port Scanner SIMD Pro v2.2`). | **Aceleração SIMD Multi-Core Paralela** (até 1.500 threads com *throttling* adaptativo de rede), **Eliminação de Falsos Positivos UDP via Sondas Ativas de Payload** (DNS, NTP, SNMP, SIP + detecção de ICMP Port Unreachable), **Deep Banner Grabbing & Inspeção TLS Forense** com captura de certificado X.509, **Triage de Risco SOC (`Crítico/Alto/Normal`)** com notas de mitigação e **Hex Dump Preview Raw**, além de exportação de laudos CSV em tempo real via **`rezTermFileSave`**. |
| **⚡ Live TCP/UDP Watcher** | Monitoramento de sockets abertos e conexões ativas no Windows. | Integração nativa com **GeoLite2 MMDB em Memória (MMF)** projetando conexões em **Mapa Mundi interativo**. |
| **🌐 NetOps & Whois/IRR** | Consulta unificada a bases mundiais de registro de IPs e ASNs. | Conectores diretos para RADB, RIPE, LACNIC, ARIN, APNIC e AFRINIC com formatação de blocos BGP. |
| **🔌 Ethernet Tests L2 (`v3.0.0`)** | Verdadeiro "Fluke de Software" operando na Camada de Enlace (L2). | Escuta passiva LLDP/CDP/MNDP, injeção ativa de **PADI Broadcast (PPPoE Rogue)**, **DHCP Discover**, verificação interativa de **Porta Trunk vs Access com VLAN Específica (`v3.0.0`)** e motor customizável com barra de progresso sincronizada (até 60s). |
| **🕵️ Rastreio Forense CGNAT** | Investigação forense em servidores Graylog com geração de relatórios. | **Aceleração Vetorial SIMD AVX2/AVX-512 Paralela** (até 250x mais rápido), **Modo Híbrido Bimodal**, cálculo de blocos **Cisco BPA (RFC 6598)** e exportação em PDF/TXT com cláusulas jurídicas e hash SHA-256. |

---

## 🔑 3. Sistema de Licenciamento Criptográfico e Controle de Acesso

Para proteger a propriedade intelectual corporativa e evitar a distribuição não autorizada da suíte de ferramentas de alta capacidade, o **RezTerm** implementa um controle rigoroso de licenciamento offline vinculado ao hardware:

* **Autenticação Vinculada ao Hardware (HWID)**: O sistema gera um código único e intransferível de 12 caracteres (ex: `REZ-8F9A-2B1C-4D5E`) computado via hash criptográfico SHA-256 a partir do `MachineGuid` e da assinatura de CPU/Placa-mãe do PC ou Notebook do analista.
* **Chaves Corporativas HMAC-SHA256**: A licença não funciona por simples verificação de texto, mas sim por assinatura criptográfica **HMAC-SHA256** utilizando um segredo mestre de 256 bits (`MasterSecret`). Qualquer tentativa de adulteração do arquivo `license.json` ou da data de validade invalida a chave instantaneamente.
* **Fluxo para o Usuário (Analista/HelpDesk)**:
  1. Ao iniciar o `RezTerm.exe`, o sistema abre em **Tela Cheia Maximizada** e exibe a tela modal de bloqueio **🔒 RezTerm Corporativo - Licença Requerida**.
  2. O técnico clica em **`[ Copiar meu HWID e Solicitar Licença ]`** e envia o código para a gestão do sistema.
  3. Com a chave recebida, o técnico cola no campo e clica em **Ativar e Desbloquear Sistema**.
  4. O status fica sempre visível no topo da Dashboard via badge verde brilhante `🔒 Licenciado (...)`. Ao clicar no badge, um popup interativo exibe o titular, setor, HWID e chave HMAC-SHA256.
* **Fluxo para a Gestão do Sistema (`RezTermKeygen.exe`)**:
  * Ferramenta privada executável geradora de chaves exclusiva da administração e time de engenharia. O executável oficial compilado (no pacote `RezTermKeygen.zip`) está disponível na pasta de ferramentas da gestão na raiz deste repositório privado.
  * O administrador cola o HWID do colaborador, define o Nome/Setor do titular e seleciona o período de concessão (**30 Dias Experiência**, **180 Dias**, **365 Dias Anual** ou **Vitalício / Permanente**).
  * O sistema gera a string assinada pronta para envio (ex: `REZ-PRO-20270706-8F9A-2B1C-4D5E-7A8B9C0D1E2F3A4B`).

---

## 🕵️ 4. Módulo Forense & Rastreio CGNAT (Graylog)

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

## 🛡️ 5. Arquitetura de Segurança & Blindagem

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

## 🚀 6. Histórico de Evolução Arquitetural e Releases Especiais

### 🚀 Release v2.2.8 (Padronização da Identidade Visual & Prolongamento Inteligente do Boot HUD)
* **Padronização da Identidade Visual (`app_icon.jpg`)**: Sincronização da logo oficial da marca entre a inicialização WebView (`wwwroot/app_icon.jpg`), ícone nativo da janela WPF (`MainWindow.xaml`) e centro do reator ciano no HUD da tela de loading.
* **Prolongamento Inteligente da Tela de Loading (`DashboardTab.razor`)**: O motor de interface agora assume e prolonga a exibição do HUD Cyberpunk de inicialização até que todas as 3 fases fundamentais de coleta e calibração (`Conectado / Varredura L2`, `Latência dos Radares de Ping` e `IP Público Externo`) estejam completas no `DashboardService`, impedindo a exibição de cards em *"Buscando..."* ou *"Testando..."* para o usuário.
* **Transição Suave e Trava de Sessão Pós-Boot (`_hasCompletedSystemBoot`)**: Finalizada a coleta, o HUD executa uma animação de *fade-out* expansiva revelando o painel totalmente populado. Nas alternâncias posteriores entre guias (*Terminal SSH*, *ICMP Suite*, *Dashboard*), a navegação ocorre de forma 100% instantânea.

### 🎯 Release v2.2.7 (Cálculo de Perda de Rota por Destino Final & Anti-CoPP Efetivo no MTR)
* **Cálculo da Rota Exclusivo pelo Destino Final (`IcmpMenuTab.razor`)**: Em conformidade com a arquitetura de roteamento IP de operadoras e provedores de telecom, o cálculo de **Perda de Rota** e os contadores globais de **Enviados / Recebidos** no MTR Avançado passaram a ser 100% baseados na conectividade com o nó destino da rota (`destHop`). Se não houve perda de pacotes no destino final (ex: `8.8.8.8` respondendo `0.0%`), a rota inteira é classificada como saudável com `0.0% LOSS` e badge verde no card de métricas.
* **Neutralização de Falsos Positivos de Drops Intermediários (CoPP Rate-Limit)**: Quando roteadores intermediários aplicam limitação de taxa de processamento ICMP no *Control Plane* (descartando pacotes ECHO dirigidos a eles ou suprimindo respostas `Time Exceeded`), esses descartes não somam mais perdas na porcentagem da rota nem nos cards gerais, sendo corretamente exibidos nas linhas individuais com a tag **`⚡ CoPP RATE-LIMIT`** (`0.0% (CoPP XX%)`).
* **Relatório MTR Executivo Exportável**: O laudo gerado via botão `Copiar Relatório` foi alinhado ao cálculo final por destino, indicando explicitamente os nós intermediários em rate-limit como `0.0%(CoPP)`.

### 🔗 Release v2.2.6 (Inteligência RF MESH / Repetidores, Zero Falsos Positivos & Laudo Enxuto)
* **Reconhecimento Arquitetural MESH / Multi-AP (`ConnectedMeshOrSiblingNodes`)**: Em redes Wi-Fi empresariais ou residenciais estruturadas em malha (ex: **TP-Link Deco**, **Google Wifi**, **MikroTik Mesh**) ou repetidores sem cabo de rede, os satélites compartilham obrigatoriamente o mesmo SSID, Canal e Frequência do roteador principal para realizar o *Wireless Backhaul* e cobertura unificada. O algoritmo identifica automaticamente antenas que emitem o mesmo `Ssid` nominal da rede conectada, excluindo-as do cálculo de penalidade Co-Canal (`CCI`) e separando ruído de terceiros da cooperação legítima do fabricante.
* **Score de Saúde de Canal Inteligente (`AnalyzeSpectrumAndChannels`)**: O motor passa a calcular a contenção de tempo de ar com base em **ESSIDs concorrentes reais (`distinctSsids.Count`)**. Malhas cooperativas multi-antena operando no mesmo canal não sofrem multas indevidas, exibindo a tag: `🟢 Topologia MESH / Multi-AP (Compartilhamento Legítimo de Canal)`.
* **Modal Interativo Enxuto (`🚨 ABRIR LAUDO DE MELHORIAS (@conn.Ssid)`) & Topologia Multi-AP**: O botão de ação rápida foi otimizado para uma linguagem executiva direta. O laudo apresenta uma tabela de **Topologia MESH cooperativa**, listando o nó principal conectado (`⭐`) e cada satélite detetado (`🔗`) com seu BSSID, sinal (`RSSI`) e status `✔ Cooperação MESH (Backhaul/Extensão)`.

### ⚡ Release v2.2.5 (Triagem Espectral & Auditoria IEEE Priorizada)
* **Card Dedicado de Triagem da Conexão Ativa (`⚡ REDE CONECTADA EM AUDITORIA`)**: Posicionado no topo da aba de espectro passivo, exibe em tempo real o SSID conectado, canal, banda, sinal (`dBm`), qualidade, e contagens exatas de interferência **Co-Canal (`CCI`)** e **Adjacente (`ACI`)** geradas por vizinhos externos.
* **Auditoria IEEE Priorizada (`AuditEngineeringStandards`)**: Ordena as recomendações de boas práticas para que as diretivas exclusivas da rede atualmente conectada (`⭐ REDE CONECTADA`) fiquem sempre em primeiro lugar.
* **Responsividade Inteligente para Notebooks de 14" (`1366x768`)**: Grids flexíveis (`flex: 1; min-height: 0; overflow-y: auto; max-height: none !important;`) nas tabelas de telemetria contínua e canais, eliminando cortes ou rolagem dupla de tela.

### 🖥️ Release v2.2.3 (Nome de Processo Oficial `RezTerm.exe` & Auto-Escala MTR)
* **Processo Nativo `RezTerm.exe` no Gerenciador de Tarefas do Windows**: Compilação alinhada em `SepulnationTerm.csproj` (`<AssemblyName>RezTerm</AssemblyName>`) e extração blindada em `RezTermSetup`, garantindo que o executável oficial em monitoramentos SOC/NOC e no Windows Task Manager se chame **`RezTerm.exe`**.
* **Responsividade no MTR Avançado**: Painel superior multi-linha com auto-escalonamento para o campo de Destino (`min-width: 240px`).

### 📊 Release v2.2.2 (Telemetria Nativa de RAM/GPU & Anti-CoPP Rate-Limit 3 Fases)
* **Telemetria de Hardware Windows API (`GlobalMemoryStatusEx` & GPU Engine WMI)**: Captura exata do consumo de memória RAM do sistema sincronizada ao byte com o Gerenciador de Tarefas do Windows e HotFix universal de carga da GPU (`NVIDIA`, `Intel HD Graphics`, `AMD Radeon`), exibindo `0.0%` em repouso absoluto em vez de `N/A`.
* **Motor Inteligente Anti-CoPP Rate-Limit em 3 Fases (TCP SYN Bypass)**: Conforme as normas **RFC 1812** (Sec 4.3.2.8) e **RFC 4443** (Sec 2.4), roteadores core de telecom e firewalls limitam a taxa de requisições ICMP para proteção da CPU do Plano de Controle (*Control Plane Policing - CoPP*). O RezTerm impede falsos positivos de queda por descarte ICMP aplicando:
  1. **Heurística CoPP de Salto Intermediário vs Destino (`TracerouteService.cs`)**: Se um salto intermediário perde pacotes mas os saltos seguintes e o destino respondem com `0%` de perda, classifica como limitação CoPP (`⚡ CoPP RATE-LIMIT`).
  2. **Poisson Random Jittering & Exponential Backoff Pacing**: Variação estocástica (`±15%` de jitter randômico) nos intervalos dos pacotes e recuo exponencial (`x1.4`) no caso de descarte para contornar *token buckets* de firewalls.
  3. **TCP SYN Bypass (`PingService.cs` & `DashboardService.cs`)**: Se o ICMP for descartado em gateways ou alvos de monitoramento, dispara instantaneamente um handshake **TCP SYN/ACK em portas 80 HTTP ou 443 HTTPS**. Se responder, atesta que a via de dados (*Data Plane*) está 100% online com `Loss = 0%`, emitindo o selo azul neon **`⚡ CoPP BYPASS (TCP)`**.

---

## 📦 7. Instalação & Atualizações CDN Automáticas

O RezTerm possui um assistente bootstrapper nativo (`RezTermSetup.exe`) que garante a instalação limpa, sem dependências externas de administração, diretamente no perfil do técnico (`%LocalAppData%\RezTerm`):
* **Sincronização de Cache de Ícone**: O instalador força a atualização do cache gráfico do Shell do Windows (`SHChangeNotify`) garantindo que o novo ícone Cyberpunk seja exibido imediatamente na barra de tarefas e área de trabalho.
* **Auto-Updater via GitHub CDN**: Ao abrir a ferramenta, o serviço `UpdateService` consulta anonimamente a API pública de lançamentos (`juniorespow/RezTerm-Downloads`). Caso uma nova versão esteja disponível, o analista recebe um alerta no topo da tela podendo baixar e aplicar a atualização em 1 clique sem interromper suas sessões.

---
<div align="center">
<b>RezTerm Network Engineer Toolkit</b> • Engenharia de Redes de Alta Performance • Reginaldo Junior
</div>
