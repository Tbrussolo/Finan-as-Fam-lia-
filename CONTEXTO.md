# Painel Financeiro Brussolo — contexto do sistema

Resumo do que foi montado nesta conversa, para referência (sua e de quem for mexer depois).

## Estrutura de dados

- **Taxonomia oficial** (grupos/subgrupos): Moradia, Contas fixas, Alimentação, Educação,
  Transporte, Saúde, Despesas pessoais, Lazer, Outros Gastos, Dívidas e empréstimos, Igreja,
  Profissional, Impostos Pessoais. Qualquer categorização nova segue só esses nomes.
- **Motor de categorização** (`categorias.py` + `motor.py`): regras em regex, primeira que bate
  vence. `ajustes_manuais.json` tem prioridade sobre as regras — é onde ficam os lançamentos
  pontuais conferidos um a um (recibos, casos especiais).
- **Premissas** (`metas.json`): orçamento mensal por grupo, dívidas em aberto (Consórcio HS,
  Agência de Fomento, Cartão BTG, Empréstimo amigo), parcelamentos de cartão em aberto.
- **Planilha de projeção** (`Projecao_Financeira_nov26_dez27.xlsx`, na pasta Particular do PC):
  fluxo de caixa mensal Nov/26–Dez/29, só atualizada por comando explícito ("atualize a
  planilha na pasta").

## Painel orçamento x realizado (GitHub Pages)

- `index.html` + `dados_orcamento.xlsx` no repositório `Tbrussolo/Finanças-Família`.
- O painel lê o Excel direto no navegador (biblioteca SheetJS) — não tem nada "ao vivo" puxando
  banco; atualiza quando o `dados_orcamento.xlsx` é substituído no repo.
- Dados de Ago/Set/Out-26 já apurados a partir dos extratos completos (Bradesco, BTG, C6),
  passados pelo mesmo motor de categorização. Meses seguintes ficam em branco (célula amarela)
  até serem preenchidos.
- Fluxo de atualização: edita o Excel → sobe no GitHub (upload direto ou GitHub Desktop,
  commit + push) → Pages atualiza sozinho em ~1 min.

## Regras de governança combinadas

- Nunca inventar dado (valor, data, forma de pagamento) — perguntar quando faltar ou não bater.
- Dupla checagem contra duplicação (ex.: pagamento de fatura de cartão pela conta não conta como
  gasto novo, já que a compra em si já foi contada no cartão).
- Mudança de taxonomia ou de premissa só acontece com confirmação explícita do usuário.
- Planilha de projeção e painel só são gerados/atualizados por comando explícito, nunca por
  iniciativa própria.

## Pendências em aberto

- Dízimo (Igreja): valores capturados nos extratos ficaram bem abaixo da meta de R$1.200/mês —
  não ficou claro se o dízimo é pago por outro meio.
- Receita real (Propósito) nos extratos não bateu com a premissa de R$10.000 fixos todo dia 15.
- Novembro/26 em diante: ainda sem extrato completo carregado no sistema.
