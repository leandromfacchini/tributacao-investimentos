# Aula 1 — Fundamentos da tributação de investimentos

Nesta primeira aula, o objetivo não é decorar alíquotas. Quero que você consiga olhar para uma movimentação financeira e responder:

**“Qual foi o rendimento? Houve fato gerador? Qual é a base de cálculo? Quem calcula o imposto? Quem retém? Quanto fica líquido?”**

Essas perguntas vão se repetir em praticamente todos os produtos que estudarmos.

As regras que vou usar aqui foram conferidas nas fontes da Receita Federal vigentes em 2026. Para renda variável, por exemplo, continuam documentadas as alíquotas de **15% para operações comuns e 20% para day trade**.

Referência:

https://www.gov.br/receitafederal/pt-br/assuntos/meu-imposto-de-renda/pagamento/renda-variavel/bolsa-de-valores-1

---

## 1. Primeiro: patrimônio não é rendimento

Imagine que um cliente aplique:

```text
R$ 100.000
```

Depois de algum tempo, sua posição vale:

```text
R$ 110.000
```

Temos três informações diferentes:

```text
Capital aplicado   = R$ 100.000
Saldo bruto        = R$ 110.000
Rendimento bruto   = R$  10.000
```

Ou:

\[
Rendimento = SaldoAtual - CapitalAplicado
\]

Portanto:

\[
110.000 - 100.000 = 10.000
\]

Parece trivial, mas essa separação é fundamental.

O IR normalmente **não incide sobre os R$ 110.000**.

O que nos interessa inicialmente são os **R$ 10.000 de rendimento**.

---

# 2. Saldo bruto

Vamos definir formalmente.

**Saldo bruto** é o valor da posição antes de descontarmos eventuais impostos relacionados ao rendimento.

Exemplo:

```text
Aplicação inicial       R$ 100.000
Rendimento acumulado    R$  10.000
----------------------------------
Saldo bruto             R$ 110.000
```

Em um sistema você poderia encontrar algo conceitualmente semelhante a:

```text
Principal
GrossIncome
GrossBalance
```

Ou:

```text
principal         = 100000
gross_income      = 10000
gross_balance     = 110000
```

Mas isso ainda não significa que o cliente possui R$ 110.000 líquidos disponíveis depois da tributação.

---

# 3. Rendimento bruto

O **rendimento bruto** representa quanto o capital produziu antes da tributação.

No nosso exemplo:

```text
Capital       = R$ 100.000
Saldo bruto   = R$ 110.000

Rendimento    = R$ 10.000
```

Agora começa a pergunta tributária:

> Esses R$ 10 mil são tributáveis?

A resposta depende do **produto** e de outras condições.

Por exemplo, renda fixa tributável pode ter IR.

Já certas aplicações possuem rendimentos isentos para pessoa física.

É por isso que futuramente nossa `TaxRule` não poderá simplesmente olhar para o valor do rendimento.

Ela precisará saber algo como:

```text
Produto
Tipo de investidor
Data de aplicação
Data do evento
Tipo de evento
Prazo
Regime tributário
```

---

# 4. Fato gerador

Este é um dos conceitos mais importantes de toda a trilha.

**Fato gerador** é o acontecimento previsto pela regra tributária que faz surgir a obrigação tributária.

Não basta existir valorização.

Precisamos saber se ocorreu o evento que provoca a incidência do imposto.

Isso será extremamente importante no back office.

Imagine um CDB:

```text
01/01
Aplicação: R$ 100.000

↓

30/06
Valor atualizado: R$ 108.000
```

A aplicação valorizou R$ 8.000.

Mas agora precisamos perguntar:

> Houve resgate, vencimento ou algum outro evento tributável?

A Receita lista, para aplicações financeiras de renda fixa, eventos como **alienação, liquidação total ou parcial, resgate, cessão ou repactuação**, entre outras situações que podem gerar rendimento.

Referência:

https://www.gov.br/receitafederal/pt-br/assuntos/meu-imposto-de-renda/preenchimento/manual-mir/rendimentos/rendimentos-do-capital

Essa diferença é importantíssima.

---

# 5. Rendimento econômico × evento tributário

Imagine:

```text
Aplicado                  R$100.000
Valor atualizado          R$110.000
Rendimento econômico       R$10.000
```

Podemos ter uma valorização da posição.

Mas o sistema tributário precisa saber:

```text
O rendimento foi realizado?
        ↓
Qual foi o evento?
        ↓
Esse evento é tributável?
```

Isso nos leva a uma ideia muito útil:

```text
POSIÇÃO
≠
MOVIMENTAÇÃO
≠
EVENTO TRIBUTÁRIO
```

Essa distinção vai aparecer bastante quando entrarmos em fundos, títulos, ações e eventos corporativos.

---

# 6. Base de cálculo

Agora chegamos ao valor sobre o qual o imposto será calculado.

Chamamos isso de:

**base de cálculo.**

Simplificando:

```text
Imposto = Base de cálculo × Alíquota
```

Suponha que um investimento tenha:

```text
Aplicação       R$100.000
Resgate         R$110.000
Rendimento       R$10.000
```

Se todo o rendimento for tributável:

```text
Base de cálculo = R$10.000
```

E não:

```text
Base de cálculo = R$110.000
```

Essa diferença é essencial.

---

# 7. Alíquota

A alíquota é simplesmente a porcentagem aplicada à base de cálculo.

Imagine:

```text
Base de cálculo = R$10.000
Alíquota        = 20%
```

Então:

\[
IR = 10.000 \times 0,20
\]

Resultado:

```text
IR = R$2.000
```

Consequentemente:

```text
Rendimento bruto        R$10.000
IR                     -R$ 2.000
--------------------------------
Rendimento líquido      R$ 8.000
```

E:

```text
Principal               R$100.000
Rendimento líquido      R$  8.000
---------------------------------
Saldo líquido           R$108.000
```

Agora começamos a ter uma cadeia completa.

---

# 8. Primeiro modelo mental

Guarde isto:

```text
Capital
   ↓
Rendimento
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

Eu gostaria que isso se tornasse quase automático para você.

---

# 9. IRRF

Agora entra outro conceito muito importante:

**IRRF = Imposto sobre a Renda Retido na Fonte.**

Isso significa que outra entidade realiza a retenção do imposto.

Por exemplo, em várias aplicações financeiras existe uma fonte pagadora responsável pela retenção.

Isso é diferente de simplesmente dizer:

> “o cliente deve imposto”.

Podemos ter:

```text
Imposto devido
```

e:

```text
Imposto já retido
```

São conceitos diferentes.

---

# 10. IRRF × IR devido

Essa diferença é fundamental no mercado financeiro.

Considere:

```text
Imposto apurado          R$1.500
IRRF já retido           R$   50
```

Então pode existir algo conceitualmente semelhante a:

```text
Imposto a recolher =
Imposto apurado - IRRF aproveitável
```

Nesse exemplo simplificado:

```text
1.500 - 50 = R$1.450
```

Por isso você provavelmente encontrará em sistemas financeiros estruturas diferentes para:

```text
TaxCalculated
TaxWithheld
TaxDue
```

Eles não representam necessariamente a mesma coisa.

---

# 11. Um ótimo exemplo disso são as ações

Vamos comparar renda fixa e ações.

Imagine:

```text
Compra de ações: R$40.000
Venda:            R$50.000
```

Ignorando custos por enquanto:

```text
Ganho líquido = 50.000 - 40.000

Ganho = R$10.000
```

Para uma operação comum tributável:

```text
Alíquota = 15%
```

Então:

```text
10.000 × 15%

IR apurado = R$1.500
```

A Receita mantém em 2026 a alíquota de **15% para operações comuns** e **20% para day trade**.

Referência:

https://www.gov.br/receitafederal/pt-br/assuntos/meu-imposto-de-renda/pagamento/renda-variavel/bolsa-de-valores-1

Mas existe outro detalhe.

---

# 12. IRRF das operações comuns

Nas operações comuns em bolsa existe uma pequena retenção de IR na fonte.

Atualmente:

**0,005% sobre o valor da venda.**

No day trade:

**1% sobre o resultado líquido da operação.**

Referência:

https://www.gov.br/receitafederal/pt-br/assuntos/meu-imposto-de-renda/pagamento/renda-variavel/bolsa-de-valores-1/retencoes

Veja como é interessante.

Venda:

```text
R$50.000
```

IRRF da operação comum:

\[
50.000 \times 0,005\%
\]

Precisamos converter:

\[
0,005\% = 0,00005
\]

Então:

\[
50.000 \times 0,00005 = 2,50
\]

Logo:

```text
IRRF = R$2,50
```

Mas o imposto calculado sobre o lucro era:

```text
R$1.500
```

Então perceba:

```text
IR devido calculado    R$1.500,00

IRRF                     R$2,50
```

O IRRF não representa o imposto completo.

A própria Receita explica que essa retenção pode ser deduzida do imposto apurado sobre os ganhos líquidos.

Referência:

https://www.gov.br/receitafederal/pt-br/assuntos/meu-imposto-de-renda/pagamento/renda-variavel/bolsa-de-valores-1

---

# 13. Por que existe esse IRRF tão pequeno?

É por isso que você talvez já tenha ouvido a expressão:

> **“dedo-duro”.**

A retenção deixa um registro tributário da operação.

Mas para nós o importante tecnicamente é separar:

```text
IRRF
```

de:

```text
IR apurado
```

e:

```text
IR efetivamente recolhido.
```

São três informações diferentes.

---

# 14. Compare CDB e ações

Agora começa a parte realmente importante.

## CDB

Imagine:

```text
Aplicação     R$100.000
Resgate       R$110.000
```

Temos:

```text
Principal               100.000
Rendimento               10.000
```

Suponha, apenas para nosso exemplo, que a alíquota aplicável seja 20%.

```text
IR = 10.000 × 20%

IR = R$2.000
```

Então:

```text
Valor bruto            R$110.000
IR                    -R$  2.000
--------------------------------
Valor líquido          R$108.000
```

Aqui a instituição financeira realiza a retenção correspondente na fonte.

Para aplicações de renda fixa em geral, a Receita mantém a estrutura regressiva que estudaremos detalhadamente na Aula 2.

Referência:

https://www.gov.br/receitafederal/pt-br/assuntos/meu-imposto-de-renda/tabelas/2025

---

# 15. Ação

Agora:

```text
Compra      R$100.000
Venda       R$110.000
```

Ganho:

```text
R$10.000
```

Se for uma operação comum tributável:

```text
10.000 × 15%

IR = R$1.500
```

Mas há uma diferença operacional importante.

A corretora não simplesmente retém os R$1.500 inteiros daquela venda.

Ela realiza a retenção de IRRF prevista para a operação, enquanto o contribuinte apura seus ganhos líquidos no período. A Receita inclusive disponibiliza atualmente o **ReVar** para auxiliar na apuração da renda variável e geração do DARF.

Referência:

https://www.gov.br/pt-br/servicos/apurar-imposto-sobre-renda-variavel

Veja a mudança de responsabilidade:

### Renda fixa

```text
Evento
 ↓
Fonte pagadora calcula/retem
 ↓
Cliente recebe líquido
```

### Bolsa

```text
Operações
 ↓
Corretora informa/retem IRRF
 ↓
Ganhos e perdas são apurados
 ↓
Imposto mensal é determinado
 ↓
Contribuinte recolhe o necessário
```

Essa diferença é enorme para sistemas financeiros.

---

# 16. Agora introduzimos custo

Até agora fizemos:

```text
Venda - Compra
```

Mas renda variável é um pouco mais interessante.

A Receita considera despesas efetivamente pagas, como corretagem, liquidação e emolumentos, na determinação do ganho líquido: despesas da compra podem compor o custo e despesas da venda podem reduzir o valor líquido da alienação.

Referência:

https://www.gov.br/receitafederal/pt-br/assuntos/meu-imposto-de-renda/pagamento/renda-variavel/bolsa-de-valores-1

Imagine:

```text
Compra                     R$40.000
Custos da compra           R$   100
```

Nosso custo passa a ser:

```text
R$40.100
```

Venda:

```text
R$50.000
```

Custos da venda:

```text
R$100
```

Valor líquido da venda:

```text
R$49.900
```

Ganho:

```text
49.900 - 40.100

= R$9.800
```

Não:

```text
R$10.000
```

Isso nos leva a outro conceito importante.

---

# 17. Custo de aquisição

Para renda variável você encontrará constantemente:

**custo de aquisição.**

Não basta guardar:

```text
quantidade = 100
preço = R$50
```

O sistema precisa acompanhar adequadamente o custo.

Por exemplo:

```text
100 ações × R$50
= R$5.000
```

Mais custos elegíveis:

```text
R$20
```

Então:

```text
Custo de aquisição = R$5.020
```

Quando vendermos esse ativo, precisaremos conhecer o custo correspondente para determinar o ganho.

Isso vai nos levar futuramente a:

**preço médio.**

---

# 18. Lucro não é a mesma coisa que rendimento de renda fixa

Essa distinção de vocabulário ajuda muito.

No CDB pensamos normalmente:

```text
Principal
+
Rendimento
```

Nas ações pensamos:

```text
Valor da alienação
-
Custo de aquisição
=
Ganho ou perda
```

Portanto:

### Renda fixa

```text
Aplicação → rendimento
```

### Renda variável

```text
Aquisição → alienação → ganho/perda
```

Essa diferença conceitual aparecerá constantemente no código e nos bancos de dados financeiros.

---

# 19. Prejuízo

Agora temos outro cenário.

```text
Compra     R$50.000
Venda      R$45.000
```

Resultado:

```text
45.000 - 50.000 = -5.000
```

Temos:

```text
Prejuízo = R$5.000
```

Em determinadas condições esse prejuízo poderá ser compensado contra ganhos futuros da mesma categoria tributária.

A Receita explicitamente informa que perdas podem ser usadas na compensação de ganhos futuros, observadas as regras aplicáveis.

Referência:

https://www.gov.br/receitafederal/pt-br/assuntos/meu-imposto-de-renda/pagamento/renda-variavel/bolsa-de-valores-1

Isso introduz uma característica extremamente importante:

> Tributação nem sempre depende apenas da operação atual.

Pode existir **estado tributário acumulado**.

---

# 20. Pense como desenvolvedor agora

Imagine uma função:

```csharp
decimal CalcularImposto(Operacao operacao)
```

Parece suficiente.

Mas não é.

Porque para renda variável poderíamos precisar saber:

```text
Operação atual
+
outras operações do mês
+
prejuízos acumulados
+
IRRF acumulado
+
tipo de operação
+
custos
+
isenções aplicáveis
```

Logo, um domínio mais realista começa a parecer:

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

Já estamos saindo de:

```text
if produto == ação
    imposto = lucro * 0.15
```

e entrando em modelagem de domínio.

---

# 21. Outro conceito importante: período de apuração

Imagine:

### Janeiro

```text
Operação A     +R$10.000
Operação B     -R$ 4.000
```

Resultado líquido:

```text
R$6.000
```

Não faria sentido simplesmente calcular:

```text
10.000 × 15%
```

e ignorar a operação B, quando a legislação permite aquela compensação.

O cálculo precisa observar o **período de apuração e as regras de compensação**.

Por isso sistemas financeiros frequentemente trabalham com conceitos semelhantes a:

```text
TaxPeriod
ReferenceMonth
AccumulatedLoss
```

---

# 22. Provisão × realização

Esse conceito é especialmente relevante para sistemas.

Imagine novamente:

```text
Aplicação      R$100.000
Saldo atual    R$110.000
```

Existem R$10.000 de rendimento econômico.

Um sistema pode estimar:

```text
IR estimado = R$2.000
```

para exibir:

```text
Saldo bruto      R$110.000
Saldo líquido    R$108.000
```

Mas isso não significa necessariamente que o imposto já tenha sido efetivamente retido.

Podemos ter:

```text
IR provisionado/estimado
```

versus:

```text
IR realizado/retido
```

Essa diferença é muito importante em carteiras e relatórios.

---

# 23. Cinco valores que você nunca deve misturar

Imagine um investimento.

```text
1. Principal

2. Saldo bruto

3. Rendimento bruto

4. Imposto

5. Saldo líquido
```

Exemplo:

```text
Principal                  100.000
Rendimento bruto            10.000
----------------------------------
Saldo bruto                110.000

IR                           2.000
----------------------------------
Saldo líquido              108.000
```

E:

```text
Rendimento líquido = 8.000
```

Então:

\[
SaldoLiquido =
Principal + RendimentoLiquido
\]

---

# 24. Mas cuidado com “saldo”

No trabalho, quando alguém disser:

> “Qual é o saldo do cliente?”

A primeira pergunta mental deve ser:

**Qual saldo?**

Pode ser:

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

Em sistemas financeiros, “saldo” sozinho quase nunca é informação suficiente.

---

# 25. Nossa primeira árvore de decisão tributária

Quando você receber qualquer produto, pense:

```text
               Houve rendimento/ganho?
                       │
              ┌────────┴────────┐
             NÃO               SIM
                              │
                       Houve fato gerador?
                              │
                     ┌────────┴───────┐
                    NÃO              SIM
                                      │
                               É tributável?
                                      │
                           ┌──────────┴────────┐
                          NÃO                 SIM
                                              │
                                      Base de cálculo
                                              │
                                           Alíquota
                                              │
                                        Imposto devido
                                              │
                                    Existe IRRF/antecipação?
```

Isso é muito melhor do que decorar centenas de regras isoladas.

---

# 26. Exercício resolvido — CDB

Imagine:

```text
Aplicação:     R$50.000
Resgate:       R$56.000
```

Primeiro:

\[
56.000 - 50.000 = 6.000
\]

Rendimento:

```text
R$6.000
```

Suponha alíquota aplicável de:

```text
17,5%
```

Então:

\[
6.000 \times 0,175 = 1.050
\]

IR:

```text
R$1.050
```

Rendimento líquido:

```text
6.000 - 1.050
= R$4.950
```

Valor líquido:

```text
50.000 + 4.950
= R$54.950
```

Modelo:

```text
Principal               50.000
      ↓
Rendimento               6.000
      ↓
Base tributável          6.000
      ↓
IR                        1.050
      ↓
Rendimento líquido       4.950
      ↓
Resgate líquido         54.950
```

---

# 27. Exercício resolvido — ações

Agora:

```text
Compra        R$50.000
Venda         R$56.000
```

Suponha operação comum tributável e, para simplificar, sem despesas.

Ganho:

```text
R$6.000
```

Alíquota:

```text
15%
```

IR apurado:

\[
6.000 \times 0,15 = 900
\]

Resultado:

```text
IR apurado = R$900
```

Mas IRRF sobre a venda:

\[
56.000 \times 0,005\%
\]

\[
56.000 \times 0,00005 = 2,80
\]

Então temos dois números:

```text
IR apurado      R$900,00
IRRF              R$2,80
```

E não:

```text
IR = R$2,80
```

Esse é exatamente o tipo de distinção que você precisa dominar no trabalho.

---

# 28. O que você deve sair sabendo desta aula

Se alguém disser:

> “Esse investimento rendeu R$ 10 mil.”

Você ainda **não tem informação suficiente para calcular o imposto**.

Precisamos descobrir:

```text
Qual produto?
Quem é o investidor?
Qual regime tributário?
Qual foi o evento?
Quando ocorreu?
Houve fato gerador?
Qual é a base?
Qual é a alíquota?
Há isenção?
Existe IRRF?
Existem perdas compensáveis?
Quem é responsável pela retenção/recolhimento?
```

Essa é a mentalidade correta.

---

# Seu mapa mental da Aula 1

Guarde este fluxo:

```text
                    INVESTIMENTO
                         │
                         ▼
                       SALDO
                         │
                         ▼
                  RENDIMENTO/GANHO
                         │
                         ▼
                      EVENTO
                         │
                         ▼
                   FATO GERADOR
                         │
                         ▼
                  BASE DE CÁLCULO
                         │
                         ▼
                     ALÍQUOTA
                         │
                         ▼
                 IMPOSTO APURADO
                         │
              ┌──────────┴──────────┐
              ▼                     ▼
            IRRF              COMPENSAÇÕES
              │                     │
              └──────────┬──────────┘
                         ▼
                 IMPOSTO A PAGAR
                         │
                         ▼
                 RESULTADO LÍQUIDO
```

E a principal conclusão da Aula 1 é:

> **Tributação de investimentos não começa pela alíquota. Começa identificando produto, evento, rendimento/ganho e fato gerador.**

Na **Aula 2**, entramos de vez em **renda fixa**, construindo uma matriz para **CDB, RDB, Tesouro Direto, LCI, LCA, CRI, CRA e debêntures**, incluindo tabela regressiva, IOF, isenções, vencimento, resgate e exemplos de cálculo. Será nosso primeiro módulo realmente focado em regras produto por produto.
