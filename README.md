# Tributação de Investimentos no Brasil

Material de estudo técnico sobre **tributação de investimentos no Brasil**, com foco em profissionais que atuam com **desenvolvimento de software, back office, custódia, liquidação e sistemas financeiros**.

O objetivo deste repositório é organizar, de forma progressiva e consultável, os principais conceitos relacionados a:

- Imposto de Renda sobre investimentos;
- rendimentos;
- saldos;
- ganhos e perdas;
- IRRF;
- fato gerador;
- base de cálculo;
- isenções;
- compensação de prejuízos;
- regras por produto;
- modelagem de domínio para sistemas financeiros.

> **Última revisão geral:** outubro de 2026  
> Regras tributárias podem mudar. Para uso em sistemas produtivos ou cálculos fiscais reais, sempre valide as regras com a legislação e as fontes oficiais vigentes.

---

## Objetivo do projeto

A proposta deste repositório não é apenas criar uma tabela de alíquotas.

O objetivo é desenvolver uma linha de raciocínio que permita analisar qualquer produto financeiro a partir da seguinte sequência:

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

A ideia central é:

> **Tributação não começa pela alíquota. Ela começa pela identificação do produto, do investidor, do evento e do fato gerador.**

---

## Público-alvo

Este material foi pensado principalmente para:

- desenvolvedores de sistemas financeiros;
- profissionais de back office;
- profissionais de corretoras e bancos;
- pessoas que trabalham com custódia e liquidação;
- profissionais de tecnologia que precisam entender regras tributárias;
- estudantes do mercado financeiro;
- investidores que desejam compreender a lógica por trás dos impostos.

---

## Estrutura do repositório

```text
tributacao-investimentos/
├── README.md
├── 00-introducao-tributacao-investimentos.md
├── 01-parte-i-fundamentos-tributacao-investimentos.md
├── 02-parte-ii-renda-fixa.md
├── 03-parte-iii-fundos-investimento.md
├── 04-parte-iv-renda-variavel.md
├── 05-parte-v-operacoes-avancadas.md
└── 06-parte-vi-backoffice-tributacao.md
```

Os arquivos serão construídos progressivamente ao longo dos estudos.

---

## Conteúdo

### 00 — Introdução

Apresenta a proposta do projeto, o modelo mental utilizado e a visão geral dos produtos que serão estudados.

Principais temas:

- produto financeiro;
- posição;
- movimentação;
- evento financeiro;
- fato gerador;
- rendimento;
- ganho;
- imposto;
- resultado líquido;
- visão de back office.

Arquivo:

[`00-introducao-tributacao-investimentos.md`](./00-introducao-tributacao-investimentos.md)

---

### 01 — Parte I: Fundamentos

Constrói a base necessária para compreender os demais módulos.

Principais conceitos:

- principal;
- patrimônio;
- saldo bruto;
- saldo líquido;
- rendimento bruto;
- rendimento líquido;
- ganho;
- perda;
- custo de aquisição;
- fato gerador;
- base de cálculo;
- alíquota;
- IR;
- IRRF;
- imposto devido;
- compensação;
- período de apuração;
- provisão;
- realização.

Arquivo:

[`01-parte-i-fundamentos-tributacao-investimentos.md`](./01-parte-i-fundamentos-tributacao-investimentos.md)

---

### 02 — Parte II: Renda Fixa

> Em desenvolvimento.

Produtos e temas previstos:

- CDB;
- RDB;
- Tesouro Direto;
- títulos públicos;
- LCI;
- LCA;
- CRI;
- CRA;
- debêntures;
- debêntures incentivadas;
- IOF;
- tabela regressiva;
- vencimento;
- resgate;
- mercado secundário.

---

### 03 — Parte III: Fundos de Investimento

> Em desenvolvimento.

Temas previstos:

- cotas;
- fundos de curto prazo;
- fundos de longo prazo;
- fundos de ações;
- tributação periódica;
- come-cotas;
- amortização;
- resgate;
- FII;
- FIAGRO;
- ETF;
- FIDC.

---

### 04 — Parte IV: Renda Variável

> Em desenvolvimento.

Temas previstos:

- ações;
- custo de aquisição;
- preço médio;
- operações comuns;
- day trade;
- ganhos;
- perdas;
- IRRF;
- compensação de prejuízos;
- período de apuração;
- DARF.

---

### 05 — Parte V: Operações Avançadas

> Em desenvolvimento.

Temas previstos:

- opções;
- mercado futuro;
- termo;
- derivativos;
- aluguel de ativos;
- eventos corporativos;
- bonificação;
- desdobramento;
- grupamento;
- subscrição.

---

### 06 — Parte VI: Tributação aplicada ao Back Office

> Em desenvolvimento.

Temas previstos:

- posição;
- custódia;
- movimentações;
- liquidação;
- eventos financeiros;
- histórico tributário;
- saldo bruto;
- saldo líquido;
- imposto provisionado;
- imposto realizado;
- conciliação;
- modelagem de domínio;
- motores tributários;
- arquitetura de sistemas.

---

## Forma de estudo

Cada produto deve ser analisado utilizando a mesma sequência:

```text
1. Entender o produto
2. Identificar o investidor
3. Identificar os eventos financeiros
4. Identificar o fato gerador
5. Identificar a base de cálculo
6. Identificar a alíquota
7. Identificar retenções
8. Identificar isenções
9. Identificar compensações
10. Calcular o resultado líquido
11. Entender quem deve reter ou recolher
12. Modelar a regra em um sistema financeiro
```

---

## Perspectiva de desenvolvimento de software

Além da teoria tributária, este repositório procura relacionar os conceitos com modelagem de sistemas.

Exemplos de entidades e conceitos que podem aparecer:

```text
Investor
Instrument
Position
Transaction
TaxEvent
TaxRule
TaxBase
TaxRate
TaxCalculation
WithholdingTax
TaxPeriod
Settlement
Income
CorporateAction
```

Um motor tributário real normalmente precisa considerar muito mais do que uma simples função:

```csharp
decimal CalcularImposto(Operacao operacao)
```

Dependendo do produto, o cálculo pode exigir:

```text
Operação atual
+
Histórico de operações
+
Período de apuração
+
Ganhos acumulados
+
Perdas acumuladas
+
IRRF acumulado
+
Custos
+
Isenções
+
Regime tributário
```

Por isso, tributação deve ser tratada como **regra de domínio**.

---

## Conceitos-chave

Algumas distinções que aparecem em praticamente todos os módulos:

```text
Principal != Rendimento

Saldo bruto != Saldo líquido

IR calculado != IRRF

Posição != Movimentação

Movimentação != Evento tributário

Rendimento econômico != Imposto realizado

Valor de venda != Ganho tributável
```

Essas diferenças são especialmente importantes em sistemas de back office.

---

## Referências oficiais

As principais fontes utilizadas neste projeto são documentos e páginas oficiais da Receita Federal.

### Receita Federal — Tributação

https://www.gov.br/receitafederal/pt-br/assuntos/meu-imposto-de-renda/tabelas/2026

### Receita Federal — Rendimentos do Capital

https://www.gov.br/receitafederal/pt-br/assuntos/meu-imposto-de-renda/preenchimento/manual-mir/rendimentos/rendimentos-do-capital

### Receita Federal — Bens Financeiros

https://www.gov.br/receitafederal/pt-br/assuntos/meu-imposto-de-renda/preenchimento/manual-mir/patrimonio/bens-financeiros

### Receita Federal — Eventos do Patrimônio

https://www.gov.br/receitafederal/pt-br/assuntos/meu-imposto-de-renda/preenchimento/manual-mir/patrimonio/eventos-do-patrimonio

### Receita Federal — Renda Variável

https://www.gov.br/receitafederal/pt-br/assuntos/meu-imposto-de-renda/pagamento/renda-variavel/bolsa-de-valores-1

### Receita Federal — Retenções em Bolsa

https://www.gov.br/receitafederal/pt-br/assuntos/meu-imposto-de-renda/pagamento/renda-variavel/bolsa-de-valores-1/retencoes

---

## Roadmap

- [x] Introdução
- [x] Parte I — Fundamentos
- [ ] Parte II — Renda Fixa
- [ ] Parte III — Fundos de Investimento
- [ ] Parte IV — Renda Variável
- [ ] Parte V — Operações Avançadas
- [ ] Parte VI — Tributação aplicada ao Back Office
- [ ] Exemplos práticos em C#
- [ ] Exemplos práticos em Java
- [ ] Exemplos práticos em Python
- [ ] Diagramas de domínio
- [ ] Casos de teste tributários
- [ ] Glossário
- [ ] Exercícios

---

## Aviso importante

Este repositório possui finalidade **educacional e técnica**.

O conteúdo não deve ser utilizado como única fonte para:

- apuração fiscal real;
- declaração de Imposto de Renda;
- desenvolvimento de sistemas tributários produtivos;
- definição de procedimentos fiscais;
- parecer jurídico ou contábil.

Antes de utilizar qualquer regra em ambiente produtivo, valide:

- legislação vigente;
- instruções normativas;
- atos da Receita Federal;
- documentação oficial do produto;
- regras internas da instituição;
- orientações das áreas jurídica, fiscal ou de compliance.

---

## Status

Projeto em construção contínua.

O conteúdo será atualizado conforme o avanço dos estudos e a evolução das regras tributárias.
