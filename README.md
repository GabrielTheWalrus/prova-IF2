# Prova-IF2

Instruções para execução:

1) Baixar o notebook python (ou utilizar o link do google colab para simular o ambiente de execução).
2) Fazer o upload dos datasets no mesmo diretório do notebook e criar um arquivo db.sqlite.
3) Executar célula a célula do notebook e observar os resultados do mesmo.

As respostas teóricas também estão no notebook.

Link para o notebook python: https://colab.research.google.com/drive/1BEqXlJhZ9MJDgSYMoEBcSKjfbzjWI3J8?usp=sharing

Respostas:

1. Qual foi a campanha mais cara? 1004
2. Qual foi a campanha mais lucrativa? 1009
3. Qual anúncio é o mais eficaz em termos de cliques? 20007
4. Qual anúncio é o mais eficaz em termos de geração de leads? 20003

Querys:

1 - SELECT SUM(COST), CAMPAIGN_ID FROM (SELECT DISTINCT ID_ADS_MEDIA_COSTS, CAMPAIGN_ID, COST FROM AD_CUSTOMER) GROUP BY CAMPAIGN_ID ORDER BY SUM(COST) DESC LIMIT 1
2 - SELECT A.CAMPAIGN_ID, (RECEITA-CUSTO) AS LUCRO FROM (SELECT SUM(COST) AS CUSTO, CAMPAIGN_ID FROM (SELECT DISTINCT ID_ADS_MEDIA_COSTS, CAMPAIGN_ID, COST FROM AD_CUSTOMER) GROUP BY CAMPAIGN_ID) A inner join (SELECT SUM(REVENUE) AS RECEITA, CAMPAIGN_ID FROM (SELECT DISTINCT ID_CUSTOMER_LEADS_FUNNEL, CAMPAIGN_ID, REVENUE FROM AD_CUSTOMER) GROUP BY CAMPAIGN_ID) B ON A.CAMPAIGN_ID = B.CAMPAIGN_ID ORDER BY LUCRO DESC LIMIT 1
3 - SELECT SUM(CLICKS), AD_CREATIVE_ID FROM (SELECT DISTINCT ID_ADS_MEDIA_COSTS, AD_CREATIVE_ID, CLICKS FROM AD_CUSTOMER WHERE AD_CREATIVE_ID IS NOT NULL) GROUP BY AD_CREATIVE_ID ORDER BY SUM(CLICKS) DESC LIMIT 1
4 - SELECT ID_CREATIVE, COUNT(ID_CREATIVE) FROM (SELECT ID_CREATIVE FROM AD_CUSTOMER WHERE ID_CREATIVE != '' AND ID_DEVICE IN (SELECT ID_DEVICE FROM AD_CUSTOMER GROUP BY ID_CUSTOMER_LEADS_FUNNEL, ID_PAGEVIEW, ID_DEVICE) GROUP BY ID_DEVICE) GROUP BY ID_CREATIVE ORDER BY COUNT(ID_CREATIVE) DESC LIMIT 1

Qualquer dúvida entrar em contato:

gabriel.meale@hotmail.com / gabriel.meale@itau-unibanco.com.br
