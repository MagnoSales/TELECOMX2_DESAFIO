# TELECOMX2_DESAFIO
Projeto final da especialização em ciência de dados

# Projeto de Predição de Churn de Clientes de Telecom

## Descrição

Este projeto tem como objetivo desenvolver e implementar um modelo de aprendizado de máquina capaz de prever a evasão (churn) de clientes de uma empresa de telecomunicações. O foco é utilizar dados históricos de clientes para identificar padrões que indicam a probabilidade de um cliente cancelar seu serviço, permitindo que a empresa tome ações proativas para retenção.

O projeto inclui:

*   Carregamento e pré-processamento de dados de clientes.
*   Análise exploratória inicial dos dados.
*   Tratamento de dados ausentes e transformação de variáveis categóricas.
*   Balanceamento da classe target (Churn).
*   Escalonamento de variáveis numéricas.
*   Treinamento e avaliação de modelos de classificação.
*   Identificação das variáveis mais importantes para a predição.
*   Criação de uma rotina para predição em novos dados.

<!-- ![Estado do Build](https://img.shields.io/badge/build-passing-brightgreen) -->
<!-- ![Licença](https://img.shields.io/badge/license-MIT-blue) -->
<!-- ![Feito com](https://img.shields.io/badge/Feito%20com-Python-blue) -->
<!-- ![Bibliotecas Principais](https://img.shields.io/badge/Bibliotecas-Pandas%2C%20Scikit--learn%2C%20Plotly%2C%20Seaborn%2C%20Imblearn-orange) -->

## Configuração do Ambiente

Para executar este projeto, você precisará de um ambiente Python com as seguintes bibliotecas instaladas. Se você estiver usando o Google Colab, a maioria delas já está disponível.

*   `pandas`: Manipulação e análise de dados.
*   `numpy`: Suporte a operações numéricas e arrays.
*   `scikit-learn`: Ferramentas para aprendizado de máquina (modelos, pré-processamento, métricas).
*   `plotly`: Visualização interativa de dados.
*   `seaborn`: Visualização estatística de dados.
*   `imblearn`: Ferramentas para lidar com dados desbalanceados (como SMOTE).
*   `pickle`: Serialização e desserialização de objetos Python (usado para salvar/carregar o modelo e pré-processadores).
*   `json`: Para trabalhar com arquivos JSON (opcional, usado no exemplo de salvar dados).

# Exemplo de novos dados (substitua com seus dados reais)
novos_dados_para_prever = {
    'customerID': ['ClienteA', 'ClienteB', 'ClienteC'],
    'customer.gender': ['Female', 'Male', 'Female'],
    'customer.SeniorCitizen': [0, 0, 1],
    'customer.Partner': ['Yes', 'No', 'Yes'],
    'customer.Dependents': ['No', 'No', 'No'],
    'customer.tenure': [24, 1, 60],
    'phone.PhoneService': ['Yes', 'Yes', 'No'],
    'phone.MultipleLines': ['Yes', 'No', 'No phone service'],
    'internet.InternetService': ['DSL', 'Fiber optic', 'DSL'],
    'internet.OnlineSecurity': ['Yes', 'No', 'Yes'],
    'internet.OnlineBackup': ['No', 'Yes', 'No'],
    'internet.DeviceProtection': ['Yes', 'No', 'Yes'],
    'internet.TechSupport': ['No', 'No', 'Yes'],
    'internet.StreamingTV': ['Yes', 'No', 'Yes'],
    'internet.StreamingMovies': ['No', 'Yes', 'Yes'],
    'account.Contract': ['One year', 'Month-to-month', 'Two year'],
    'account.PaperlessBilling': ['Yes', 'Yes', 'No'],
    'account.PaymentMethod': ['Credit card (automatic)', 'Electronic check', 'Bank transfer (automatic)'],
    'Total.Day': [2.1, 3.5, 1.6],
    'account.Charges.Monthly': [70.5, 100.0, 50.0],
    'account.Charges.Total': [1692.0, 100.0, 3000.0]
}

# Certifique-se de que a função run_churn_prediction_routine está definida (execute a célula correspondente no notebook)
# E que os arquivos .pkl do modelo e pré-processadores estão disponíveis.

# Chamada da rotina de predição
import pandas as pd # Necessário se seus dados estiverem em dicionário

# Se seus dados são um dicionário:
previsoes = run_churn_prediction_routine(novos_dados_para_prever)

# Se seus dados já são um DataFrame:
# novos_dados_df = pd.DataFrame(novos_dados_para_prever) # Converter seu dicionário para DataFrame se necessário
# previsoes = run_churn_prediction_routine(novos_dados_df)
