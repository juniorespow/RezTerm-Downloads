# 🌌 REZTERM DESIGN SYSTEM & AP KEY VISUAL API
**Especificação Técnica, Paleta de Cores, Tipografia, DWM Imersivo e Metodologia de Uso para Ecossistemas Cyberpunk SOC/NOC**

<div align="center">

![Theme Dictatorship](https://img.shields.io/badge/Theme-Dark%20Mode%20Dictatorship-0D1117?style=for-the-badge)
![Primary Accent](https://img.shields.io/badge/Primary%20Accent-Cyan%20Neon%20(%2300f0ff)-00f0ff?style=for-the-badge&logoColor=black)
![Secondary Accent](https://img.shields.io/badge/Secondary%20Accent-Emerald%20(%2339ff14)-39ff14?style=for-the-badge&logoColor=black)
![Typography](https://img.shields.io/badge/Typography-Segoe%20UI%20%2B%20Consolas%20Mono-58A6FF?style=for-the-badge)
![Engine](https://img.shields.io/badge/Render%20Engine-WPF%20DWM%20%2B%20Blazor%20Hybrid-5C2D91?style=for-the-badge)

*Documentação arquitetural oficial de identidade visual para desenvolvedores, arquitetos de UI/UX e analistas que mantêm ou criam novos submódulos, sidecars ou aplicações no padrão corporativo da Diretoria Telecom.*

</div>

---

## 🏛️ 1. Filosofia Arquitetural e "Ditadura do Tema Dark"

O **RezTerm** não é uma aplicação corporativa comum; é um instrumento de operação crítica de alta performance para engenheiros de rede, analistas de SOC (*Security Operations Center*) e operadores de NOC (*Network Operations Center*) trabalhando sob estresse em turnos de 24 horas.

Conforme instituído nas **Regras de Ouro e Diretrizes do Projeto RezTerm (`AGENTS.md`)**:
> **Estatuto da Ditadura do Tema Dark & Azul Neon**: Respeite a ditadura do tema Dark (nunca adicione ou sugira opções de tema claro / *Light Mode*). Utilize a cor de destaque Azul Neon (`#00f0ff`) para botões ativos, gráficos, radares e acentos.

### 🧠 Justificativa Neuro-Cognitiva do AP Key Visual:
1. **Fadiga Ocular Zero**: Superfícies escuras profundas absorvem o excesso de brilho em ambientes pouco iluminados (Datacenters, salas de monitoramento SOC/NOC e sobreaviso noturno).
2. **Triagem por Luminescência**: Em vez de blocos de texto monocromáticos, o cérebro humano processa anomalias em microssegundos através de "pílulas neon" (*Glow Badges*). Um salto CoPP em `#00f0ff` ou um alerta RF em `#F85149` é reconhecido instantaneamente na visão periférica.
3. **Imersão de Terminal Nativo**: A transição do host WPF para o Blazor WebView é imperceptível, com bordas milimétricas e sombras de difusão de fótons que remetem a terminais Sci-Fi (*Cyberpunk 2077*, *Blade Runner*, *The Matrix*).

---

## 🎨 2. Catálogo de Tokens CSS (`:root`) e Paleta Criptográfica

Todos os novos componentes e aplicações devem obrigatoriamente consumir os tokens CSS definidos no motor `app.css`. É **proibido o uso de cores *hardcoded*** fora desta especificação.

### 🧱 2.1. Superfícies de Fundo (Background Surface Tiers)
| Token CSS (`:root`) | Hexadecimal | RGBA Equivalente | Aplicação Arquitetural no Sistema |
| :--- | :--- | :--- | :--- |
| **`--bg-dark`** | `#0D1117` | `rgba(13, 17, 23, 1.0)` | **Camada L0 (Fundo Global do App)**: Fundo raiz do `body`, margens do WPF e áreas externas das abas. |
| **`--bg-sidebar`** | `#161B22` | `rgba(22, 27, 34, 1.0)` | **Camada L1 (Barra Lateral e Navegação)**: Fundo do painel lateral esquerdo, cabeçalhos de seções principais. |
| **`--bg-card`** | `#161B22` | `rgba(22, 27, 34, 1.0)` | **Camada L1 (Cards e Painéis)**: Fundo estruturado de cards de métricas, modais (`LicensingModal`) e tabelas. |
| **`--bg-subcard`** | `#0B0E13` | `rgba(11, 14, 19, 1.0)` | **Camada L2 (Sub-Blocos Internos)**: Área interna de cards divisores (ex: blocos *Download/Upload* no Dashboard). |
| **`--bg-console`** | `#0C0F12` | `rgba(12, 15, 18, 1.0)` | **Camada L2 (Terminais e Logs)**: Fundo do `xterm.js`, Hex Dump Raw Preview e saídas de comando `stderr/stdout`. |
| **`--pcap-table-bg`** | `#140808` | `rgba(20, 8, 8, 1.0)` | **Camada L2 Forense**: Fundo especializado de tabelas de pacotes PCAP e dissecadores de tráfego. |
| **`--pcap-sticky-bg`**| `#2A0E0E` | `rgba(42, 14, 14, 1.0)` | **Camada L3 Forense**: Fundo de cabeçalhos e linhas selecionadas em auditorias forenses e Graylog. |

---

### 💡 2.2. Acentos Neon & Luminescência Ativa (Neon Accents & Glow)
| Token CSS (`:root`) | Hexadecimal | Cor Nominal | Uso e Comportamento Visual |
| :--- | :--- | :--- | :--- |
| **`--ul-color` / `Accent`** | `#00f0ff` | **Azul Neon / Ciano** | **Acento Principal (AP Key Visual)**: Botões ativos, abas selecionadas (`sidebar-menu li.active`), selo **`⚡ CoPP BYPASS`**, radar de latência, gráficos de upload e títulos em destaque. |
| **`--dl-color`** | `#39ff14` | **Verde Esmeralda Neon** | **Acento de Download / Saúde**: Gráficos de tráfego de entrada, sinal Wi-Fi ideal (`>-65 dBm`), status `🟢 Topologia MESH`. |
| **`--accent`** | `#4EC9B0` | **Verde Menta / Cobre** | **Acento Técnico de Tipos**: Nomes de classes, badges de status de link L2 (`LLDP/CDP`), títulos de triagem. |
| **`--accent-blue`** | `#58A6FF` | **Azul Aço (.NET)** | **Links e IPv6**: Endereços IPv6, links para WHOIS/IRR, caminhos de arquivo clicáveis. |
| **`--danger`** | `#F85149` | **Vermelho Carmim / Alerta** | **Perda de Pacotes e Ataques**: `Loss > 0%`, detecção de `PADI Rogue / PPPoE`, alarmes de contenção Co-Canal (`CCI > 2`). |
| **`--warning`** | `#D29922` | **Âmbar / Amarelo** | **Atenção Intermediária**: Sinais médios (`-66 a -75 dBm`), canal fora da grade recomendada 1/6/11, avisos de recuo de pacotes. |
| **`--success`** | `#3FB950` | **Verde Conforme** | **Sucesso de Validação**: Chave HMAC-SHA256 válida, porta TCP aberta, DNS resolvido. |

---

### ✒️ 2.3. Tipografia, Legibilidade e Hierarquia Numérica
A tipografia do **RezTerm** divide-se em dois motores estritamente segregados para maximizar a velocidade de leitura técnica:

1. **Interface Geral & UI Clean (`font-family: 'Segoe UI', Tahoma, Geneva, Verdana, sans-serif;`)**:
   * Utilizada em títulos, menus laterais, modais e cards explicativos.
   * **`--text-main` (`#C9D1D9`)**: Cor principal para texto de leitura, garantindo contraste de 10:1 sobre o fundo `#0D1117` sem o ofuscamento do branco puro (`#FFFFFF`).
   * **`--text-muted` (`#8B949E`)**: Cor secundária para legendas, portas secundárias, rótulos de campos e metadados.

2. **Telemetria, Endereçamento e Forense (`font-family: 'Consolas', 'JetBrains Mono', 'Courier New', monospace;`)**:
   * **Obrigatório em**: Endereços IPv4 (`192.168.1.1`), IPv6 (`fe80::...`), MAC Addresses (`00:1A:2B:3C:4D:5E`), ASNs (`AS15169`), Hex Dumps (`4A 50 47 ...`), tabelas do MTR e terminal SSH `xterm.js`.
   * **Por que Monospace?** Garante alinhamento vertical milimétrico em tabelas e painéis de portas sem trepidação visual quando números dinâmicos (`0-9`) mudam a 60 FPS.

---

## ⚡ 3. Aceleração Híbrida Gráfica e Efeitos Fluorescentes

O AP Key Visual não se limita a cores estáticas; ele implementa efeitos dinâmicos de renderização nas camadas nativa (WPF) e web (Blazor):

### 🖥️ 3.1. Imersão Nativa WPF DWM (`DwmSetWindowAttribute`)
Para evitar que a janela do Windows exiba aquela barra de título branca ou cinza padrão (que destrói a imersão Cyberpunk), o **MainWindow.xaml.cs** injeta comandos na API Desktop Window Manager (`DWM` / `Kernel32.dll`):
```csharp
// Força a barra de título do Windows 10/11 a renderizar em Dark Mode Imersivo
int DWMWA_USE_IMMERSIVE_DARK_MODE = 20;
int useImmersiveDarkMode = 1;
DwmSetWindowAttribute(windowHandle, DWMWA_USE_IMMERSIVE_DARK_MODE, ref useImmersiveDarkMode, sizeof(int));
```

### 🔮 3.2. Sombras Neon e Difusão Fóton (*Glow Badges*)
Botões ativos e cards de alerta utilizam sombras projetadas em RGBA sincronizadas com a cor da borda, simulando tubos de gás neon:
```css
/* Exemplo de Botão / Badge Ativo em Azul Neon */
.neon-badge-active {
    background-color: rgba(0, 240, 255, 0.12);
    border: 1px solid var(--ul-color); /* #00f0ff */
    color: var(--ul-color);
    font-weight: 600;
    box-shadow: 0 0 14px rgba(0, 240, 255, 0.45);
    text-shadow: 0 0 5px rgba(0, 240, 255, 0.6);
    transition: all 0.25s cubic-bezier(0.16, 1, 0.3, 1);
}

.neon-badge-active:hover {
    background-color: var(--ul-color);
    color: #000000; /* Texto preto sobre fundo ciano aceso para legibilidade máxima */
    box-shadow: 0 0 22px rgba(0, 240, 255, 0.85);
}
```

### 🌟 3.3. Motores Canvas WebGL / 60 FPS (`pcap-cyberpunk-map.js`)
Nos módulos **Live TCP/UDP Watcher** e **Leitor PCAP Forense**, mapas e radares utilizam aceleração de hardware via WebGL / HTML5 Canvas. As conexões ativas disparam partículas esmaecendo (*Breathing Neon Particles*) com suporte a bloqueio nativo de rolagem da janela (`{ passive: false }`).

---

## 🛠️ 4. Metodologia de Integração para Outros Projetos e Sidecars

Se você estiver desenvolvendo um novo submódulo, microsserviço visual, ferramenta WPF/WinForms auxiliar ou componente Blazor/React que se integre ao ecossistema **SepulnationTerm / RezTerm**, siga este **Checklist Arquitetural de 5 Passos**:

### Passo 1: Estrutura CSS Base Requerida (`index.css` / `app.css`)
Copie o bloco `:root` exato desta documentação e defina o *Box Model* universal sem vazamento de barra de rolagem externa:
```css
*, *::before, *::after {
    box-sizing: border-box;
}

html, body, .app-container {
    margin: 0;
    padding: 0;
    width: 100vw;
    height: 100vh;
    background-color: var(--bg-dark);
    color: var(--text-main);
    overflow: hidden; /* Proíbe scroll global da janela do navegador/WebView2 */
}
```

### Passo 2: O Padrão de Flexbox Auto-Escalável (`Flexbox & min-height: 0`)
Para que o layout **nunca corte ou empurre elementos para fora da tela** em notebooks de 14" (`1366x768`) ou telas divididas (`max-height: 860px`), todos os painéis e tabelas devem ser estruturados como colunas flexíveis onde o grid ou tabela assume `flex: 1; min-height: 0; overflow-y: auto;`:
```css
/* Container Pai da Aba / Módulo */
.module-view {
    display: flex;
    flex-direction: column;
    height: 100%;
    width: 100%;
    padding: 15px;
    gap: 15px;
    overflow: hidden;
}

/* Painel de Controles Superior (Fixo no Topo) */
.controls-header {
    flex: 0 0 auto;
    background-color: var(--bg-card);
    border: 1px solid var(--border);
    padding: 12px 18px;
    border-radius: 6px;
    display: flex;
    flex-wrap: wrap;
    gap: 12px;
    align-items: center;
}

/* Painel de Tabela / Telemetria (Ocupa Todo o Resto da Tela) */
.telemetry-grid-container {
    flex: 1 1 auto;
    min-height: 0; /* SEGREDO DE ENGENHARIA: Impede que o container exploda além da tela */
    overflow-y: auto; /* A rolagem acontece APENAS dentro da tabela */
    background-color: var(--bg-card);
    border: 1px solid var(--border);
    border-radius: 6px;
}
```

### Passo 3: Auto-Escala Dinâmica para Notebooks de 14" (`@media scaling`)
Injete as Media Queries responsivas oficiais para compactação adaptativa da tipografia e espaçamentos quando o software rodar em notebooks em campo:
```css
@media (max-height: 860px), (max-width: 1450px) {
    .controls-header {
        padding: 8px 12px;
        gap: 8px;
    }
    .telemetry-grid-container table th,
    .telemetry-grid-container table td {
        padding: 6px 10px !important;
        font-size: 0.85rem !important;
    }
    .neon-badge-active {
        padding: 3px 8px !important;
        font-size: 0.78rem !important;
    }
}
```

### Passo 4: Componente Padrão de Tabela Cyberpunk (Snippet Blazor/HTML)
Ao renderizar tabelas de IP, MTR, Wi-Fi ou pacotes PCAP, utilize este cabeçalho escurecido com bordas em `#30363D` e hover em `#1b222c`:
```html
<table class="cyber-table">
    <thead>
        <tr>
            <th>IP DESTINO / HOST</th>
            <th>STATUS COPP</th>
            <th>PING (MS)</th>
            <th>PERDA (%)</th>
        </tr>
    </thead>
    <tbody>
        <tr>
            <td class="mono-text">8.8.8.8 (dns.google)</td>
            <td><span class="neon-pill-cyan">⚡ CoPP BYPASS (TCP)</span></td>
            <td class="mono-text">11.4 ms</td>
            <td class="status-ok">0.0%</td>
        </tr>
    </tbody>
</table>
```
```css
.cyber-table {
    width: 100%;
    border-collapse: collapse;
}

.cyber-table thead th {
    background-color: var(--table-header-bg);
    color: var(--accent);
    text-align: left;
    padding: 10px 14px;
    font-size: 0.82rem;
    border-bottom: 2px solid var(--border);
    position: sticky;
    top: 0;
    z-index: 5;
}

.cyber-table tbody tr {
    border-bottom: 1px solid rgba(255, 255, 255, 0.03);
    transition: background-color 0.15s ease;
}

.cyber-table tbody tr:hover {
    background-color: rgba(0, 240, 255, 0.05);
}

.cyber-table tbody td {
    padding: 9px 14px;
    font-size: 0.9rem;
    color: var(--text-main);
}

.mono-text {
    font-family: 'Consolas', 'JetBrains Mono', monospace;
    color: #FFFFFF;
}
```

### Passo 5: Verificação de Conformidade Visual (QA SOC/NOC)
Antes de enviar seu Pull Request ou publicar sua ferramenta no repositório, verifique o checklist abaixo:
- [ ] **Zero Branco Puro em Fundo**: Não há nenhum card, modal ou div com `background: #FFFFFF;` ou `color: #000000;` sobre fundo claro.
- [ ] **Acento Principal em `#00f0ff`**: O botão principal da tela (*Ação/Triagem/Ativar*) usa a luminescência Ciano Neon do projeto.
- [ ] **IPs e Números em Monospace**: Todos os campos numéricos, portas, MACs e latências estão com fonte `Consolas` / `monospace`.
- [ ] **Rolagem Interna Isolada**: Ao dimensionar a janela para `1366x768`, a tela inteira cabe no monitor sem criar barra de rolagem lateral/vertical na borda da janela principal do Windows.

---
<div align="center">
<b>RezTerm SOC/NOC Suite • AP Key Visual & Design System API</b><br>
<i>Diretoria Telecom • Reginaldo Junior (Razon) • Todos os Direitos Reservados</i>
</div>
