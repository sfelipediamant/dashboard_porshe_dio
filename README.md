# Painel de Vendas Porsche

Dashboard interativo de vendas de carros da marca Porsche, com visual inspirado no site oficial da Porsche Brasil. Foi construído a partir da planilha `Vendas Porsche.xlsx` (100 registros) e entregue como um único arquivo HTML, que funciona offline em qualquer navegador.

**Arquivo principal:** `dashboard/index.html`

---

## 1. Perguntas de negócio e por que elas importam

As quatro perguntas abaixo foram definidas no briefing do projeto. Juntas formam o ciclo básico de uma análise comercial: *quanto vendemos, quanto isso rendeu, quando vendemos mais e o que vendemos mais*.

| # | Pergunta | Por que importa para o gestor |
|---|----------|-------------------------------|
| 1 | **Qual é o volume total de vendas?** | É a medida de tamanho da operação e a base para comparar períodos, vendedores e regiões. Sem o volume, os demais números não têm referência. |
| 2 | **Qual é o faturamento total e o ticket médio?** | Volume e receita nem sempre andam juntos. O faturamento mostra o resultado financeiro. O ticket médio mostra se a receita vem de muitos carros mais acessíveis ou de poucos carros de alto valor, o que muda a estratégia de estoque e de abordagem comercial. |
| 3 | **Quais meses apresentam maior volume de vendas?** | Revela a sazonalidade. Com ela, o gestor planeja estoque, metas, campanhas e equipe para os meses de pico, e investiga os meses fracos. |
| 4 | **Quais modelos possuem maior participação no faturamento?** | Mostra onde está o dinheiro. Ajuda a decidir quais modelos priorizar em estoque, mídia e metas, e quais dependem de revisão de preço ou de posicionamento. |

### Respostas encontradas (visão geral, sem vendas canceladas)

| Pergunta | Resultado |
|----------|-----------|
| Volume total | **93** vendas válidas (41 já entregues) |
| Faturamento e ticket médio | **R$ 12.202.550,50** de faturamento e **R$ 131.210** de ticket médio |
| Meses de maior volume | **Setembro (9)**, **Maio (8)** e **Dezembro (7)** |
| Participação no faturamento | Por família: **911 (34,2%)**, **Taycan (19,1%)** e **Cayenne (17%)**. Por modelo: **911 Dakar (6,6%)**, **911 Turbo S (6%)** e **911 GT3 (5,7%)** |

### Filtros do dashboard

Ano, mês, família, modelo, status, forma de pagamento e estado. Os gráficos de mês, família, modelo e estado também são clicáveis e aplicam o filtro. Todos os indicadores e as respostas escritas se recalculam a cada filtro, então a mesma tela responde às quatro perguntas para qualquer recorte.

---

## 2. Prompt que gerou o dashboard e o que mudou até a versão final

### Prompt original (primeira versão)

````text
## objetivo
Atue como analista de dados e crie um dashboard de vendas de carros da marca Porshe. Com ênfase na resposta de algumas pergunats de regras de negócio:
1. Qual é o volume total de vendas?
2. Qual é o faturamento total e o ticket médio?
3. Quais meses apresentam maior volume de vendas?
4. Quais modelos possuem maior participação no faturamento?

## base de dados (modelo)
sale_id | SaleDateSanitized | customer_name | PorscheModelSanitized | ModelYearSanitized | SalesPriceSanitized | VehicleMileageSanitized | PayMethodSanitized | CitySanitized | StateSanitized | salesperson | DeliveryStatusSanitized
6 | INVALID    | Michael Adams | 718 Cayman    | 2022 | R$ 79.500,00  | 9800  | Credit Card   | Boston  | MA | kevin        | Delivered
7 | 2024-03-14 | SOPHIA Miller | 911 Turbo S   | 2024 | R$ 235.000,00 | 1200  | Wire Transfer | Seattle | WA | AMANDA scott | Delivered
8 | 2024-04-18 | Daniel-Jones  | Cayenne Coupe | 2023 | R$ 112.750,00 | 6400  | Financing     | Austin  | TX | Brian Hall   | In Transit
9 | INVALID    | Olivia Brown  | Macan S       | 2021 | R$ 68.900,00  | 28    | Cash          | Denver  | CO | jessica      | Pending

## conclusao
agora é com você, crie o dashboard, me respondendo as perguntas de regra de negócio, seguindo um visual moderno e elegante, como encontramos no site official da marca (https://www.porsche.com/brazil/pt/), adicione filtros no dashboard que façam sentido na análise e que auxilie gestores a tomarem melhores decisões.
````

Anexos enviados junto com o prompt: o link do site oficial da Porsche Brasil e a planilha `Vendas Porsche.xlsx`.

### O que mudou até a versão final

| Etapa | Pedido | O que mudou |
|-------|--------|-------------|
| **v1: primeiro dashboard** | O prompt acima | Visual claro com cabeçalho preto e vermelho como destaque. Continha: cartões das 4 perguntas, respostas escritas dinâmicas, evolução mensal, sazonalidade, participação por família e modelo, status de entrega, pagamento, estados, ticket médio por família e tabela com busca. Também tinha 7 filtros e gráficos clicáveis. |
| **v2: versão final** | *"melhore o design, deixe mais premium, use imagens da marca como carros, enfim, deixe a página moderna"* | Tema escuro premium. Imagem de abertura em tela cheia, com título grande e menu de navegação por seção. Imagens de carros (estilo 911, Taycan e Cayenne e interior esportivo), embutidas no arquivo. Nova seção de **cartões por família** com imagem, participação, vendas e ticket médio, que também funcionam como filtro. Barra de filtros com efeito de vidro e fixa no topo. Gráficos em gradiente, tabela e etiquetas de status redesenhadas, e animações discretas (respeitando a preferência de movimento reduzido do sistema). |

**Mantido da v1 para a v2:** os dados, as regras de cálculo, os filtros e as respostas às quatro perguntas. A v2 foi uma evolução visual e de experiência, sem alterar os números.

**Observação sobre as imagens:** as imagens dos carros foram geradas por IA, no estilo dos modelos, e não são fotos oficiais da marca. Para publicar com fotos oficiais, é preciso ter a licença de uso da marca e trocar as imagens no código.

---

## 3. Tratamento da base antes de ir para a IA

### Tratamento feito antes (colunas de preço e quilometragem)

| Coluna | Tratamento |
|--------|------------|
| `SalesPriceSanitized` | Normalização do preço para um valor numérico. O texto no formato brasileiro (`R$ 79.500,00`) passou a ser número, e o arquivo mantém a formatação de moeda em R$. |
| `VehicleMileageSanitized` | Normalização da quilometragem para um valor numérico inteiro. |

Na planilha enviada, as duas colunas estão numéricas e sem células vazias. O preço vai de R$ 58.900 a R$ 286.500 e a quilometragem vai de 0 a 52.000.

A coluna de quilometragem foi tratada na base, mas **não é usada nas visualizações da versão atual**. Ela fica como candidata a uma evolução futura, por exemplo para analisar seminovos.

### Tratamentos adicionais aplicados dentro do dashboard

| Situação encontrada | Como foi tratada |
|---------------------|------------------|
| Datas com o valor `INVALID` (24 registros) | Os registros permanecem nos totais de volume e faturamento, mas não entram nos gráficos nem nos filtros por período. Isso é informado no painel. |
| Vendas com status *Cancelled* (7 registros) | Excluídas por padrão como "vendas válidas". O filtro de status permite incluí-las ou ver só elas. |
| Nomes de clientes e vendedores com capitalização inconsistente (`SOPHIA Miller`, `AMANDA scott`, `kevin`, `Daniel-Jones`) | Padronizados para formato de nome próprio. |
| Status de entrega e formas de pagamento em inglês | Traduzidos para português. Os status foram agrupados em Entregue, Em logística, Pendente e Cancelado. |
| Famílias de modelos | Criadas a partir do nome do modelo (911, 718, Cayenne, Macan, Panamera e Taycan), para permitir a análise de participação por família. |

**Pontos de atenção na base:**
- Há vendas com datas até outubro de 2027, o que sugere dados fictícios ou de projeção. Todas foram mantidas.
- A quantidade de datas inválidas (24%) limita a análise de sazonalidade. Corrigir essa coluna na origem é o ganho de qualidade mais importante para uma próxima versão.

---

## 4. Ferramenta utilizada

Usei o **Microsoft Copilot** com o modelo **Sonnet 5.5**. Não usei ChatGPT com Canvas.

Na conversa, o Copilot leu a planilha, calculou os indicadores com código, gerou o HTML do dashboard e as imagens dos carros, e testou o resultado em um navegador automatizado (filtros e gráficos clicáveis, sem erros de script).

---

## 5. Endereço da dashboard publicada

**URL:** _a definir (publicação em andamento)_

Como o dashboard é um único arquivo HTML estático, ele pode ser publicado sem servidor, por exemplo na Vercel, no GitHub Pages ou no SharePoint. Depois de publicar, substitua o texto acima pelo endereço final.
