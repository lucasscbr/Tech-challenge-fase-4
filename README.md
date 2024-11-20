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
- Mensagens de log são salvas no arquivo `app.log`.
  
## 🚀 **Executando o Projeto**

### 1️⃣ Clonar o Repositório

``` bash
git clone https://github.com/lucasscbr/Tech-challenge-fase-4.git
cd Tech-challenge-fase-4
```

### 2️⃣ Instalar Dependências

``` bash
python -m venv venv
venv\Scripts\activate
pip install -r requirements.txt
```

### 3️⃣ Treinar o Modelo (Opcional)

Caso deseje treinar o modelo novamente, execute o script:
``` bash
python Previsoes_Itau.py
```

### 4️⃣ Rodar a API
Inicie o servidor Flask:
``` bash
python app.py
```

A API estará disponível em: `http://127.0.0.1:5000`.

### 5️⃣ Realizar Previsões
Envie uma requisição POST para o endpoint `/predict` com o seguinte corpo JSON:
``` 
{
  "prices": [37.0, 37.0, 37.61, 36.98, 37.05, 37.52, 38.1, 37.9, 36.7, 37.2, 38.3, 39.5, 38.7, 38.2, 38.0, 37.8, 37.3, 37.0, 36.9, 37.1, 37.6, 38.0, 37.7, 36.9, 37.3, 38.1, 38.9, 38.5, 37.8, 38.0, 37.9, 38.3, 38.2, 37.9, 37.5, 37.3, 36.8, 37.0, 37.7, 38.4, 38.6, 38.5, 38.0, 37.9, 37.8, 37.6, 37.2, 37.4, 38.0, 38.2, 38.5, 38.7, 38.8, 39.0, 39.1, 39.2, 39.3, 39.4, 39.5, 39.6, 39.7],
  "days": 3
}
```

## 🧩 **Estrutura do Repositório**

``` bash
├── Previsoes_Itau.py        # Código para coleta de dados, treinamento e avaliação do modelo
├── app.py                   # Código da API Flask
├── requirements.txt         # Dependências do projeto
├── modelo_lstm_itub4.h5     # Modelo LSTM treinado
├── app.log                  # Logs salvos
└── README.md                # Documentação do projeto
```

