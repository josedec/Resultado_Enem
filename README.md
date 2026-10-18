# Descrição do projeto: Assistente de Investimentos com RPA, n8n e IA Generativa

O projeto [DIO Lab — Assistente de Investimentos RPA n8n](<https://github.com/josedec/dio-lab-assistente-investimentos-rpa-n8n?utm_source=chatgpt.com>) tem como objetivo automatizar a coleta de dados de clientes e a geração de mensagens personalizadas sobre investimentos, utilizando Python, RPA, n8n e, opcionalmente, Inteligência Artificial Generativa.

Josedec · GitHub

A proposta é simular um processo de atendimento financeiro no qual um robô coleta informações de clientes, identifica o perfil de investidor e prepara uma comunicação adequada para cada pessoa.

## 1. Como funciona o projeto?

1. Fonte de dados

Página HTML com clientes fictícios e arquivo CSV com opções de investimento.

2. RPA com Python

O script utiliza BeautifulSoup para extrair os dados dos clientes da página web.

3. Webhook do n8n

Recebe os dados enviados pelo script Python e inicia o workflow de automação.

4. Processamento dos dados

Cruza o perfil do cliente com as opções de investimento disponíveis.

5. Geração da mensagem

Cria uma mensagem baseada em um modelo fixo ou, na versão avançada, com auxílio de IA generativa.

Fluxo resumido a partir da arquitetura e das etapas documentadas no repositório.

Josedec · GitHub

## 2. Tecnologias utilizadas

| Tecnologia | Função no projeto |
| --- | --- |
| Python | Executar o script de automação. |
| BeautifulSoup | Extrair informações da página HTML. |
| n8n | Orquestrar as etapas do processo visualmente. |
| Webhook HTTP | Fazer a comunicação entre Python e n8n. |
| CSV | Armazenar opções de investimento por perfil. |
| IA Generativa | Criar mensagens personalizadas na versão avançada. |
| GitHub Pages | Hospedar a página de clientes e o arquivo CSV. |

Essas tecnologias são descritas no README do projeto.

Josedec · GitHub

## 3. Exemplo prático de funcionamento

Imagine que a página contenha os seguintes clientes fictícios:

Cliente A — Conservador

O fluxo seleciona opções com foco em renda fixa e segurança.

Resultado: mensagem que prioriza estabilidade e preservação de capital.

Cliente B — Moderado

O fluxo considera alternativas de renda fixa e variável.

Resultado: mensagem com uma abordagem equilibrada entre risco e retorno.

Cliente C — Arrojado

O fluxo considera alternativas com maior exposição à renda variável.

Resultado: mensagem que explica o potencial de retorno e os riscos envolvidos.

Esses exemplos ilustram a lógica proposta pelo laboratório; não são recomendações financeiras reais.

Josedec · GitHub

## 4. Qual é o papel do n8n?

O n8n é o centro da automação. Ele conecta as diferentes etapas sem exigir que toda a lógica seja programada manualmente em Python.

O workflow deve executar estas tarefas:

- Receber: capturar os dados enviados pelo Webhook.
- Consultar: obter as opções de investimento do arquivo CSV.
- Tratar: organizar os dados recebidos e cruzá-los com os perfis.
- Gerar: montar a mensagem correspondente a cada cliente.
- Expandir: integrar um modelo de IA para tornar as mensagens mais dinâmicas.

Na versão mínima, a geração utiliza mensagens predefinidas. Na versão avançada, é possível integrar um modelo como Gemini ou GPT.

Josedec · GitHub

## 5. Como começar a executar o projeto

1. Acesse o repositório. Entre no [GitHub do projeto](<https://github.com/josedec/dio-lab-assistente-investimentos-rpa-n8n?utm_source=chatgpt.com>) e faça o fork ou baixe os arquivos.
2. Execute o notebook Python. Abra o notebook de extração no [Google Colab](<https://colab.research.google.com/?utm_source=chatgpt.com>) e entenda como os dados são coletados.
3. Crie um workflow no n8n. Adicione um node Webhook para receber os dados dos clientes.
4. Configure a integração. Copie a URL do Webhook e configure o envio no script Python. Atenção: o README informa que essa parte do envio ainda está pendente no código inicial.
5. Implemente o processamento. Configure os nodes para ler as opções de investimento, cruzar os dados e gerar as mensagens.
6. Teste o fluxo completo. Verifique se os dados chegam corretamente e se cada cliente recebe a mensagem correspondente ao seu perfil.
 GitHub

## 6. O que você aprende com esse projeto?

- Automação de tarefas repetitivas com RPA.
- Integração entre Python e n8n por meio de Webhooks.
- Manipulação de dados estruturados e arquivos CSV.
- Construção de workflows visuais.
- Aplicação de IA generativa em processos de negócio.
- Separação de responsabilidades entre coleta, processamento e comunicação.

Em resumo: é um projeto de aprendizado que demonstra como transformar uma tarefa manual de coleta e preparação de comunicações financeiras em um processo automatizado, integrando Python, n8n e IA. O repositório descreve a arquitetura e as etapas do desafio, mas o workflow completo precisa ser implementado e testado para que a automação funcione de ponta a ponta.
