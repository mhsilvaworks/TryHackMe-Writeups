# 🦈 Wireshark: Operações de Pacotes

**Plataforma:** TryHackMe  
**Categoria:** Network Forensics / Traffic Analysis  
**Ferramentas Utilizadas:** Wireshark  

---

## 1. Objetivo do Laboratório
Dominar a sintaxe dos filtros de exibição do Wireshark para isolar pacotes específicos e extrair estatísticas de tráfego. O foco foi usar operadores lógicos (AND, OR, NOT) e expressões regulares para resolver investigações diretas, em vez de analisar pacotes um por um manualmente.

## 2. Fundamentos de Filtragem
Existem dois tipos principais de filtros:
* **Filtros de Captura:** Usados *antes* de iniciar a captura para salvar apenas o tráfego desejado no arquivo bruto (usam sintaxe mais rígida).
* **Filtros de Exibição (Display Filters):** Usados para investigar e reduzir o que vemos na tela em tempo real, sem apagar o arquivo original. É a principal ferramenta de investigação.

## 3. Filtros e Consultas (Cheat Sheet)
Durante a análise, além dos filtros básicos, construí e utilizei os seguintes comandos para isolar exatamente o que eu precisava:

* **Isolar requisições web:** `http.request`
* **Buscar tentativas de login (texto claro):** `http.request.method == "POST"`
* **Isolar consultas DNS do tipo A (sem respostas e sem LLMNR):** `dns.qry.type == 1 and dns.flags.response == 0 and !llmnr`
* **Buscar servidores Microsoft IIS em portas não-padrão:** `http.server contains "Microsoft-IIS" and !(tcp.srcport == 80)`
* **Filtrar por uma versão específica de servidor HTTP:** `http.server contains "IIS" and http.server contains "7.5"`
* **Usar Regex para pacotes com TTL terminando em número par:** `string(ip.ttl) matches "[02468]$"`
* **Identificar pacotes com Checksum TCP inválido:** `tcp.checksum.status == 2`

> **Dica de Ouro:** Evite usar o operador antigo `!= valor`. Prefira sempre envolver a expressão numa negação lógica, por exemplo: `!(ip.src == 10.10.10.222)`.

## 4. Análise e Descobertas
Nesta máquina, o foco foi estatística e precisão na filtragem. Algumas das principais descobertas:

1. **O perigo dos falsos positivos no DNS:** Ao tentar contar consultas DNS, notei que o Wireshark mistura requisições, respostas e protocolos similares (como o LLMNR). Tive que usar operadores de negação (`!llmnr`) para chegar ao número real.
2. **Mapeamento Rápido:** Usando o menu *Statistics > IPv4 Statistics*, foi muito mais rápido identificar que o IP `10.100.1.33` era o destino mais acessado da rede do que tentar adivinhar rolando a tela. 
3. **Regex no Wireshark salva tempo:** A possibilidade de converter campos em texto (`string(ip.ttl)`) e aplicar Regex foi essencial para encontrar comportamentos específicos direto no Wireshark, sem precisar exportar os dados para Python ou terminal.

*(Adicionar na pasta `assets` prints da barra inferior do Wireshark mostrando o número exato no campo "Displayed" após aplicar os filtros mais complexos)*

## 5. Extração de Artefatos
Neste laboratório específico, o objetivo não foi extrair arquivos (como executáveis via `Export Objects`), mas sim extrair **métricas e contagens**. 
* **Dados mapeados:** Levantamento quantitativo de servidores web (IIS versão 7.5) operando na rede e o agrupamento de requisições de vários subdomínios vinculados à Microsoft/MSN.
* **Protocolos mais analisados:** DNS, HTTP e os cabeçalhos de controle TCP e IP.

## 6. Mitigação e Defesa
Para melhorar a segurança e dificultar a análise do nosso tráfego por terceiros:
* **Desativar protocolos barulhentos:** Protocolos como o LLMNR costumam gerar muito tráfego em redes Windows e podem ser usados para ataques de envenenamento (Poisoning/Spoofing). Devem ser desativados via GPO.
* **Criptografia Padrão:** O fato de conseguirmos ler a versão exata do servidor IIS em texto claro reforça a necessidade de usar HTTPS/TLS para mascarar cabeçalhos HTTP e impedir vazamento de dados.
* **Monitoramento e Alertas:** Configurar o SIEM para alertar sobre volumes anômalos de consultas DNS ou tráfego HTTP em portas não convencionais, o que pode indicar exfiltração de dados ou Command and Control (C2).
