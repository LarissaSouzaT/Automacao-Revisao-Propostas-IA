# 🤖 Auditor Inteligente de Propostas Comerciais (Python + Flask + IA)

Estudo de caso e arquitetura de uma aplicação web desenvolvida durante minha atuação na área de **Pré-Vendas** da **Stefanini Group**, com o objetivo de automatizar a revisão ortográfica, gramatical e a auditoria textual de propostas comerciais em PowerPoint (`.pptx`).

> **Nota sobre o código-fonte:** Por ter sido desenvolvido em ambiente corporativo para uso interno da empresa, os arquivos originais são protegidos por propriedade intelectual e confidencialidade. Este repositório documenta a arquitetura da solução, o fluxo de processamento e o impacto gerado na rotina de Pré-Vendas.

---

### 🎯 Problema de Negócio
Na rotina de Pré-Vendas, as propostas comerciais eram elaboradas em apresentações de PowerPoint com dezenas de slides e exigiam revisões manuais minuciosas antes do envio aos clientes. Esse processo consumia tempo relevante da equipe e mantinha o risco de falhas ortográficas ou inconsistências de escrita passarem despercebidas em entregas com prazos curtos.

### 💡 A Solução
Desenvolvi uma aplicação web interna utilizando **Python**, **Flask** e integração com a **API da OpenAI** para auditar automaticamente os arquivos de apresentação:

1. **Upload via Interface Web (Flask):** O colaborador acessa o portal web, anexa o arquivo da proposta comercial em formato **PowerPoint (`.pptx`)** e aciona o envio com um clique.
2. **Extração Estruturada por Slide (Python):** O backend processa o arquivo `.pptx`, mapeando e extraindo os blocos de texto vinculados ao número exato de cada slide.
3. **Auditoria Linguística e Explicativa (OpenAI API + Prompt Engineering):** Os textos extraídos são enviados via API (autenticada por variáveis de ambiente / `API Key`) com prompts estruturados para identificar desvios ortográficos e gramaticais.
4. **Relatório Diagnóstico na Tela (Human-in-the-Loop):** O site em Flask exibe um diagnóstico detalhado apontando:
   * **Qual slide** contém o erro;
   * **Qual trecho** apresenta inconsistência;
   * **Como aplicar a correção** e a **explicação gramatical** do motivo pelo qual o texto estava incorreto.

> **Escopo e Governança (Human-in-the-Loop):** A aplicação foi projetada intencionalmente para atuar como uma ferramenta de **diagnóstico e apoio à decisão**, sem gerar ou sobrescrever um novo arquivo PowerPoint automaticamente. Dessa forma, o analista mantém controle total sobre o layout e o conteúdo final da apresentação, sabendo exatamente onde intervir e aprendendo com cada apontamento.

---

### 🏗️ Arquitetura da Solução

    [Analista de Pré-Vendas] 
           │
           ▼ (Faz upload do arquivo .pptx e clica em Enviar)
    [Interface Web em Flask] 
           │
           ▼ (Extração do texto mapeado por número de slide)
    [Backend Python + Prompt Engineering] 
           │
           ▼ (Autenticação segura via API Key)
    [API OpenAI (LLM)] ──► [Identificação de Erros + Sugestão + Explicação]
           │
           ▼
    [Relatório Diagnóstico exibido no site (Slide | Erro | Correção | Motivo)]

---

### 🛠️ Tecnologias e Conceitos Aplicados
* **Linguagem:** Python (manipulação e leitura de arquivos `.pptx`)
* **Framework Web:** Flask (upload de arquivos, rotas, processamento de requisições e renderização de resultados)
* **Inteligência Artificial:** OpenAI API (GPT) e Engenharia de Prompts com foco educativo/explicativo
* **Segurança e Boas Práticas:** Proteção de credenciais (`API Key`) via variáveis de ambiente para controle de custos e acesso

### 📈 Resultados Alcançados
* **Agilidade na revisão:** Redução expressiva do tempo gasto pela equipe de Pré-Vendas na conferência manual de apresentações extensas.
* **Precisão cirúrgica:** Ao indicar exatamente o número do slide e o trecho incorreto, o analista vai direto ao ponto de ajuste sem precisar reler toda a proposta.
* **Capacitação contínua:** A explicação do porquê de cada correção reduziu a recorrência dos mesmos erros de escrita nas propostas seguintes.
