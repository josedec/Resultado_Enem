# Como implementar IA no n8n para gerar mensagens automáticas de aprovação no ENEM

Vamos evoluir o workflow anterior para que a Inteligência Artificial escreva uma mensagem personalizada para cada estudante aprovado e envie essa mensagem automaticamente pelo Telegram.

Em vez de enviar sempre o mesmo texto, a IA poderá usar o nome do estudante, o curso e o contexto da aprovação para criar uma mensagem mais natural e acolhedora.

## 1. Arquitetura do workflow com IA

1. Schedule Trigger

Executa a cada 15 minutos

2. Google Sheets

Lê os resultados dos estudantes

3. IF

Aprovado e ainda não notificado?

4. OpenAI — gerar mensagem

Cria um texto personalizado com IA

5. Telegram — Send Message

Envia o texto produzido pela IA

6. Google Sheets — Update Row

Registra que o aviso foi enviado

O principal acréscimo é o node de IA entre o IF e o Telegram. O restante do workflow continua responsável por filtrar os aprovados e controlar os envios.

## 2. Adicionar o node de IA

A opção mais direta é usar o node OpenAI do n8n, com uma operação de geração de texto. Você precisará de uma chave de API da OpenAI; o uso da API pode ser cobrado separadamente da assinatura do ChatGPT.

1. No workflow, clique em `+`.
2. Pesquise `OpenAI`.
3. Adicione o node e selecione a operação de geração de texto ou mensagem, conforme a versão disponível.
4. Crie uma credencial usando sua API key.
5. Selecione um modelo de texto econômico disponível na sua conta, por exemplo, `gpt-4o-mini`, se estiver disponível.

A integração oficial permite usar modelos da OpenAI nos workflows do n8n.

n8n

## 3. Configurar o prompt da IA

No campo de instruções ou mensagem do node OpenAI, cole este prompt. As expressões entre chaves serão substituídas pelos dados de cada linha da planilha.

### Prompt de geração automática

 Copiar prompt

Você é um assistente de comunicação educacional. Escreva uma mensagem de parabéns em português brasileiro para um estudante cuja aprovação já foi confirmada na planilha. Nome: {{ $json.nome }} Curso: {{ $json.curso }} Regras: - Seja acolhedor, natural e positivo. - Use no máximo 100 palavras. - Use no máximo 2 emojis. - Não invente notas, classificação, universidade, bolsa ou informações que não foram fornecidas. - Não prometa matrícula ou vaga além do que os dados confirmam. - Não inclua explicações sobre o prompt. - Retorne somente o texto final da mensagem, pronto para enviar no Telegram.

Por que esse prompt funciona? Ele orienta o modelo a personalizar a mensagem sem inventar detalhes sobre o resultado do estudante.

## 4. Conectar a IA ao Telegram

Conecte o node OpenAI ao node Telegram, mantendo o Telegram depois da geração do texto.

Configure o Telegram:

- Resource: Message
- Operation: Send Message
- Credential: sua credencial do bot
- Chat ID: use a expressão abaixo para recuperar o identificador da planilha.

javascript
```
{{ $('IF').item.json.chat_id }}
```

No campo Text, selecione a saída gerada pelo node OpenAI.

O caminho exato depende da operação e da versão do node. Para configurá-lo corretamente:

1. Execute o node OpenAI com um estudante de teste.
2. Abra o resultado em Output.
3. Localize o campo que contém o texto produzido pela IA.
4. No campo Text do Telegram, ative o modo Expression e selecione esse campo pelo painel de expressões.

Por exemplo, se o resultado do node tiver uma propriedade chamada `text`, a expressão será:

javascript
```
{{ $json.text }}
```

Não use essa última expressão sem conferir a saída real do seu node. O Telegram aceita o texto gerado diretamente no campo de mensagem.

GitHub

## 5. Atualizar a planilha

Depois do envio, mantenha o node `Google Sheets — Update Row` para marcar `aviso_enviado = SIM`.

Use uma coluna de identificação única, como `id_estudante`, para atualizar a linha correta. Se o node de IA substituir os dados de entrada pela resposta do modelo, recupere o identificador a partir do node anterior ou use um node `Merge` para combinar os dados originais com o texto gerado.

O envio deve ocorrer somente depois de o resultado estar confirmado e o campo de controle indicar que ainda não houve notificação.

## 6. Exemplo do resultado

Para uma linha com nome `Ana` e curso `Administração`, a IA poderia gerar:

Bot de aprovação ENEM

🎉 Parabéns, Ana!

Sua aprovação é uma conquista muito especial! Todo o esforço e a dedicação ao longo dessa jornada merecem ser celebrados.

Que essa nova etapa no curso de Administração traga muitas oportunidades de aprendizado e crescimento. Desejamos muito sucesso nessa caminhada! 📚

Exemplo ilustrativo de mensagem gerada por IA.

## 7. Teste antes de ativar

- [ ]O IF permite somente estudantes aprovados ainda não notificados.
- [ ]O OpenAI recebe o nome e o curso corretos.
- [ ]O texto gerado aparece corretamente na saída do node.
- [ ]O Telegram recebe o texto e usa o `chat_id` correto.
- [ ]A planilha é atualizada após o envio bem-sucedido.
- [ ]Uma segunda execução não envia a mesma mensagem novamente.

Minha recomendação: comece com o node OpenAI e o Telegram funcionando para uma única linha de teste. Depois, teste o processamento de várias linhas e o controle de mensagens duplicadas antes de ativar a execução automática.
