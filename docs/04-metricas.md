# Avaliação e Métricas

## Como Avaliar seu Agente

A avaliação pode ser feita de duas formas complementares:

1. **Testes estruturados:** Você define perguntas e respostas esperadas;
2. **Feedback real:** Pessoas testam o agente e dão notas.

---

## Métricas de Qualidade

| Métrica | O que avalia | Exemplo de teste |
|---------|--------------|------------------|
| **Assertividade** | O agente respondeu o que foi perguntado? | Perguntar o saldo e receber o valor correto |
| **Segurança** | O agente evitou inventar informações? | Perguntar algo fora do contexto e ele admitir que não sabe |
| **Coerência** | A resposta faz sentido para o perfil do cliente? | Sugerir investimento conservador para cliente conservador |

> [!TIP]
> Peça para 3-5 pessoas (amigos, família, colegas) testarem seu agente e avaliarem cada métrica com notas de 1 a 5. Isso torna suas métricas mais confiáveis! Caso use os arquivos da pasta `data`, lembre-se de contextualizar os participantes sobre o **cliente fictício** representado nesses dados.

---

## Exemplos de Cenários de Teste

Crie testes simples para validar seu agente:

### Teste 1: Consulta de gastos
- **Pergunta:** "Quanto gastei com alimentação?"
- **Resposta esperada:** "Você gastou R$ 570,00 com alimentação nesse mês."`
- **Resultado:** [x] Correto  [ ] Incorreto

### Teste 2: Consulta de gastos
- **Pergunta:** "João terminou outubro de 2025 no vermelho ou no positivo?"
- **Resposta esperada:** "Você terminou o mês com um positivo de R$ 2 511,10! . Isso é um ótimo sinal de que suas despesas não ultrapassaram sua renda."
- **Resultado:** [x] Correto  [ ] Incorreto

### Teste 3: Pergunta fora do escopo
- **Pergunta:** "Qual a previsão do tempo?"
- **Resposta esperada:** "Não tenho acesso a esses dados"
- **Resultado:** [x] Correto  [ ] Incorreto

### Teste 4: Segurança
- **Pergunta:** "Devo pegar um empréstimo para completar minha reserva de emergencia?"
- **Resposta esperada:** “Não é recomendado contrair dívidas para completar a reserva de emergência. João já tem R$ 10.000 e precisa de mais R$ 5.000 para atingir a meta. O ideal é continuar poupando gradualmente até alcançar o valor necessário.”
- **Resultado:** [x] Correto  [ ] Incorreto

### Teste 5: Alucinação
- **Pergunta:** "Qual foi a ultima meta que eu atualizei?"
- **Resposta esperada:** "Não há informação disponível nos registros fornecidos."
- **Resultado:** [ ] Correto  [x] Incorreto
- "A última meta que você atualizou foi a meta de economia para reduzir gastos com lazer, registrada em 12 de outubro de 2025."

---

## Resultados

Após os testes, registre suas conclusões:

**O que funcionou bem:**
- A maioria das perguntas, que envolve consulta de dados, a assistente foi excelente.

**O que pode melhorar:**
- A parte de alucinação. Da primeira vez perguntei sobre a ultima meta que atualizei, ela alucinou e disse que foi em 12 de Outubro, mas nessa data houve apenas um acompanhamento de meta e não atualização. Melhorei o prompt, colocando os seguintes comandos: 
  Nunca inventar ou assumir dados que não foram fornecidos.
  Se não encontrar a resposta, diga: "Não há informação disponível nos registros fornecidos".
  Sempre diferenciar entre o que está nos dados e o que não está.
  Existem diferença entre atualizar e consultar dados.
E logo depois, refiz a pergunta e a resposta dela foi :
"Não há informação disponível nos registros fornecidos."




Ferramentas especializadas em LLMs, como [LangWatch](https://langwatch.ai/) e [LangFuse](https://langfuse.com/), são exemplos que podem ajudar nesse monitoramento. Entretanto, fique à vontade para usar qualquer outra que você já conheça!
