# 🎣 TryHackMe: Phishing Analysis

**Plataforma:** TryHackMe  
**Categoria:** Cybersecurity / Phishing Analysis / SOC  
**Objetivo:** Aprender a identificar, analisar e prevenir ataques de phishing por meio da investigação de e-mails suspeitos, análise de indicadores e uso de ferramentas de segurança.

---

## 📌 Sobre o módulo

Neste módulo, estudei como funciona o phishing e como esse tipo de ataque pode ser utilizado para enganar usuários, roubar informações e comprometer sistemas.

Durante as salas, o foco foi entender como analisar e-mails suspeitos, identificar sinais de fraude, verificar informações do remetente, investigar links e anexos e conhecer mecanismos utilizados para proteger a comunicação por e-mail.

O módulo também apresenta situações práticas nas quais é necessário utilizar os conhecimentos adquiridos para investigar mensagens suspeitas e compreender como uma equipe de segurança pode responder a esse tipo de incidente.

## 🧠 Salas estudadas

### 1. Phishing Analysis Fundamentals

**Objetivo:** Entender os fundamentos do phishing e aprender a reconhecer características suspeitas em e-mails.

Nesta sala, o foco é compreender como os e-mails eles são estruturados e quais são as informações podem ajudar durante uma investigação. Um e-mail pode parecer legítimo visualmente, mas ele pode ter inconsistências em seus cabeçalhos, remetente, conteúdo ou links.

Principais conceitos:
- Estrutura e funcionamento de e-mails.
- Análise de cabeçalhos e informações do remetente.
- Identificação de mensagens fraudulentas e técnicas de engenharia social.
- Reconhecimento de erros de escrita, mensagens genéricas e tentativas de imitar empresas conhecidas.
- Identificação de links suspeitos e anexos potencialmente maliciosos.
- Conceito de Business Email Compromise (BEC).

**O que aprendi:**  
Aprendi que não é suficiente analisar apenas o texto que aparece na mensagem. É importante verificar outras informações do e-mail e procurar inconsistências que possam indicar uma tentativa de fraude.

**Minha experiência na sala:**  
[Adicione aqui o que você achou mais interessante, uma questão que resolveu ou alguma dificuldade que encontrou.]

---

### 2. Phishing Emails in Action

**Objetivo:** Observar como ataques de phishing são construídos e quais estratégias são utilizadas para enganar as vítimas.

A sala apresenta exemplos de e-mails fraudulentos que tentam imitar comunicações legítimas. A análise permite observar como os atacantes utilizam marcas conhecidas, mensagens convincentes e elementos visuais para aumentar a credibilidade do golpe.

Principais conceitos:
- Uso de marcas e serviços conhecidos para criar mensagens falsas.
- Falsificação ou manipulação de informações do remetente.
- Utilização de links encurtados ou disfarçados.
- Análise do conteúdo HTML de e-mails.
- Uso de elementos de rastreamento, como pixels de rastreamento.
- Tentativas de roubo de credenciais e manipulação de anexos.

**O que aprendi:**  
Entendi melhor como um e-mail malicioso pode ser construído para parecer verdadeiro. Também percebi a importância de conferir os links e o contexto da mensagem antes de confiar no conteúdo recebido.

**Minha experiência na sala:**  
[Descreva um exemplo analisado e o sinal que ajudou a identificar a tentativa de phishing.]

---

### 3. Phishing Analysis Tools

**Objetivo:** Conhecer ferramentas utilizadas para auxiliar na investigação de e-mails suspeitos.

Nesta sala, o foco é utilizar recursos de análise para coletar informações, examinar indicadores e compreender melhor o comportamento de mensagens potencialmente maliciosas.

Principais conceitos e ferramentas:
- Análise de cabeçalhos e conteúdo de e-mails.
- Coleta de indicadores relevantes para a investigação.
- Verificação da reputação de endereços IP e URLs.
- Uso de ambientes de análise de malware (*sandbox*).
- Utilização do PhishTool como apoio à investigação.
- Organização das evidências encontradas durante a análise.

**O que aprendi:**  
Aprendi que as ferramentas de análise ajudam a reunir evidências e facilitam a investigação. Entretanto, os resultados precisam ser interpretados em conjunto com o contexto da mensagem, pois um único indicador nem sempre é suficiente para confirmar que um e-mail é malicioso.

**Minha experiência na sala:**  
[Informe quais ferramentas você utilizou, o que conseguiu identificar e qual foi a parte mais difícil.]

---

### 4. Phishing Prevention

**Objetivo:** Compreender mecanismos que ajudam a prevenir ataques de phishing e a reduzir a falsificação de e-mails.

Além de identificar mensagens suspeitas, é importante conhecer as tecnologias utilizadas para autenticar e proteger a comunicação por e-mail.

Principais conceitos:
- **SPF (Sender Policy Framework):** ajuda a verificar se um servidor está autorizado a enviar e-mails em nome de um domínio.
- **DKIM (DomainKeys Identified Mail):** utiliza assinaturas digitais para verificar a integridade de determinadas partes da mensagem e sua associação com o domínio.
- **DMARC (Domain-based Message Authentication, Reporting and Conformance):** define políticas e relatórios relacionados à autenticação de e-mails, utilizando SPF e DKIM.
- **S/MIME:** permite utilizar certificados digitais para assinatura e criptografia de mensagens compatíveis.
- Análise de respostas SMTP.
- Inspeção de mensagens e anexos suspeitos.

**O que aprendi:**  
Entendi que a prevenção depende de diferentes mecanismos de segurança. A autenticação de e-mails ajuda a dificultar determinados tipos de falsificação, enquanto a análise das mensagens e a conscientização dos usuários continuam sendo importantes.

**Minha experiência na sala:**  
[Adicione o conceito que você teve mais dificuldade para entender ou um exemplo que ajudou a fixar o conteúdo.]

---

### 5. The Greenholt Phish

**Objetivo:** Aplicar os conhecimentos de análise de phishing em um desafio prático.

Esta sala propõe a investigação de um e-mail suspeito, exigindo atenção aos detalhes e análise das informações disponíveis na mensagem.

Durante uma investigação desse tipo, é importante observar:
- Identidade e endereço do remetente.
- Informações presentes nos cabeçalhos.
- Conteúdo e contexto da mensagem.
- Links e possíveis destinos suspeitos.
- Anexos e outros indicadores relevantes.

**O que aprendi:**  
O principal aprendizado esperado é colocar em prática os conceitos estudados anteriormente, analisando as evidências antes de chegar a uma conclusão.

**Minha experiência na sala:**  
[Registre como você investigou o e-mail, quais evidências encontrou e como chegou às respostas do desafio.]

---

### 6. Snapped Phish-ing Line

**Objetivo:** Investigar uma sequência de e-mails suspeitos e identificar possíveis relações entre as mensagens.

Diferentemente de uma análise isolada, investigar várias mensagens permite procurar padrões que possam indicar uma campanha de phishing.

Pontos importantes:
- Comparação entre diferentes e-mails.
- Identificação de semelhanças no conteúdo e nos remetentes.
- Análise de URLs e outros indicadores.
- Identificação de padrões de ataque.
- Organização das evidências para compreender a possível campanha.

**O que aprendi:**  
Entendi a importância de comparar os indicadores encontrados em diferentes mensagens. Quando várias evidências apontam para padrões semelhantes, elas podem ajudar a compreender melhor o funcionamento de uma campanha de phishing.

**Minha experiência na sala:**  
[Descreva os padrões que você identificou, as dificuldades encontradas e o que utilizou para resolver o desafio.]

---

### 7. Topic Rewind Recap

**Objetivo:** Revisar e reforçar os conhecimentos apresentados durante o módulo.

Esta etapa funciona como uma revisão dos conceitos estudados, ajudando a consolidar o entendimento sobre análise de e-mails, identificação de indicadores suspeitos, ferramentas de investigação e mecanismos de prevenção.

Principais assuntos para revisar:
- Estrutura e cabeçalhos de e-mails.
- Técnicas de engenharia social.
- Análise de links e anexos.
- Ferramentas de investigação.
- Autenticação e proteção de e-mails.
- Identificação de sinais de phishing.

**O que aprendi:**  
A revisão ajuda a conectar os diferentes assuntos do módulo e a perceber como cada etapa contribui para uma análise mais completa de um possível ataque.

**Minha experiência na sala:**  
[Registre os conceitos que você conseguiu revisar e os assuntos que ainda precisa estudar melhor.]

---

### 8. Phishing Unfolding

**Objetivo:** Aplicar conhecimentos de investigação em um cenário de simulação relacionado a um incidente de phishing.

Esta atividade apresenta uma situação investigativa mais próxima do contexto de uma equipe de segurança. O objetivo é acompanhar um incidente em desenvolvimento e analisar as informações disponíveis para compreender o que está acontecendo.

Em uma investigação desse tipo, algumas atividades importantes são:
- Analisar alertas e informações disponíveis.
- Correlacionar evidências de diferentes fontes.
- Investigar indicadores relacionados ao possível ataque.
- Documentar as descobertas.
- Avaliar a necessidade de encaminhar ou escalar o incidente.

**O que aprendi:**  
Compreendi a importância de analisar os eventos em conjunto, manter as evidências organizadas e documentar as conclusões durante uma investigação. Esse tipo de atividade também ajuda a entender como os conhecimentos de análise de phishing podem ser aplicados em um contexto de SOC (*Security Operations Center*).

**Minha experiência na sala:**  
[Descreva como você conduziu a investigação, quais evidências foram importantes e como interpretou os alertas apresentados.]

---

## 🛠️ Principais conhecimentos desenvolvidos

Ao longo do módulo, os principais assuntos estudados foram:

- Identificação de características comuns em ataques de phishing.
- Análise de cabeçalhos e conteúdo de e-mails.
- Investigação de links, endereços IP e anexos suspeitos.
- Utilização de ferramentas de apoio à análise.
- Compreensão de mecanismos de autenticação de e-mails.
- Identificação de padrões em mensagens fraudulentas.
- Organização de evidências e documentação de investigações.
- Aplicação de conhecimentos em desafios e cenários simulados.

## 🎯 Conclusão

O módulo contribuiu para ampliar meu entendimento sobre phishing e sobre os cuidados necessários durante a análise de e-mails suspeitos.

Um dos principais pontos que levo desse estudo é a importância de investigar as informações disponíveis antes de classificar uma mensagem como legítima ou maliciosa. A análise de diferentes indicadores, o uso de ferramentas apropriadas e a documentação das evidências são etapas importantes para uma investigação mais consistente.

Pretendo continuar praticando esses conceitos em outros laboratórios, buscando melhorar minha capacidade de identificar ameaças e compreender como funciona o processo de investigação em segurança cibernética.

---

**Plataforma:** [TryHackMe](https://tryhackme.com/module/phishing)  
**Área de estudo:** Cybersecurity / Blue Team / SOC  
**Status:** [Em andamento / Concluído]  
**Data:** [Adicione a data em que estudou o módulo]
