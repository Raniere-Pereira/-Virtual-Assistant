# Base de Conhecimento

## Dados Utilizados

| Arquivo | Formato | Utilização no Agente |
|---------|---------|---------------------|
| `historico_atendimento.csv` | CSV | Contextualizar interações anteriores |
| `perfil_investidor.json` | JSON | Personalizar recomendações |
| `produtos_financeiros.json` | JSON | Sugerir produtos adequados ao perfil |
| `personal_transactions.xlsx` | XLSX | Analisar padrão de gastos do cliente |

---

## Adaptações nos Dados

Dados mockados do arquivo `personal_transactions.xlsx` obtidos a partir do [Kaggle](https://www.kaggle.com/datasets/entrepreneurlife/personal-finance/code)

---

## Estratégia de Integração

### Como os dados são carregados?
Os arquivos são carregados no início da sessão via código conforme abaixo ou incluídos no contexto do prompt.

```python
import json
import pandas as pd

# CSV 
historico=pd.read_csv('data/historico_atendimento.csv')

#XLSX
transacoes = pd.read_excel('data/personal_transactions.xlsx')

#JSON
with open('data/perfil_investidor.json','r',enconding='utf-8') as f:
  perfil = json.load(f)

with open('data/produtos_financeiros.json','r',enconding ='utf-8') as f:
produtos = json.load(f)

```
### Como os dados são usados no prompt?

Os dados podem ser utilizados para:

Entender o contexto financeiro do usuário: renda, despesas, orçamento, investimentos e objetivos.
Identificar padrões: analisar gastos recorrentes, categorias com maior consumo e possíveis desvios do orçamento.
Personalizar recomendações: adaptar sugestões de acordo com os objetivos e perfil financeiro informado.
Realizar cálculos: saldo disponível, percentual de gastos, projeções, metas de economia e cenários financeiros.
Gerar alertas proativos: identificar, por exemplo, aumento incomum de despesas ou aproximação de um limite orçamentário.
Contextualizar a resposta: utilizar os dados mais recentes disponíveis para evitar respostas genéricas.
Manter segurança: limitar as recomendações aos dados fornecidos e sinalizar quando não houver informações suficientes para uma conclusão.

## Exemplo de Contexto Montado

```
Dados do Cliente:
- Nome: João Silva
- Perfil: Moderado
- Saldo disponível: R$ 5.000

Últimas transações:
- 01/11: Supermercado - R$ 450
- 03/11: Streaming - R$ 55
...
```
