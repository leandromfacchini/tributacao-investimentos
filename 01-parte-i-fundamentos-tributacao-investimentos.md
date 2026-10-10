# Parte I — Fundamentos da Tributação de Investimentos

> Material de estudo voltado para desenvolvimento e back office de instituições financeiras.
>
> **Versão de referência:** outubro de 2026

---

# 1. Objetivo

Antes de estudar CDB, Tesouro, ações, fundos, FII ou derivativos, é necessário dominar os conceitos fundamentais utilizados na tributação.

Ao final desta parte, você deve conseguir analisar uma operação financeira e identificar:

- principal;
- saldo bruto;
- rendimento;
- ganho ou perda;
- fato gerador;
- base de cálculo;
- alíquota;
- IR;
- IRRF;
- imposto devido;
- saldo líquido;
- custo de aquisição;
- período de apuração;
- compensação de prejuízos;
- imposto provisionado;
- imposto realizado.

---

# 2. Patrimônio, principal e saldo

## 2.1 Principal

Principal é o capital inicialmente investido.

Exemplo:

```text
Aplicação inicial = R$ 100.000
```

Neste caso:

```text
Principal = R$ 100.000
```

---

## 2.2 Saldo bruto

Saldo bruto é o valor da posição antes de considerar os impostos incidentes sobre o rendimento.

Exemplo:

```text
Principal              R$ 100.000
Rendimento acumulado   R$  10.000
---------------------------------
Saldo bruto            R$ 110.000
```

Podemos representar:

```text
Saldo bruto = Principal + Rendimento bruto
```

---

# 3. Rendimento

Rendimento representa a remuneração produzida pelo capital.

Em uma situação simplificada:

```text
Rendimento = Saldo atual - Principal
```

Exemplo:

```text
Principal      R$ 100.000
Saldo bruto    R$ 110.000
```

Logo:

```text
Rendimento = 110.000 - 100.000

Rendimento = R$ 10.000
```

Um erro comum é calcular o imposto sobre o saldo total.

Normalmente, em uma aplicação tributável, o foco está no **rendimento**, e não no capital originalmente investido.

---

# 4. Rendimento bruto e rendimento líquido

## Rendimento bruto

Valor produzido antes dos impostos.

## Rendimento líquido

Valor restante depois dos impostos aplicáveis.

Exemplo:

```text
Rendimento bruto        R$ 10.000
IR                     -R$  2.000
---------------------------------
Rendimento líquido      R$  8.000
```

Assim:

```text
Saldo líquido = Principal + Rendimento líquido
```

No exemplo:

```text
100.000 + 8.000 = R$ 108.000
```

---

# 5. Saldo bruto e saldo líquido

Considere:

```text
Principal                 R$ 100.000
Rendimento bruto          R$  10.000
------------------------------------
Saldo bruto               R$ 110.000

IR                        R$   2.000
------------------------------------
Saldo líquido             R$ 108.000
```

Portanto:

```text
Saldo bruto != Saldo líquido
```

Isso parece simples, mas é extremamente importante em sistemas financeiros.

---

# 6. O termo "saldo" pode ser ambíguo

Em sistemas de back office, a palavra **saldo** pode representar coisas diferentes.

Exemplos:

```text
Saldo contábil
Saldo financeiro
Saldo bruto
Saldo líquido
Saldo disponível
Saldo bloqueado
Saldo em liquidação
Saldo de custódia
```

Portanto, ao trabalhar com APIs, bancos de dados ou regras de negócio, evite campos genéricos como:

```text
balance
```

quando o domínio exige algo mais específico.

É preferível algo como:

```text
gross_balance
net_balance
available_balance
blocked_balance
settled_balance
```

---

# 7. Fato gerador

Fato gerador é o acontecimento previsto na legislação que dá origem à obrigação tributária.

Uma valorização econômica não significa necessariamente que o imposto já tenha sido efetivamente retido ou realizado.

Considere:

```text
Aplicação inicial       R$ 100.000
Valor atualizado        R$ 108.000
```

Existe:

```text
Rendimento econômico = R$ 8.000
```

Mas ainda precisamos perguntar:

```text
Houve resgate?
Houve vencimento?
Houve alienação?
Houve amortização?
Houve distribuição?
Houve outro evento tributável?
```

A Receita Federal relaciona, entre os rendimentos de aplicações financeiras de renda fixa, eventos como:

- alienação;
- liquidação total ou parcial;
- resgate;
- cessão;
- repactuação;
- rendimentos periódicos;
- outras formas de remuneração previstas.

---

# 8. Posição, movimentação e evento tributário

Esses conceitos não devem ser confundidos.

```text
POSIÇÃO
   !=
MOVIMENTAÇÃO
   !=
EVENTO TRIBUTÁRIO
```

## Posição

Representa aquilo que o investidor possui em determinado momento.

## Movimentação

Representa uma alteração registrada no ativo ou no financeiro.

## Evento tributário

Evento que pode produzir consequência fiscal.

Uma movimentação pode alterar a posição sem necessariamente produzir imediatamente uma obrigação tributária.

---

# 9. Base de cálculo

Base de cálculo é o valor sobre o qual a alíquota será aplicada.

De forma simplificada:

```text
Imposto = Base de cálculo × Alíquota
```

Exemplo:

```text
Aplicação          R$ 100.000
Resgate            R$ 110.000
Rendimento         R$  10.000
```

Se todo o rendimento for tributável:

```text
Base de cálculo = R$ 10.000
```

e não:

```text
Base de cálculo = R$ 110.000
```

---

# 10. Alíquota

Alíquota é o percentual utilizado para determinar o imposto.

Exemplo:

```text
Base de cálculo = R$ 10.000
Alíquota        = 20%
```

Cálculo:

```text
IR = 10.000 × 0,20

IR = R$ 2.000
```

Resultado:

```text
Rendimento bruto        R$ 10.000
IR                     -R$  2.000
---------------------------------
Rendimento líquido      R$  8.000
```

---

# 11. Fluxo tributário básico

```text
Capital
   ↓
Rendimento / Ganho
   ↓
Evento
   ↓
Fato gerador
   ↓
Base de cálculo
   ↓
Alíquota
   ↓
Imposto
   ↓
Rendimento líquido
```

Esse fluxo deve ser utilizado como ponto de partida para qualquer produto.

---

# 12. IR e IRRF

## 12.1 IR

IR representa o Imposto sobre a Renda apurado segundo as regras aplicáveis.

## 12.2 IRRF

IRRF significa:

> Imposto sobre a Renda Retido na Fonte.

Nesse caso, existe uma fonte responsável por efetuar a retenção prevista na legislação.

É importante diferenciar:

```text
Imposto calculado
Imposto retido
Imposto a recolher
```

Eles não são necessariamente o mesmo valor.

---

# 13. IRRF versus imposto devido

Exemplo conceitual:

```text
Imposto apurado          R$ 1.500
IRRF aproveitável       -R$    50
---------------------------------
Saldo de imposto         R$ 1.450
```

Em sistemas, podemos encontrar conceitos semelhantes a:

```text
TaxCalculated
TaxWithheld
TaxDue
```

Esses campos devem possuir significados bem definidos.

---

# 14. Exemplo de renda fixa

Considere:

```text
Aplicação    R$ 100.000
Resgate      R$ 110.000
```

Rendimento:

```text
110.000 - 100.000 = R$ 10.000
```

Suponha, apenas para o exemplo, uma alíquota aplicável de 20%.

```text
IR = 10.000 × 20%

IR = R$ 2.000
```

Resultado:

```text
Principal               R$ 100.000
Rendimento bruto        R$  10.000
IR                     -R$   2.000
----------------------------------
Rendimento líquido      R$   8.000
Saldo líquido           R$ 108.000
```

Nas aplicações de renda fixa em geral, a Receita Federal publica atualmente a tabela regressiva:

| Prazo | Alíquota |
|---|---:|
| Até 180 dias | 22,5% |
| De 181 a 360 dias | 20,0% |
| De 361 a 720 dias | 17,5% |
| Acima de 720 dias | 15,0% |

As particularidades serão estudadas no módulo de renda fixa.

---

# 15. Ganho e perda em renda variável

Na renda variável, normalmente trabalhamos com conceitos como:

```text
Aquisição
Alienação
Custo de aquisição
Ganho
Perda
```

Em uma simplificação:

```text
Ganho = Valor líquido de alienação - Custo de aquisição
```

---

# 16. Exemplo de ganho em ações

Considere:

```text
Compra      R$ 40.000
Venda       R$ 50.000
```

Ignorando custos:

```text
Ganho = 50.000 - 40.000

Ganho = R$ 10.000
```

Em uma operação comum tributável, a Receita Federal informa atualmente alíquota de:

```text
15%
```

Assim:

```text
10.000 × 15% = R$ 1.500
```

---

# 17. IRRF em bolsa

A Receita Federal publica atualmente:

## Operações comuns

```text
IRRF = 0,005% sobre o valor da venda
```

## Day trade

```text
IRRF = 1% sobre o resultado líquido das operações day trade do dia
```

O IRRF pode funcionar como antecipação e ser deduzido do imposto apurado, observadas as regras aplicáveis.

---

# 18. Exemplo de IRRF em operação comum

Venda:

```text
R$ 50.000
```

IRRF:

```text
50.000 × 0,005%
```

Como:

```text
0,005% = 0,00005
```

Temos:

```text
50.000 × 0,00005 = R$ 2,50
```

Se o ganho tributável fosse:

```text
R$ 10.000
```

e o imposto apurado:

```text
R$ 1.500
```

teríamos:

```text
IR apurado      R$ 1.500,00
IRRF            R$     2,50
```

O IRRF de R$ 2,50 **não representa o imposto total da operação**.

---

# 19. Custo de aquisição

O custo de aquisição é fundamental na renda variável.

Não basta armazenar:

```text
Quantidade
Preço unitário
```

É necessário considerar os elementos que compõem o custo conforme as regras aplicáveis.

Exemplo simplificado:

```text
Compra                    R$ 40.000
Custos relacionados       R$    100
-----------------------------------
Custo de aquisição        R$ 40.100
```

Venda:

```text
Valor bruto               R$ 50.000
Custos da venda           R$    100
-----------------------------------
Valor líquido             R$ 49.900
```

Ganho:

```text
49.900 - 40.100 = R$ 9.800
```

Portanto:

```text
Ganho tributável != simplesmente preço de venda - preço bruto de compra
```

---

# 20. Rendimento versus ganho

Essa distinção ajuda a entender os produtos.

## Renda fixa

Pensamos normalmente em:

```text
Principal
+
Rendimento
```

## Renda variável

Pensamos normalmente em:

```text
Aquisição
↓
Custo de aquisição
↓
Alienação
↓
Ganho ou perda
```

---

# 21. Prejuízo

Considere:

```text
Compra        R$ 50.000
Venda         R$ 45.000
```

Resultado:

```text
45.000 - 50.000 = -5.000
```

Logo:

```text
Prejuízo = R$ 5.000
```

Em determinadas situações, perdas podem ser compensadas com ganhos futuros, observadas:

- a modalidade da operação;
- o período;
- as regras legais;
- a segregação entre categorias tributárias.

A Receita Federal mantém campos específicos para informação de prejuízos anteriores em renda variável.

---

# 22. Estado tributário acumulado

Uma das principais diferenças entre um cálculo simples e um sistema tributário real é que o imposto nem sempre depende apenas da operação atual.

Um cálculo pode depender de:

```text
Operação atual
+
Outras operações do mês
+
Ganhos acumulados
+
Perdas acumuladas
+
IRRF acumulado
+
Tipo de operação
+
Custos
+
Isenções
```

Isso significa que o domínio possui **estado**.

---

# 23. Período de apuração

Considere um mês com:

```text
Operação A      +R$ 10.000
Operação B      -R$  4.000
```

Resultado líquido simplificado:

```text
R$ 6.000
```

Dependendo das regras aplicáveis, as operações precisam ser analisadas conjuntamente dentro do período de apuração.

Em modelagem de software, isso pode levar a objetos como:

```text
TaxPeriod
ReferenceMonth
Gains
Losses
LossCarryforward
WithholdingTax
TaxDue
```

---

# 24. Provisão versus realização

Considere uma posição:

```text
Aplicação             R$ 100.000
Valor atualizado      R$ 110.000
```

O sistema pode exibir um imposto estimado:

```text
IR estimado           R$ 2.000
```

e um saldo líquido estimado:

```text
Saldo líquido         R$ 108.000
```

Isso não significa necessariamente que o imposto já foi efetivamente retido.

Podemos ter:

```text
Imposto provisionado / estimado
```

e:

```text
Imposto realizado / retido
```

São conceitos diferentes.

---

# 25. Cinco valores que não devem ser misturados

Em uma aplicação financeira, diferencie sempre:

```text
1. Principal
2. Saldo bruto
3. Rendimento bruto
4. Imposto
5. Saldo líquido
```

Exemplo:

```text
Principal                  R$ 100.000
Rendimento bruto           R$  10.000
-------------------------------------
Saldo bruto                R$ 110.000

IR                         R$   2.000
-------------------------------------
Saldo líquido              R$ 108.000
```

E:

```text
Rendimento líquido = R$ 8.000
```

---

# 26. Árvore de decisão tributária

```text
                 Houve rendimento ou ganho?
                         │
                ┌────────┴────────┐
               NÃO               SIM
                                  │
                           Houve fato gerador?
                                  │
                         ┌────────┴────────┐
                        NÃO               SIM
                                           │
                                    É tributável?
                                           │
                                  ┌────────┴────────┐
                                 NÃO               SIM
                                                    │
                                            Base de cálculo
                                                    │
                                                Alíquota
                                                    │
                                            Imposto apurado
                                                    │
                                      Existe IRRF / antecipação?
                                                    │
                                              Compensações
                                                    │
                                             Imposto devido
                                                    │
                                             Resultado líquido
```

---

# 27. Exemplo completo — CDB

Considere:

```text
Aplicação     R$ 50.000
Resgate       R$ 56.000
```

Rendimento:

```text
56.000 - 50.000 = R$ 6.000
```

Suponha alíquota aplicável de:

```text
17,5%
```

IR:

```text
6.000 × 0,175 = R$ 1.050
```

Rendimento líquido:

```text
6.000 - 1.050 = R$ 4.950
```

Resgate líquido:

```text
50.000 + 4.950 = R$ 54.950
```

Fluxo:

```text
Principal               R$ 50.000
        ↓
Rendimento              R$  6.000
        ↓
Base tributável         R$  6.000
        ↓
IR                      R$  1.050
        ↓
Rendimento líquido      R$  4.950
        ↓
Resgate líquido         R$ 54.950
```

---

# 28. Exemplo completo — ações

Considere:

```text
Compra       R$ 50.000
Venda        R$ 56.000
```

Suponha:

- operação comum;
- tributável;
- sem custos, apenas para simplificação.

Ganho:

```text
R$ 6.000
```

Alíquota:

```text
15%
```

Imposto apurado:

```text
6.000 × 15% = R$ 900
```

IRRF:

```text
56.000 × 0,005%
= 56.000 × 0,00005
= R$ 2,80
```

Logo:

```text
IR apurado      R$ 900,00
IRRF            R$   2,80
```

São valores com finalidades diferentes.

---

# 29. Modelagem de domínio

Uma implementação ingênua poderia começar assim:

```csharp
decimal CalcularImposto(Operacao operacao)
```

Mas um motor tributário real pode precisar de muito mais contexto:

```text
Investor
 └── TaxPeriod
      ├── Transactions
      ├── Gains
      ├── Losses
      ├── LossCarryforward
      ├── WithholdingTax
      └── TaxDue
```

Além disso:

```text
Instrument
Position
Transaction
TaxEvent
TaxRule
TaxBase
TaxRate
TaxCalculation
WithholdingTax
Settlement
Income
CorporateAction
```

A tributação deve ser tratada como **regra de domínio**, e não apenas como um conjunto de `if` e `switch`.

---

# 30. Checklist para analisar qualquer operação

Ao receber uma operação, responda:

```text
[ ] Qual é o produto?
[ ] Quem é o investidor?
[ ] Qual é a data da aquisição?
[ ] Qual foi o evento?
[ ] Houve rendimento, ganho ou perda?
[ ] Houve fato gerador?
[ ] Existe isenção?
[ ] Qual é a base de cálculo?
[ ] Qual é a alíquota?
[ ] Existe IRRF?
[ ] Existem prejuízos compensáveis?
[ ] Qual é o período de apuração?
[ ] Quem deve reter?
[ ] Quem deve recolher?
[ ] Qual é o valor bruto?
[ ] Qual é o valor líquido?
[ ] O imposto está provisionado ou realizado?
```

---

# 31. Resumo

O conceito central desta parte é:

> **Tributação de investimentos não começa pela alíquota. Começa pela identificação do produto, do investidor, do evento e do fato gerador.**

A cadeia fundamental é:

```text
Investimento
   ↓
Posição
   ↓
Rendimento / ganho / perda
   ↓
Evento
   ↓
Fato gerador
   ↓
Base de cálculo
   ↓
Alíquota
   ↓
Imposto apurado
   ↓
IRRF
   ↓
Compensações
   ↓
Imposto devido
   ↓
Resultado líquido
```

Essa estrutura será utilizada em todos os módulos seguintes.

---

# Referências oficiais

## Receita Federal — Tributação de 2026

Contém, entre outras informações, as alíquotas de aplicações de renda fixa e fundos.

https://www.gov.br/receitafederal/pt-br/assuntos/meu-imposto-de-renda/tabelas/2026

## Receita Federal — Rendimentos do Capital

Apresenta informações sobre aplicações financeiras, renda fixa e renda variável.

https://www.gov.br/receitafederal/pt-br/assuntos/meu-imposto-de-renda/preenchimento/manual-mir/rendimentos/rendimentos-do-capital

## Receita Federal — Retenções em operações de bolsa

Informações oficiais sobre IRRF em operações comuns e day trade.

https://www.gov.br/receitafederal/pt-br/assuntos/meu-imposto-de-renda/pagamento/renda-variavel/bolsa-de-valores-1/retencoes

## Receita Federal — Bens Financeiros

Classificação de aplicações, investimentos, fundos e outros ativos financeiros.

https://www.gov.br/receitafederal/pt-br/assuntos/meu-imposto-de-renda/preenchimento/manual-mir/patrimonio/bens-financeiros

## Receita Federal — Eventos do Patrimônio

Eventos relacionados a investimentos e rendimentos, incluindo aplicações isentas.

https://www.gov.br/receitafederal/pt-br/assuntos/meu-imposto-de-renda/preenchimento/manual-mir/patrimonio/eventos-do-patrimonio

---

## Aviso de manutenção

Regras tributárias podem sofrer alterações.

Ao utilizar este material como referência para:

- sistemas produtivos;
- motores de cálculo;
- conciliações fiscais;
- relatórios oficiais;
- informes de rendimentos;

sempre valide a regra contra a legislação e a documentação oficial vigente.

**Última revisão deste material: outubro de 2026.**
