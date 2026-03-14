# Base de Conhecimento

## Dados Utilizados



| Arquivo | Formato | Para que serve na Elena? |
|---------|---------|---------------------|
| `historico_atendimento.csv` | CSV | Contextualizar interações anteriores, ou seja dar continuidade ao atendimento de maneira mais eficiente |
| `transacoes.csv` | CSV | Analisar padrão de gastos do cliente e usar essas informações para alerta-los |
| `perfil_investidor.json` | JSON | Dados do cliente , identificação, metas e objetivos. 



---

## Adaptações nos Dados

> Você modificou ou expandiu os dados mockados? Descreva aqui.

Sim, alterei os dados de histórico de atendimento e perfil do cliente  para ficar de acordo com o projeto. 

---

## Estratégia de Integração

### Como os dados são carregados?

Existem duas possibilidades de injetar o arquivo, via prompt( Ctrl + C, Ctrl + V) ou carregando um arquivo via código como o exemplo abaixo. 
```Python
import pandas as pd
import json
historico = pd.read_csv('data/historico_atendimento.csv')
transacoes = pd.read_csv('data/transacoes.csv')

with open ('data/perfil_investidor.json', 'r', encoding = 'utf-8' as f:
    perfil = json.load(f)

```


### Como os dados são usados no prompt?
> Os dados vão no system prompt? São consultados dinamicamente?

Para simplificar, podemos injetar dados em nosso prompt, garantindo que o assistente tenha o melhor contexto possível. Mas , para soluções mais robustas, o ideal é que essas informações sejam carfregadas dinamicamente para que possamos ganhar flexibilidade. 

```texto
Dados do cliente(data/perfil_investidor.json):
{
  "nome": "João Silva",
  "idade": 32,
  "profissao": "Analista de Sistemas",
  "renda_mensal": 5000.00,
  "perfil_investidor": "moderado",
  "objetivo_principal": "Construir reserva de emergência",
  "patrimonio_total": 15000.00,
  "reserva_emergencia_atual": 10000.00,
  "aceita_risco": false,
  "metas": [
    {
      "meta": "Completar reserva de emergência",
      "valor_necessario": 15000.00,
      "prazo": "2026-06"
    },
    {
      "meta": "Entrada do apartamento",
      "valor_necessario": 50000.00,
      "prazo": "2027-12"
    }
  ]
}

Histórico de transações(data/transacoes.csv):
data,descricao,categoria,valor,tipo
2025-10-01,Salário,receita,5000.00,entrada
2025-10-02,Aluguel,moradia,1200.00,saida
2025-10-03,Supermercado,alimentacao,450.00,saida
2025-10-05,Netflix,lazer,55.90,saida
2025-10-07,Farmácia,saude,89.00,saida
2025-10-10,Restaurante,alimentacao,120.00,saida
2025-10-12,Uber,transporte,45.00,saida
2025-10-15,Conta de Luz,moradia,180.00,saida
2025-10-20,Academia,saude,99.00,saida
2025-10-25,Combustível,transporte,250.00,saida

Histórico de atendimento(data/historico_atendimento.csv):
data,canal,tema,resumo,resolvido
2025-09-15,chat,Limite de gastos,Cliente perguntou como definir limite mensal de despesas,sim
2025-09-22,telefone,Notificação de alerta,Erro ao receber alerta de gasto foi corrigido,sim
2025-10-01,chat,Categoria de despesas,Cliente pediu explicação sobre classificação automática de gastos,sim
2025-10-12,chat,Metas de economia,Cliente acompanhou o progresso da meta de reduzir gastos com lazer,sim
2025-10-25,email,Atualização de preferências,Cliente atualizou e-mail para receber alertas de gastos,sim


````
---

## Exemplo de Contexto Montado

> Mostre um exemplo de como os dados são formatados para o agente.


O exemplo de contexto montado abaixo, se baseia nos dados originais da base de conhecimento, mas sintetiza deixando apenas os mais relevantes, otimizando assim o consumo de tokens. Porém o mais importante do que economizar tokens é ter todas as informações relevantes disponíveis. 

```
Dados do Cliente:
- Nome: João Silva
- Saldo disponível: R$ 5.000

Últimas transações:
- 01/11: Supermercado - R$ 450
- 03/11: Streaming - R$ 55

Total de saídas: R$ 505
Saldo restante: R$ 4995
...
```
