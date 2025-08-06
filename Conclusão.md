# Conclusão e Análise Detalhada do Projeto de Predição de Churn

## Introdução

Este documento apresenta a análise aprofundada dos resultados obtidos no projeto de predição de churn de clientes de telecomunicações. O objetivo principal foi identificar os padrões e fatores que levam os clientes a cancelar seus serviços e desenvolver um modelo preditivo para antecipar essa evasão.

## Comparação de Modelos

Foram treinados e avaliados dois modelos de classificação: uma Árvore de Decisão e uma Regressão Logística. A avaliação foi realizada utilizando métricas apropriadas para conjuntos de dados desbalanceados, como Recall, Precisão, F1-score, AUC (Area Under the ROC Curve) e AP (Average Precision).

Com base no desempenho no conjunto de validação, a **Regressão Logística** demonstrou ser o modelo mais promissor para este problema de negócio, apresentando um desempenho superior em métricas cruciais para a identificação de clientes em risco de evasão:

*   **Regressão Logística:**
    *   Recall: Aproximadamente 0.7733
    *   Precisão: Aproximadamente 0.5284
    *   F1-score: Aproximadamente 0.6278
    *   AUC: Aproximadamente 0.8409
    *   AP: Aproximadamente 0.6594

*   **Árvore de Decisão (Melhor Modelo Otimizado):**
    *   Recall: Aproximadamente 0.5693
    *   Precisão: Aproximadamente 0.5636
    *   F1-score: Aproximadamente 0.5664
    *   AUC: Aproximadamente 0.7854
    *   AP: Aproximadamente 0.5259

O **Recall** da Regressão Logística, sendo significativamente mais alto, indica que este modelo é mais eficaz em identificar a maioria dos clientes que realmente irão evadir (menor taxa de Falsos Negativos), o que é fundamental para ações de retenção proativas. O **AUC** e **AP** superiores também reforçam a melhor capacidade da Regressão Logística em discriminar entre as classes e ranquear corretamente os clientes por probabilidade de churn.

## Análise de Variáveis Influentes

A análise da importância das variáveis no modelo de Árvore de Decisão e dos coeficientes no modelo de Regressão Logística revelou os principais fatores associados à evasão de clientes. Embora os modelos tenham abordagens diferentes para determinar a importância, houve uma sobreposição significativa nas variáveis mais influentes:

*   **Tipo de Contrato (`account.Contract_Month-to-month`, `account.Contract_Two year`):** O tipo de contrato Mês a Mês é consistentemente o fator mais forte associado ao churn. Clientes sem um compromisso de longo prazo (contratos de um ou dois anos) são muito mais propensos a cancelar. O coeficiente positivo para "Month-to-month" e negativo para "Two year" na Regressão Logística corrobora fortemente essa relação.
*   **Tempo de Contrato (`customer.tenure`):** O tempo que um cliente está com a empresa tem uma forte relação negativa com a evasão. Clientes com maior *tenure* (mais meses de contrato) são significativamente menos propensos a cancelar. Este foi um dos coeficientes negativos mais fortes na Regressão Logística.
*   **Cobranças (`account.Charges.Monthly`, `account.Charges.Total`):** Tanto as cobranças mensais quanto as totais estão associadas à evasão. Cobranças mais altas tendem a aumentar a probabilidade de churn. O coeficiente positivo para `account.Charges.Total` e negativo para `account.Charges.Monthly` na Regressão Logística sugere uma interação complexa, onde o valor total (acumulado) pode ser um melhor preditor de churn do que apenas a cobrança mensal, mas a interpretação precisa dos coeficientes em dados codificados requer cautela. A importância na Árvore de Decisão também confirmou a relevância destas variáveis.
*   **Serviço de Internet (`internet.InternetService_Fiber optic`, `internet.InternetService_DSL`):** Clientes com serviço Fiber Optic parecem ter uma maior probabilidade de churn em comparação com clientes DSL ou sem serviço de internet. O coeficiente positivo para "Fiber optic" e negativo para "DSL" na Regressão Logística sugere que, apesar de ser uma tecnologia mais avançada, o serviço Fiber Optic pode estar associado a problemas que levam à evasão (custo percebido, qualidade do serviço, etc.).
*   **Serviços Adicionais (Segurança Online, Suporte Técnico, Streaming):** A ausência de serviços de segurança online (`internet.OnlineSecurity_No`) e suporte técnico (`internet.TechSupport_No`) foi identificada como importante pela Árvore de Decisão e sugerida pelos coeficientes positivos na Regressão Logística. Clientes sem esses recursos adicionais de proteção e suporte podem se sentir menos seguros ou ter mais dificuldades técnicas não resolvidas, aumentando o risco de churn. Ter serviços de streaming (TV/Movies) também mostrou uma associação positiva com churn na Regressão Logística, embora com menor impacto.
*   **Faturamento sem Papel (`account.PaperlessBilling_Yes`):** Clientes que optam por faturamento sem papel (`PaperlessBilling_Yes`) têm uma probabilidade maior de churn. Isso pode ser um indicador de clientes mais digitalizados ou menos engajados com métodos de comunicação tradicionais, e pode estar correlacionado com outros fatores que influenciam a evasão.
*   **Método de Pagamento (`account.PaymentMethod_Electronic check`):** O método de pagamento via Cheque Eletrônico foi destacado, especialmente pela Árvore de Decisão, como associado a maior churn. Isso pode indicar clientes com menor estabilidade financeira ou menos familiaridade com métodos de pagamento automático.

## Estratégias de Retenção Propostas

Com base nos fatores que mais influenciam a evasão, as seguintes estratégias de retenção podem ser consideradas:

1.  **Foco em Clientes com Contratos Mês a Mês:** Este é o grupo de maior risco. Oferecer incentivos significativos para a migração para contratos mais longos (um ou dois anos), como descontos na mensalidade, benefícios adicionais ou upgrades de serviço gratuitos por um período, pode reduzir a taxa de churn neste segmento.
2.  **Programas de Fidelidade para Clientes de Longo Prazo:** Reconhecer e recompensar clientes com maior tempo de contrato para reforçar a lealdade e diminuir a probabilidade de considerarem concorrentes. Descontos progressivos, acesso a serviços premium ou suporte prioritário podem ser opções.
3.  **Análise de Preços e Pacotes:** Investigar se as cobranças mensais e totais percebidas como altas estão ligadas a pacotes específicos ou a uma percepção de baixo custo-benefício. Oferecer opções de pacotes mais flexíveis ou renegociar planos pode ser eficaz para clientes com alta carga de cobrança e risco de churn.
4.  **Melhoria da Qualidade do Serviço Fiber Optic:** Se a análise confirmar que a insatisfação com o serviço Fiber Optic é um motor de churn, investir na melhoria da infraestrutura, na resolução mais rápida de problemas técnicos e na comunicação proativa sobre manutenções pode ser crucial.
5.  **Promoção de Serviços de Segurança Online e Suporte Técnico:** Enfatizar os benefícios e a importância da segurança online e do suporte técnico, talvez oferecendo períodos de teste gratuitos ou descontos para clientes sem esses serviços. Isso pode aumentar a percepção de valor e segurança na utilização dos serviços.
6.  **Experiência do Cliente com Faturamento sem Papel e Cheques Eletrônicos:** Investigar se há pontos de atrito específicos na experiência do cliente relacionados ao faturamento sem papel ou ao uso de cheques eletrônicos que possam contribuir para a insatisfação e churn. Simplificar processos ou oferecer alternativas mais convenientes pode ajudar.

## Conclusão

O modelo de Regressão Logística desenvolvido neste projeto demonstrou uma boa capacidade de prever a evasão de clientes, superando o modelo de Árvore de Decisão nas métricas mais relevantes para o problema de churn. A análise das variáveis influentes forneceu insights acionáveis sobre os principais motivadores de evasão, destacando a importância do tipo e tempo de contrato, custos, serviço de internet e serviços adicionais. As estratégias de retenção propostas, direcionadas a estes fatores e segmentos de risco, podem ser implementadas pela empresa para reduzir a taxa de churn e aumentar a retenção de clientes valiosos.
