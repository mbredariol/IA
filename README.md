# IA
Machine Learning


Etapa 1: Criar o Modelo Preditivo no Azure Machine Learning Studio
1. Acessar o Azure Machine Learning Studio
Entre no Azure Machine Learning Studio.
Certifique-se de ter criado um recurso de Azure Machine Learning no portal do Azure.
2. Criar um Workspace
No Azure ML Studio, crie um Workspace caso ainda não tenha um:
Vá em Workspaces e clique em Create New.
Configure os detalhes do workspace, como nome, assinatura e região.
3. Utilizar o Recurso de AutoML
Clique em Automated Machine Learning no menu lateral.
Selecione New Automated ML Run.
Escolha o dataset que será usado (você pode fazer upload de um arquivo CSV, por exemplo).
Exemplo de Dataset: Conjunto de dados de vendas, com colunas como Data, Vendas e Região.
Defina a coluna-alvo para previsão (exemplo: Vendas).
Configure a tarefa como Regressão (para prever valores numéricos).
Escolha os recursos de computação (você pode criar um cluster de máquinas virtuais se necessário).
4. Treinar o Modelo
Execute o treinamento e aguarde a conclusão.
O AutoML testará vários algoritmos automaticamente e escolherá o melhor modelo com base em métricas como R2 Score ou Mean Absolute Error (MAE).
5. Implantar o Modelo
Após o treinamento, clique em Deploy no melhor modelo identificado.
Configure um endpoint RESTful:
Escolha um nome para o endpoint.
Escolha o tipo de serviço (geralmente ACI, para Azure Container Instances).
Aguarde a implantação.
6. Obter as Informações do Endpoint
Depois de implantado, acesse o endpoint no Azure ML Studio.
Copie o endpoint URL e a chave de autenticação.
Salve as informações em um arquivo endpoint.json:
json
Copiar código
{
  "endpoint": "https://seu-endpoint-no-azure.azure.com/score",
  "key": "sua-chave-de-autenticacao",
  "method": "POST"
}
Etapa 2: Criar o Arquivo README.md
Crie um arquivo README.md com o seguinte conteúdo:

markdown
Copiar código
# Projeto de Previsão com Azure Machine Learning

## Introdução
Este projeto consiste na criação de um modelo de previsão utilizando o **Azure Machine Learning Studio**. O objetivo é prever as vendas futuras de uma empresa com base em dados históricos.

## Objetivo
Construir e implantar um modelo preditivo capaz de analisar dados históricos de vendas e fornecer previsões precisas para apoiar decisões estratégicas.

## Tecnologias Utilizadas
- **Azure Machine Learning Studio**
- **Automated Machine Learning (AutoML)**
- **Python (para consumo do endpoint)**

## Passo a Passo

### 1. Preparação dos Dados
- O dataset utilizado contém informações de vendas, com colunas como `Data`, `Vendas` e `Região`.
- Os dados foram limpos para remover valores nulos e normalizados para melhorar o desempenho do modelo.

### 2. Treinamento do Modelo
- Foi utilizado o recurso **Automated Machine Learning (AutoML)** para testar diferentes algoritmos de regressão.
- O AutoML escolheu o modelo com melhor desempenho com base na métrica **R2 Score**.

### 3. Implantação do Modelo
- O modelo foi implantado como um endpoint RESTful utilizando **Azure Container Instances (ACI)**.
- As informações do endpoint foram exportadas para um arquivo `endpoint.json` que pode ser utilizado para consumo.

## Como Utilizar o Endpoint

### Exemplo de Requisição em Python:
```python
import requests

# URL do endpoint e chave de autenticação
url = "https://seu-endpoint-no-azure.azure.com/score"
headers = {"Authorization": "Bearer sua-chave-de-autenticacao"}
data = {
    "data": [
        {"Data": "2024-01-01", "Região": "Sul", "Outros_Campos": "valores"}
    ]
}

# Enviar requisição
response = requests.post(url, json=data, headers=headers)

# Ver resposta
if response.status_code == 200:
    print("Previsão:", response.json())
else:
    print("Erro:", response.text)
Exemplo de Requisição em curl:
bash
Copiar código
curl -X POST \
     -H "Authorization: Bearer sua-chave-de-autenticacao" \
     -H "Content-Type: application/json" \
     -d '{"data": [{"Data": "2024-01-01", "Região": "Sul"}]}' \
     https://seu-endpoint-no-azure.azure.com/score
