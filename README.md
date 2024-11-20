# 📄 Descrição do Projeto
Este projeto utiliza redes neurais do tipo Long Short-Term Memory (LSTM) para prever os preços de fechamento das ações do Itaú Unibanco (ITUB4.SA) com base em dados históricos obtidos do Yahoo Finance. O modelo é exposto por meio de uma API RESTful desenvolvida com Flask, permitindo que usuários façam previsões de preços futuros com base em entradas personalizadas.

## 📊 **Pipeline do Projeto**

### 1️⃣ Coleta e Pré-processamento dos Dados

- Os dados históricos das ações foram baixados utilizando a biblioteca **yfinance**.
- Apenas os valores de fechamento (`Close`) foram considerados.
- Os dados foram normalizados com o **MinMaxScaler** para acelerar o aprendizado do modelo.

### 2️⃣ Desenvolvimento do Modelo

- O modelo é uma arquitetura LSTM com:
    - 3 camadas LSTM (50 unidades cada).
    - Dropout para evitar overfitting.
    - Uma camada densa para saída escalar.
- O modelo foi treinado com 70% dos dados e testado nos 30% restantes.
- Métrica de avaliação principal: **Root Mean Squared Error (RMSE)**.
  
### 3️⃣ Exportação do Modelo

- O modelo foi salvo no formato `.h5` utilizando o método `model.save()` do Keras, garantindo compatibilidade para carregamento e inferência.

### 4️⃣ Deploy da API

- A API permite:
    - Submissão de uma lista de preços históricos (mínimo de 60 preços).
    - Especificação do número de dias a prever.
- A API utiliza um modelo pré-carregado para realizar as previsões e retorna os valores em formato JSON.

### 5️⃣ Monitoramento

- Implementado monitoramento básico com **logging**, registrando tempo de resposta das requisições.
- Mensagens de log são salvas em um arquivo chamado `app.log`.
  
