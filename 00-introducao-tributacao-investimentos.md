# Tributação de Investimentos no Brasil — Introdução

> Material de estudo voltado para desenvolvimento e back office de instituições financeiras.
>
> **Versão de referência:** outubro de 2026  
> **Importante:** regras tributárias podem mudar. Sempre valide regras críticas nas fontes oficiais antes de utilizá-las em sistemas produtivos, cálculos fiscais ou decisões financeiras.

---

## 1. Objetivo deste material

Este material tem como objetivo construir uma base sólida sobre tributação de investimentos no Brasil, com foco especial em situações comuns em sistemas de **corretoras, bancos, custódia, liquidação e back office**.

O objetivo não é apenas decorar quais produtos possuem ou não Imposto de Renda.

A proposta é desenvolver uma linha de raciocínio que permita responder, para qualquer produto financeiro:

1. Qual é o produto?
2. Quem é o investidor?
3. Qual é o regime tributário aplicável?
4. Qual foi o evento financeiro?
5. Houve fato gerador?
6. Qual é a base de cálculo?
7. Qual é a alíquota?
8. Existe isenção?
9. Existe IRRF?
10. Quem é responsável pela retenção ou recolhimento?
11. Existem compensações?
12. Qual é o valor líquido da operação?
13. Como esse evento deve ser representado em um sistema de back office?

---

## 2. Por que tributação de investimentos é um domínio complexo?

Dizer apenas:

> "CDB paga IR."

ou:

> "LCI é isenta."

não é suficiente para trabalhar com sistemas financeiros.

Cada produto pode possuir regras diferentes relacionadas a:

- tipo de investidor;
- pessoa física ou pessoa jurídica;
- residência fiscal;
- prazo da aplicação;
- data da aquisição;
- tipo de evento;
- resgate;
- vencimento;
- alienação;
- amortização;
- distribuição;
- retenção na fonte;
- compensação de prejuízos;
- período de apuração;
- regime tributário;
- mudanças legislativas.

Por isso, a tributação deve ser estudada como um **domínio**.

---

## 3. Modelo mental principal

A lógica utilizada ao longo de todo o material será:

```text
PRODUTO
   ↓
POSIÇÃO
   ↓
MOVIMENTAÇÃO
   ↓
EVENTO
   ↓
RENDIMENTO / GANHO / PERDA
   ↓
FATO GERADOR
   ↓
BASE DE CÁLCULO
   ↓
ALÍQUOTA
   ↓
IR / IRRF
   ↓
COMPENSAÇÕES
   ↓
VALOR LÍQUIDO
   ↓
INFORMAÇÃO FISCAL
```

O ponto central é:

> **Tributação não começa pela alíquota. Ela começa pela identificação do produto, do investidor e do evento.**

---

## 4. Perspectiva de back office

Em uma aplicação financeira, o mesmo investimento pode gerar informações diferentes.

Exemplo:

```text
Aplicação inicial       R$ 100.000
Rendimento acumulado    R$  10.000
Saldo bruto             R$ 110.000
IR estimado             R$   2.000
Saldo líquido estimado  R$ 108.000
```

Esses valores não representam a mesma coisa.

Em sistemas financeiros, podemos encontrar conceitos como:

```text
Principal
GrossBalance
GrossIncome
TaxBase
TaxRate
TaxCalculated
TaxWithheld
TaxDue
NetIncome
NetBalance
```

A compreensão dessas diferenças é fundamental para evitar erros em:

- APIs;
- relatórios;
- informes;
- conciliações;
- liquidações;
- cálculo de posição;
- cálculo de rentabilidade;
- motores tributários;
- eventos financeiros.

---

## 5. Produtos que serão estudados

### Renda fixa

- CDB
- RDB
- Tesouro Direto
- títulos públicos
- LCI
- LCA
- CRI
- CRA
- debêntures
- debêntures incentivadas
- poupança
- operações compromissadas

### Fundos

- fundos de renda fixa
- fundos multimercado
- fundos de ações
- fundos de curto prazo
- fundos de longo prazo
- FII
- FIAGRO
- ETF
- FIDC
- fundos sujeitos à tributação periódica

### Renda variável

- ações
- operações comuns
- day trade
- ETF
- FII
- FIAGRO
- mercado a termo
- opções
- futuros

### Eventos e situações especiais

- amortização
- resgate
- vencimento
- alienação
- bonificação
- desdobramento
- grupamento
- subscrição
- compensação de prejuízos
- IRRF
- DARF
- custo de aquisição
- preço médio

---

## 6. Visão inicial: produtos tributados e isentos

A classificação abaixo é apenas introdutória.

As condições específicas serão estudadas posteriormente.

| Produto | Visão inicial para pessoa física |
|---|---|
| CDB | Tributado |
| RDB | Tributado |
| Tesouro Direto | Tributado |
| LCI | Rendimento isento, observadas as regras legais |
| LCA | Rendimento isento, observadas as regras legais |
| CRI | Pode possuir tratamento isento para PF, conforme requisitos legais |
| CRA | Pode possuir tratamento isento para PF, conforme requisitos legais |
| Poupança | Isenta para PF |
| Debênture comum | Tributável |
| Debênture incentivada | Possui tratamento fiscal específico conforme legislação |
| Ações | Ganhos podem ser tributados conforme tipo de operação e regras aplicáveis |
| Fundos | Dependem da classificação e do regime do fundo |

A Receita Federal atualmente classifica, entre outros, **poupança, LCI, LCA, CRI e CRA** entre os patrimônios que podem possuir rendimentos isentos.

---

## 7. Tabela regressiva — visão inicial

Para **fundos de longo prazo e aplicações de renda fixa em geral**, a Receita Federal publica em 2026:

| Prazo | Alíquota de IR |
|---|---:|
| Até 180 dias | 22,5% |
| De 181 a 360 dias | 20,0% |
| De 361 a 720 dias | 17,5% |
| Acima de 720 dias | 15,0% |

Essa tabela será estudada detalhadamente na parte dedicada à renda fixa.

---

## 8. Estrutura do curso

### Parte I — Fundamentos

- patrimônio;
- principal;
- saldo bruto;
- saldo líquido;
- rendimento;
- ganho;
- perda;
- custo de aquisição;
- fato gerador;
- base de cálculo;
- alíquota;
- IR;
- IRRF;
- imposto devido;
- período de apuração;
- compensação;
- provisão;
- realização.

### Parte II — Renda fixa

- CDB;
- RDB;
- Tesouro;
- LCI;
- LCA;
- CRI;
- CRA;
- debêntures;
- IOF;
- resgate;
- vencimento;
- mercado secundário.

### Parte III — Fundos de investimento

- cotas;
- fundos de curto prazo;
- fundos de longo prazo;
- fundos de ações;
- tributação periódica;
- come-cotas;
- resgate;
- amortização;
- FII;
- FIAGRO;
- ETF.

### Parte IV — Renda variável

- ações;
- custo de aquisição;
- preço médio;
- operações comuns;
- day trade;
- ganhos;
- perdas;
- compensação;
- IRRF;
- DARF.

### Parte V — Operações avançadas

- opções;
- futuros;
- termo;
- derivativos;
- aluguel de ativos;
- eventos corporativos.

### Parte VI — Tributação aplicada ao back office

- posição;
- custódia;
- movimentação;
- liquidação;
- eventos;
- histórico tributário;
- saldo bruto;
- saldo líquido;
- imposto provisionado;
- imposto realizado;
- conciliação;
- arquitetura de motores tributários.

---

## 9. Como estudar este material

Para cada produto, utilizar sempre a sequência:

```text
1. Entender o produto
2. Identificar os eventos financeiros
3. Identificar o fato gerador
4. Identificar a base de cálculo
5. Identificar a alíquota
6. Identificar retenções
7. Identificar compensações
8. Calcular o resultado líquido
9. Modelar o comportamento no sistema
10. Implementar exemplos em código
```

Uma boa pergunta para cada capítulo é:

> "Se eu precisasse implementar isso em um sistema de back office amanhã, quais informações precisaria armazenar?"

---

# Referências oficiais

## Receita Federal — Tributação de 2026

Tabela oficial de tributação, incluindo rendimentos de capital e aplicações financeiras.

https://www.gov.br/receitafederal/pt-br/assuntos/meu-imposto-de-renda/tabelas/2026

## Receita Federal — Rendimentos do Capital

Informações sobre rendimentos de aplicações financeiras e renda variável.

https://www.gov.br/receitafederal/pt-br/assuntos/meu-imposto-de-renda/preenchimento/manual-mir/rendimentos/rendimentos-do-capital

## Receita Federal — Bens Financeiros

Estrutura utilizada pela Receita para aplicações, investimentos, fundos e outros ativos financeiros.

https://www.gov.br/receitafederal/pt-br/assuntos/meu-imposto-de-renda/preenchimento/manual-mir/patrimonio/bens-financeiros

## Receita Federal — Eventos do Patrimônio

Informações sobre eventos relacionados a bens e investimentos, incluindo rendimentos de aplicações financeiras e títulos isentos.

https://www.gov.br/receitafederal/pt-br/assuntos/meu-imposto-de-renda/preenchimento/manual-mir/patrimonio/eventos-do-patrimonio

---

## Observação

Este repositório deve ser utilizado como **material educacional e técnico**.

Para cálculos fiscais reais, desenvolvimento de sistemas produtivos ou interpretação de situações específicas, é importante verificar:

- legislação vigente;
- instruções normativas;
- atos da Receita Federal;
- documentação da instituição;
- parecer das áreas fiscal, jurídica ou de compliance quando aplicável.

As regras deste documento foram verificadas em **outubro de 2026**.
