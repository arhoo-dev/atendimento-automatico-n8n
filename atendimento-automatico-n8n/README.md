\# 🤖 Atendimento Automático para Pequenas Empresas com n8n



Sistema de atendimento automático via formulário web, processamento com IA (Gemini) e resposta por e-mail, desenvolvido para fins acadêmicos.



---



\## 📋 Sobre o Projeto



Este projeto implementa um fluxo de automação no \*\*n8n\*\* que:



1\. Recebe solicitações de clientes via formulário web

2\. Processa a mensagem com a API do \*\*Google Gemini\*\* (gratuita)

3\. Gera uma resposta personalizada em formato JSON

4\. Envia automaticamente um e-mail de retorno ao cliente



\*\*Objetivo:\*\* Demonstrar a viabilidade de automação de atendimento para pequenas empresas usando ferramentas no-code/low-code.



---



\## 🛠️ Tecnologias Utilizadas



\- \*\*n8n\*\* - Plataforma de automação de workflows

\- \*\*Google Gemini API\*\* - Modelo de IA para geração de respostas

\- \*\*SMTP\*\* - Envio de e-mails (Gmail, Outlook, etc.)



---



\## 📦 Estrutura do Workflow



O workflow é composto por \*\*9 nodes\*\*:



1\. \*\*Form Trigger\*\* - Formulário web para captura de dados (Nome, E-mail, Mensagem)

2\. \*\*Set (Dados Iniciais)\*\* - Normaliza os campos recebidos

3\. \*\*Code (Prompt Setting)\*\* - Monta o prompt para a IA com contexto da empresa

4\. \*\*Code (Build Gemini JSON)\*\* - Prepara o payload para a API do Gemini

5\. \*\*Set (Keep Content)\*\* - Preserva nome e e-mail antes da chamada HTTP

6\. \*\*HTTP Request\*\* - Envia requisição para a Gemini API

7\. \*\*Merge\*\* - Combina dados do formulário com resposta da IA

8\. \*\*Code (Parse AI)\*\* - Extrai e formata a resposta JSON da IA

9\. \*\*Send Email\*\* - Envia resposta automática ao cliente



\### Diagrama Visual



!\[Workflow Completo](docs/prints/workflow-completo.png)



---



\## ⚙️ Configuração



\### Pré-requisitos



\- n8n instalado (local ou cloud)

\- Conta Google com acesso à \[Gemini API](https://aistudio.google.com/app/apikey)

\- Conta de e-mail com SMTP habilitado



\### Passo a Passo



\#### 1. Importar o Workflow



1\. Abra o n8n

2\. Clique em \*\*"Import from File"\*\*

3\. Selecione o arquivo `workflows/atendimento-automatico.json`



\#### 2. Configurar a API do Gemini



1\. Acesse \[Google AI Studio](https://aistudio.google.com/app/apikey)

2\. Gere uma \*\*API Key\*\*

3\. No node \*\*HTTP Request\*\*, substitua o valor do parâmetro `key` pela sua chave



\#### 3. Configurar o SMTP



No node \*\*Send Email\*\*:



\- \*\*From Email\*\*: seu e-mail

\- \*\*SMTP Credentials\*\*: configure nas credenciais do n8n

&nbsp; - Host: `smtp.gmail.com` (ou seu provedor)

&nbsp; - Port: `587` (TLS) ou `465` (SSL)

&nbsp; - User/Password: suas credenciais



\*\*Dica Gmail:\*\* Ative "Senhas de app" nas configurações de segurança da conta Google.



\#### 4. Personalizar os Dados da Empresa



No node \*\*Code (Prompt Setting)\*\*, edite o objeto `EMPRESA`: javascript const EMPRESA = { nome: "Sua Empresa", segmento: "Seu Segmento", cidade: "Sua Cidade", horario: "Seg–Sex 09:00–18:00", servicos: "Descrição dos serviços", politicas: "Políticas de atendimento" };

#### 5. Testar o Workflow

1. Ative o workflow
2. Acesse a URL do formulário (exibida no node **Form Trigger**)
3. Preencha e envie
4. Verifique o e-mail de resposta

---

## 📧 Exemplo de Saída

**Assunto do e-mail:**
> Informações sobre automação para sua empresa

**Corpo do e-mail:**
Olá João,

Obrigado por entrar em contato com a Ark Serviços em TI! Trabalhamos com automação de processos para pequenas empresas e podemos analisar seu cenário para propor uma solução sob medida.

Para avançarmos, você poderia me informar brevemente quais processos hoje mais consomem tempo na sua empresa?

Atenciosamente, Ark Serviços em TI

---

## 🔧 Troubleshooting

### Problema: E-mail não chega

- Verifique as credenciais SMTP
- Confira a caixa de spam
- Teste com outro provedor de e-mail

### Problema: Resposta da IA vem em branco

- Verifique se a API Key do Gemini está correta
- Confira os logs do node **HTTP Request**
- Veja se o prompt está sendo montado corretamente

### Problema: JSON inválido no Parse AI

- O código já tem fallback para esse caso
- Se persistir, verifique a resposta bruta no campo `ia_raw`

---

## 📚 Documentação Adicional

Consulte a pasta `docs/` para:
- [Configuração detalhada dos nodes](docs/configuracao.md)
- Prints de cada etapa do workflow

---

## 📄 Licença

Este projeto é de uso **acadêmico e educacional**. Sinta-se livre para usar, modificar e distribuir.

Licença: [MIT](LICENSE)

---

## 👤 Autor

**Adriel Ruda Henrique Ogawa Osorio**  
Projeto desenvolvido como trabalho acadêmico sobre automação de processos para pequenas empresas.

---

## 🤝 Contribuições

Sugestões e melhorias são bem-vindas! Abra uma **issue** ou envie um **pull request**.

---





