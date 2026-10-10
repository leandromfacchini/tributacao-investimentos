# Introdução — Tributação de Investimentos

Material de estudo voltado para desenvolvimento e back office de instituições financeiras.

A base mental que você precisa dominar para cada produto é sempre a mesma:

**posição/saldo → rendimento → evento financeiro → fato gerador → base de cálculo → alíquota → retenção → compensação → saldo/rendimento → obrigação da instituição e do cliente**.

Isso é particularmente importante porque, no ambiente de corretora, não basta saber que “CDB paga IR” ou “LCI é isenta”. Você precisa entender **quando o imposto nasce, sobre qual valor ele incide, quem retém, como o custo é controlado e como isso aparece nos saldos e rendimentos**.

Um cuidado importante para o nosso estudo: a MP 1.303/2025 chegou a propor mudanças grandes — inclusive alíquota única para diversas aplicações —, mas **perdeu vigência em 8 de outubro de 2025**. Portanto, não devemos estudar aquelas propostas como se fossem as regras de 2026.

Referência:

https://www.planalto.gov.br/ccivil_03/_ato2023-2026/2025/congresso/adc-67-mpv1.303.htm

## O que você precisa dominar

Eu dividiria seu estudo em **8 módulos**.

| Módulo | Tema |
|---|---|
| 1 | Fundamentos tributários dos investimentos |
| 2 | Renda fixa |
| 3 | Fundos de investimento |
| 4 | Ações e mercado à vista |
| 5 | Day trade e renda variável |
| 6 | FII, FIAGRO, ETF e produtos especiais |
| 7 | Derivativos e operações mais complexas |
| 8 | Visão de back office: posição, rendimentos, eventos e IR |

A ideia não é decorar. É chegar ao ponto em que alguém no trabalho diga:

> “Precisamos calcular o rendimento líquido desse cliente no resgate.”

E automaticamente você pense:

**produto → data de aquisição → custo → rendimento → prazo → tributação → IRRF → líquido.**

---

# 1. Fundamentos — começa aqui

Antes dos produtos, você precisa dominar estes conceitos:

**Principal / capital aplicado**

Valor originalmente investido.

**Saldo bruto**

Valor atual antes da incidência dos impostos aplicáveis.

**Rendimento**

Em uma simplificação:

`Rendimento = valor atual - capital`

**Base de cálculo**

Valor sobre o qual o imposto efetivamente incidirá.

Normalmente não é o patrimônio inteiro.

Por exemplo:

- aplicação: R$ 100.000
- resgate: R$ 110.000
- rendimento: R$ 10.000

O IR não é calculado sobre R$ 110 mil.

É calculado sobre os **R$ 10 mil de rendimento**, quando aquela aplicação é tributável.

---

# 2. Renda fixa

Esse deve ser seu primeiro grande bloco.

Você deve estudar pelo menos:

**Tesouro Direto, CDB, RDB, debêntures, debêntures incentivadas, LCI, LCA, CRI, CRA, poupança e operações compromissadas.**

Aqui aparece uma das classificações fundamentais.

### Tributados

Em linhas gerais, títulos como **CDB e diversos títulos de renda fixa tributáveis** seguem a tabela regressiva de IR para pessoa física.

| Prazo | IR |
|---|---:|
| até 180 dias | 22,5% |
| 181–360 dias | 20% |
| 361–720 dias | 17,5% |
| acima de 720 dias | 15% |

Essa lógica também aparece na tributação de determinados fundos de longo prazo. A Receita continua documentando em 2026 essas faixas de 22,5%, 20%, 17,5% e 15%.

Referência:

https://www.gov.br/receitafederal/pt-br/centrais-de-conteudo/publicacoes/perguntas-e-respostas/dirpf/p-r-irpf-2026-v1-00-2026-04-23.pdf

Aqui quero que você aprenda principalmente a distinguir:

**saldo bruto ≠ rendimento bruto ≠ IR ≠ rendimento líquido ≠ saldo líquido.**

Por exemplo:

Capital:

**R$ 100.000**

Valor no resgate:

**R$ 112.000**

Rendimento:

**R$ 12.000**

Suponha IR de 17,5%.

IR:

`12.000 × 17,5% = R$ 2.100`

Rendimento líquido:

`12.000 - 2.100 = R$ 9.900`

Valor líquido:

`100.000 + 9.900 = R$ 109.900`

Isso parece simples, mas é a base de praticamente tudo que vem depois.

---

# 3. Produtos isentos

Aqui começa uma fonte comum de confusão.

A Receita identifica como títulos/rendimentos isentos, entre outros, **poupança, LCI, LCA, CRI e CRA**.

Referência:

https://www.gov.br/receitafederal/pt-br/assuntos/meu-imposto-de-renda/preenchimento/manual-mir/patrimonio/eventos-do-patrimonio

Então uma primeira tabela mental seria:

| Produto | PF — IR sobre rendimento |
|---|---:|
| CDB | tributado |
| RDB | tributado |
| Tesouro | tributado |
| LCI | isento |
| LCA | isento |
| CRI | normalmente isento nas condições legais |
| CRA | normalmente isento nas condições legais |
| Poupança | isenta |
| Debênture comum | tributada |
| Debênture incentivada | benefício fiscal conforme requisitos |

Mas vamos aprender também algo muito importante:

> **“Produto isento” é uma simplificação perigosa.**

Sempre precisamos perguntar:

**Isento para quem? Pessoa física? Pessoa jurídica? Residente? Não residente? Sob quais condições?**

É exatamente esse tipo de detalhe que diferencia alguém que conhece investimentos de alguém que consegue trabalhar com tributação em sistemas financeiros.

---

# 4. Fundos de investimento

Esse merece praticamente um curso separado.

Vamos estudar:

- fundos de renda fixa;
- multimercado;
- fundos de ações;
- fundos de curto prazo;
- fundos de longo prazo;
- come-cotas;
- amortização;
- resgate;
- fundo fechado;
- FIDC;
- ETF;
- FII;
- FIAGRO.

Aqui entra o famoso **come-cotas**.

E há uma distinção importante entre fundos classificados como curto e longo prazo. A Receita documenta, por exemplo, que fundos de curto prazo têm tributação de 22,5% ou 20%, enquanto fundos de longo prazo podem atingir a alíquota mínima de 15%, dependendo do prazo.

Referência:

https://www.gov.br/receitafederal/pt-br/centrais-de-conteudo/publicacoes/perguntas-e-respostas/dirpf/p-r-irpf-2026-v1-00-2026-04-23.pdf

Vamos estudar isso não só conceitualmente, mas fazendo:

**quantidade de cotas × valor da cota → patrimônio → rendimento → redução de cotas pelo IR → saldo posterior.**

Isso vai conversar diretamente com sistemas de custódia e back office.

---

# 5. Ações

Aqui muda completamente a lógica.

Não existe aquela tabela regressiva da renda fixa.

Para as regras atuais documentadas pela Receita:

**operações comuns: 15%**

**day trade: 20%**.

Referência:

https://www.gov.br/receitafederal/pt-br/assuntos/meu-imposto-de-renda/pagamento/renda-variavel/bolsa-de-valores-1

Mas o imposto incide sobre o **ganho líquido**.

Precisaremos estudar profundamente:

`Preço médio`

`Custo de aquisição`

`Custos operacionais`

`Venda`

`Lucro/prejuízo`

`Compensação de prejuízos`

`IRRF`

`DARF`

---

# 6. A famosa isenção dos R$ 20 mil

Esse é outro ponto que você precisa dominar muito bem.

A Receita estabelece isenção para ganhos líquidos de determinadas vendas de ações no mercado à vista quando o total de vendas no mês é de até **R$ 20.000**. Essa isenção não vale, por exemplo, para day trade ou ETF.

Referência:

https://www.gov.br/receitafederal/pt-br/assuntos/meu-imposto-de-renda/pagamento/renda-variavel/bolsa-de-valores-1/isencoes

É importante perceber:

**R$ 20 mil não é lucro.**

É **valor de alienação**.

Exemplo:

Compra:

R$ 10.000

Venda:

R$ 18.000

Lucro:

R$ 8.000

Como a alienação mensal está dentro do limite e as demais condições foram atendidas, esse ganho pode estar abrangido pela isenção.

Agora:

Compra:

R$ 30.000

Venda:

R$ 35.000

Lucro:

R$ 5.000

A venda ultrapassou R$ 20 mil.

Então entramos na regra de tributação.

Essa distinção dá bastante problema quando alguém aprende apenas “até 20 mil não paga imposto”.

---

# 7. IRRF — o imposto “dedo-duro”

Outro ponto fundamental para quem trabalha em corretora.

Operações comuns têm retenção de:

**0,005% sobre a venda.**

Day trade:

**1% sobre o resultado líquido da operação**, segundo as regras documentadas pela Receita.

Referência:

https://www.gov.br/receitafederal/pt-br/assuntos/meu-imposto-de-renda/pagamento/renda-variavel/bolsa-de-valores-1/retencoes

Esse pequeno IRRF em bolsa tem uma função importante de rastreabilidade e depois pode ser considerado na apuração do imposto.

Então teremos exercícios como:

```text
Venda ações          50.000
Custo                40.000
Lucro                10.000

IR devido 15%         1.500
IRRF já retido           2,50

IR a recolher         1.497,50
```

Depois vamos complicar isso com prejuízos acumulados.

---

# 8. FII, FIAGRO e ETF

Aqui aparecem diferenças importantes que muita gente mistura.

Por exemplo:

**rendimento distribuído pelo fundo**

não é a mesma coisa que

**ganho obtido vendendo a cota.**

A Receita separa inclusive a apuração das operações com **FII/FIAGRO** das operações comuns e day trade no demonstrativo de renda variável.

Referência:

https://www.gov.br/receitafederal/pt-br/assuntos/meu-imposto-de-renda/preenchimento/manual-mir/rendimentos/rendimentos-do-capital

E ETF também precisa ser estudado separadamente.

É justamente por isso que eu não recomendo aprender uma tabela enorme de:

> CDB = X%, FII = Y%, ação = Z%.

Você decoraria e esqueceria.

Vamos entender os eventos.

---

# 9. A parte mais importante para o seu trabalho

Eu acrescentaria uma camada que normalmente **não aparece em cursos de investimentos**.

Para cada produto estudaremos sempre este modelo:

```text
PRODUTO
    ↓
POSIÇÃO
    ↓
MOVIMENTAÇÃO
    ↓
EVENTO
    ↓
RENDIMENTO
    ↓
FATO GERADOR
    ↓
BASE DE CÁLCULO
    ↓
ALÍQUOTA
    ↓
IRRF
    ↓
VALOR LÍQUIDO
    ↓
INFORMAÇÃO FISCAL
```

Por exemplo, CDB:

```text
Aplicação
R$ 100.000
       ↓
carregamento
       ↓
Saldo bruto
R$ 110.000
       ↓
Resgate
       ↓
Rendimento
R$ 10.000
       ↓
Prazo da aplicação
       ↓
Alíquota
       ↓
IRRF
       ↓
Valor líquido
```

Para ações:

```text
Compra
       ↓
posição
       ↓
preço médio
       ↓
venda
       ↓
ganho/prejuízo
       ↓
comum ou day trade
       ↓
compensações
       ↓
IRRF
       ↓
IR devido
```

Isso já começa a parecer muito mais com **software de back office** do que com curso para investidor.

E é exatamente onde quero chegar com você.

---

# O material que eu sugiro construirmos

Em vez de simplesmente indicar um livro, podemos construir aqui uma espécie de **curso de Tributação de Investimentos para Desenvolvedor de Back Office**.

Cada capítulo terá:

**teoria → legislação/fonte oficial → exemplo financeiro → cálculo manual → tabela de regras → cenário de corretora → modelagem de dados → exercício → implementação em C#/Java/Python.**

Por exemplo, quando chegarmos em renda fixa poderíamos implementar:

```csharp
public decimal CalcularIr(
    decimal rendimento,
    int diasAplicacao)
{
    var aliquota = diasAplicacao switch
    {
        <= 180 => 0.225m,
        <= 360 => 0.20m,
        <= 720 => 0.175m,
        _ => 0.15m
    };

    return rendimento * aliquota;
}
```

Mas não vamos parar no `switch`.

Depois entraremos em coisas mais próximas da realidade:

```text
Instrument
Position
Transaction
TaxEvent
TaxRule
TaxBase
WithholdingTax
Income
CorporateAction
Settlement
```

E aí tributação começa a se conectar com **arquitetura e domínio financeiro**, que é extremamente útil para o tipo de sistema com que você trabalha.

## Nossa trilha

Eu faria nesta sequência:

**Parte I — Fundamentos:** rendimento, saldo, custo, lucro, fato gerador, IRRF, IR devido, isenção, tributação exclusiva/definitiva, antecipação e compensação.

**Parte II — Renda fixa:** CDB/RDB → Tesouro → LCI/LCA → CRI/CRA → debêntures → títulos incentivados → IOF → resgate antecipado → mercado secundário.

**Parte III — Fundos:** cotas → curto/longo prazo → come-cotas → fundos de ações → FII → FIAGRO → ETF → amortizações e resgates.

**Parte IV — Renda variável:** ações → preço médio → operações comuns → isenção de R$20 mil → day trade → prejuízo → compensação → IRRF → DARF.

**Parte V — Avançado:** opções, futuro, termo, aluguel de ações, eventos corporativos, bonificação, desdobramento, grupamento, subscrição e situações de transferência.

**Parte VI — Back office:** posição, custódia, financeiro, eventos, liquidação, saldo bruto/líquido, rendimento, imposto provisionado x realizado, histórico tributário e conciliação.

A Receita inclusive estrutura a declaração moderna separando **bens financeiros, eventos patrimoniais, rendimentos de aplicações financeiras e renda variável**, o que nos dá uma boa referência conceitual para estruturar esse estudo.

Referência:

https://www.gov.br/receitafederal/pt-br/assuntos/meu-imposto-de-renda/preenchimento/manual-mir/patrimonio/bens-financeiros

Eu começaria pela **Aula 1 — Fundamentos de tributação de investimentos: saldo, rendimento, lucro, fato gerador, base de cálculo, IRRF e IR devido**, usando exemplos de CDB e ações lado a lado. Essa primeira aula resolve várias confusões antes de entrarmos em cada produto.
