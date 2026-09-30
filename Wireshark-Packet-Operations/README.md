# 🦈 Wireshark: Operações de Pacotes

**Plataforma:** TryHackMe  
**Categoria:** Network Forensics / Traffic Analysis  
**Ferramentas Utilizadas:** Wireshark, NetworkMiner (se aplicável)

---

## 1. Objetivo do Laboratório
Analisar capturas de tráfego de rede (arquivos `.pcap`) para investigar incidentes, entender o fluxo de pacotes e extrair informações sensíveis (como credenciais, arquivos transferidos ou comunicação de malware).

## 2. Filtros e Consultas (Cheat Sheet)
Durante a análise, construí e utilizei os seguintes filtros no Wireshark para isolar o tráfego relevante:

* **Isolar requisições web:** `http.request`
* **Buscar tentativas de login:** `http.request.method == "POST"`
* **Analisar tráfego FTP/Telnet (texto claro):** `tcp.port == 21 or tcp.port == 23`
* **Filtrar por IP específico:** `ip.addr == 192.168.X.X`

*(Adicione outros filtros interessantes que você aprender na sala)*

## 3. Análise e Descobertas
*Explique aqui o que você encontrou na captura de pacotes.*

**Exemplo de Investigação:**
1. Ao filtrar por tráfego HTTP, notei um POST para uma página de login.
2. Seguindo o fluxo TCP (`Follow > TCP Stream`), foi possível capturar a requisição completa.
3. Como a conexão não usava HTTPS (sem criptografia TLS), as credenciais estavam expostas em texto claro.

*(Coloque na pasta `assets` prints da tela do Wireshark mostrando o TCP Stream e exiba as imagens aqui)*

## 4. Extração de Artefatos
*Se a sala pedir para você extrair arquivos de dentro do tráfego (File > Export Objects).*
* Descreva quais arquivos foram recuperados (ex: um executável suspeito, uma imagem, um arquivo de configuração).
* Qual protocolo foi usado na transferência (HTTP, SMB, FTP).

## 5. Mitigação e Defesa
* Como prevenir que essas informações vazem no mundo real? (Ex: Forçar o uso de TLS/HTTPS, desativar protocolos legados como Telnet, usar VPNs para comunicação interna).
    