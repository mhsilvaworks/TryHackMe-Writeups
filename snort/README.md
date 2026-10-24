# Snort 101: Cheatsheet em Português

> Baseado no cheatsheet da sala **Snort** do TryHackMe (https://tryhackme.com/room/snort).
> Comandos, flags e opções de regra ficam em inglês, porque é assim que você os digita. Só as explicações foram traduzidas.

---

## Sobre este material

| Item | Detalhe |
|---|---|
| **Origem** | Cheatsheet em PDF (2 páginas) da sala *Snort* do TryHackMe |
| **Página 1** | "Snort 101": comandos organizados por modo de uso |
| **Página 2** | "Snort Rule Breakdown": anatomia de uma regra, com exemplo e tabela de campos |
| **Versão do Snort** | Sintaxe do **Snort 2.x** (usa `snort.conf` e flags como `-A cmg`) |
| **Público** | Iniciantes em blue team, SOC e análise de tráfego |

### O que é o Snort?

O Snort é um sistema open source de **detecção e prevenção de intrusão de rede** (NIDS/NIPS). Ele inspeciona pacotes e os compara com **regras**. Quando um pacote casa com uma regra, o Snort executa uma ação, como gerar um alerta, registrar o pacote ou bloquear o tráfego. Foi criado por Martin Roesch e hoje é mantido pela Cisco (Talos).

### Os 4 modos de operação

| Modo | Para que serve | Exemplo mínimo |
|---|---|---|
| **Sniffer Mode** | Ler pacotes e mostrá-los na tela | `snort -v` |
| **Logger Mode** | Gravar pacotes em disco | `snort -v -l /caminho` |
| **IDS/IPS Mode** | Aplicar regras e gerar alertas (ou bloquear) | `snort -c /etc/snort/snort.conf` |
| **PCAP Processing** | Analisar arquivos `.pcap` já capturados | `snort -c ... -r file.pcap` |

### Atenção: Snort 2 vs Snort 3

Este cheatsheet usa a sintaxe do **Snort 2**. O Snort 3 tem configuração em Lua (`snort.lua`) e algumas flags diferentes. Se um comando daqui não funcionar na sua máquina, confira a versão com `snort -V`.

---

## 1. Global Commands

| Objetivo | Comando |
|---|---|
| Exibir a versão | `snort -V` ou `snort -version` |
| Não exibir o banner de versão | `snort -q` |
| Usar uma interface específica | `snort -i eth0` |

---

## 2. Sniffer Mode

| Objetivo | Comando |
|---|---|
| Modo verbose | `snort -v` |
| Exibir cabeçalhos da camada de enlace (link-layer) | `snort -e` |
| Exibir o payload (dados) do pacote | `snort -d` |
| Exibir os detalhes completos do pacote em HEX | `snort -X` |
| Várias flags juntas: exibe todos os detalhes do pacote | `snort -eX` |
| Capturar "N" pacotes | `snort -v -n 10` |

**Resumo das flags:**

| Flag | Mostra |
|---|---|
| `-v` | Cabeçalhos TCP/IP básicos |
| `-e` | Cabeçalhos da camada de enlace (Ethernet, MACs) |
| `-d` | Dados da camada de aplicação (payload) |
| `-X` | Pacote completo em hexadecimal e ASCII |

---

## 3. Logger Mode

| Objetivo | Comando |
|---|---|
| Caminho padrão dos logs | `/var/log/snort` |
| Usar um caminho de log alternativo | `snort -v -l /home/username/Desktop` |
| Gravar log em formato ASCII | `snort -v -K ASCII` |
| Ler arquivos de log do Snort | `snort -v -r snort.log` |
| Ler "N" pacotes | `snort -v -r snort.log -n 10` |

### Filtros BPF (Berkeley Packet Filter)

O filtro vem **no final** do comando e reduz o que será lido:

```bash
snort -v -r snort.log tcp
snort -v -r snort.log 'udp and port 53'
```

Outros exemplos úteis de BPF: `host 10.0.0.5`, `port 80`, `icmp`, `tcp and not port 22`.

---

## 4. IDS/IPS Mode

| Objetivo | Comando |
|---|---|
| Usar arquivo de configuração | `snort -c /etc/snort/snort.conf` |
| Testar a instância e o arquivo de configuração | `snort -c /etc/snort/snort.conf -T` |
| Desabilitar o logging | `snort -c /etc/snort/snort.conf -N` |
| Rodar o Snort em segundo plano | `snort -c /etc/snort/snort.conf -D` |
| Usar regras sem arquivo de configuração | `snort -c /etc/snort/rules/local.rules -v -A console` |

### Modos de alerta (`-A`)

| Modo | Comando | O que faz |
|---|---|---|
| **1: Sem saída** | `snort -c /etc/snort/snort.conf -v -A none` | Não gera alertas |
| **2: Console 1** | `snort -c /etc/snort/snort.conf -v -A console` | Alerta resumido (uma linha) na tela |
| **2: Console 2** | `snort -c /etc/snort/snort.conf -v -A cmg` | Alerta na tela com cabeçalho e payload em hex e texto |
| **3: Arquivo 1** | `snort -c /etc/snort/snort.conf -v -A fast` | Alerta resumido gravado em arquivo |
| **3: Arquivo 2** | `snort -c /etc/snort/snort.conf -v -A full` | Alerta completo gravado em arquivo |

> **Dica:** antes de rodar em produção, valide sempre com `-T`. Ele aponta erros de sintaxe nas regras e na configuração sem iniciar a captura.

---

## 5. PCAP Processing

| Objetivo | Comando |
|---|---|
| Processar um único arquivo pcap | `snort -c /etc/snort/snort.conf -q -r file.pcap -A console` |
| Processar vários arquivos pcap | `snort -c /etc/snort/snort.conf -q --pcap-list="file1.pcap file2.pcap" -A console` |
| Processar todos os pcaps de uma pasta | `snort -c /etc/snort/snort.conf -q --pcap-dir=/home/pcap-folder -A console` |
| Mostrar o nome do pcap processado | `snort -c /etc/snort/snort.conf -q --pcap-list="file1.pcap file2.pcap" -A console --pcap-show` |

---

## 6. Snort Rule Breakdown

Uma regra do Snort tem **duas partes lógicas**:

| Parte | Conteúdo |
|---|---|
| **Rule Header** | Informações de rede: action (ação), protocol (protocolo), IP e porta de origem e destino, direção do tráfego |
| **Rule Options** | Detalhes da investigação do pacote: mensagem, referência, flow e conteúdo |

### Estrutura geral

```
ACTION  PROTOCOL  SRC_IP  SRC_PORT  DIRECTION  DST_IP  DST_PORT  ( OPTIONS )
└──────────────────── Rule Header ───────────────────────┘  └─ Rule Options ─┘
```

### Regra de exemplo

Regra de alerta para detectar uma possível "Directory Traversal Attempt" (tentativa de percorrer diretórios):

```
alert tcp $EXTERNAL_NET any -> $HOME_NET $HTTP_PORTS (
msg:"Directory Traversal Attempt!";
flow:established;
nocase; content:"HTTP"; fast_pattern; content:"| 2E 2E 2F|"; content:"/..";
session:all;
reference:CVE,XXX;
sid:100001; rev:1;)
```

**Lendo a regra linha a linha:**

| Trecho | Significado |
|---|---|
| `alert` | Gere um alerta quando houver casamento |
| `tcp` | Só analise tráfego TCP |
| `$EXTERNAL_NET any` | Origem: qualquer IP de fora da rede, qualquer porta |
| `->` | Direção: da origem para o destino |
| `$HOME_NET $HTTP_PORTS` | Destino: sua rede, nas portas HTTP |
| `msg:"..."` | Texto que aparece no alerta |
| `flow:established` | Só em conexões TCP já estabelecidas |
| `content:"\| 2E 2E 2F\|"` | Procura os bytes `2E 2E 2F`, que são `../` em hexadecimal |
| `content:"/.."` | Procura o texto `/..` no payload |
| `nocase` | Ignora maiúsculas e minúsculas |
| `fast_pattern` | Usa esse `content` como filtro rápido inicial |
| `session:all` | Extrai os dados da sessão TCP |
| `reference:CVE,XXX` | Referência externa (aqui, um espaço reservado) |
| `sid:100001; rev:1` | ID único da regra e número da revisão |

### Referência dos campos

#### Rule Header

| Campo | Keyword / exemplo | Descrição |
|---|---|---|
| Action | `alert` | Ação: diz ao Snort o que fazer quando a regra casar |
| Protocol | `tcp` | Protocolo analisado. Suportados: TCP, UDP, ICMP, IP |
| Source IP | `$EXTERNAL_NET` | Endereços IP de origem |
| Source Port | `any` | Portas de origem |
| Direction | `->` | Operador de direção. Indica a orientação do tráfego |
| Destination IP | `$HOME_NET` | Endereços IP de destino |
| Destination Port | `$HTTP_PORTS` | Portas de destino |

#### Rule Options

| Grupo | Campo | Keyword | Descrição |
|---|---|---|---|
| **General** | Message | `msg` | Mensagem exibida quando a regra casa |
| | Reference | `reference` | Informação adicional ou referência sobre a regra |
| | Rule id | `sid` | Número único da regra |
| | Revision info | `rev` | Informação de revisão da regra |
| **Non-Payload Detection** | Flow | `flow` | Direção do fluxo TCP |
| **Payload Detection** | Nocase | `nocase` | Desativa a diferenciação de maiúsculas/minúsculas para melhorar o casamento do content |
| | Content | `content` | Filtra os dados do payload e procura um casamento exato |
| | Fast-pattern | `fast-pattern` | Prioriza a busca de conteúdo para acelerar a busca no payload. Obrigatório ao usar várias opções `content` |
| **Post-Detection** | Session | `session` | Extrai dados do usuário de sessões TCP |

---

## Informações extras (fora do PDF original)

### Outras ações de regra comuns (Snort 2)

| Action | O que faz |
|---|---|
| `alert` | Gera alerta e registra o pacote |
| `log` | Só registra o pacote, sem alerta |
| `pass` | Ignora o pacote |
| `drop` | Bloqueia e registra (exige modo inline/IPS) |
| `reject` | Bloqueia e envia reset TCP ou ICMP unreachable |
| `sdrop` | Bloqueia sem registrar |

### Operadores de direção

| Operador | Significado |
|---|---|
| `->` | Origem para destino |
| `<>` | Bidirecional |

### Sintaxe de IPs e portas

| Sintaxe | Exemplo | Significado |
|---|---|---|
| Qualquer | `any` | Qualquer IP ou porta |
| Negação | `!192.168.1.0/24` | Tudo, exceto essa rede |
| Lista | `[80,443,8080]` | Várias portas |
| Intervalo | `1:1024` | Da porta 1 à 1024 |
| CIDR | `10.0.0.0/8` | Uma sub-rede inteira |

### Variáveis comuns (definidas no `snort.conf`)

`$HOME_NET`, `$EXTERNAL_NET`, `$HTTP_PORTS`, `$SSH_PORTS`, `$DNS_SERVERS`, entre outras. Se a variável não estiver definida, o Snort falha ao carregar a regra.

### Fluxo de trabalho sugerido

1. Valide a configuração: `snort -c /etc/snort/snort.conf -T`
2. Escreva a regra em `/etc/snort/rules/local.rules` com um `sid` acima de **1000000**, faixa reservada para regras locais.
3. Teste a regra contra um pcap: `snort -c /etc/snort/snort.conf -q -r file.pcap -A console`
4. Refine a regra e incremente o `rev` a cada mudança.
5. Só então rode em tempo real (`-i eth0`) ou em segundo plano (`-D`).

### Erros comuns de iniciante

| Erro | Causa provável |
|---|---|
| Regra não é carregada | Falta `;` ao final de uma opção, ou parêntese não fechado |
| Nenhum alerta aparece | Faltou `-A console` (ou `-A fast`), ou a direção `->` está invertida |
| `content` não casa | Diferença de maiúsculas/minúsculas (use `nocase`) ou bytes em hex mal escritos |
| Erro de variável | `$HOME_NET` ou outra variável não definida no `snort.conf` |
| `sid` duplicado | Duas regras com o mesmo ID |

### Termos úteis

| Termo | Significado |
|---|---|
| **IDS** | Intrusion Detection System: detecta e alerta |
| **IPS** | Intrusion Prevention System: detecta e bloqueia |
| **Payload** | Dados transportados pelo pacote, sem os cabeçalhos |
| **PCAP** | Arquivo com captura de tráfego de rede |
| **BPF** | Linguagem de filtro de pacotes |
| **SID** | Signature ID, identificador único da regra |
| **CVE** | Identificador público de vulnerabilidade conhecida |

---

*Material de estudo. Use apenas em ambientes que você tem autorização para monitorar.*  