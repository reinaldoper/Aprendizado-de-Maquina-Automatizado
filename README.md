# Aprendizado de Maquina Automatizado
Aprendizado de Máquina Automatizado para Previsão de Aluguel de Bicicletas


## Introdução

- Este repositório contém código e instruções para aproveitar o Azure Machine Learning Studio e realizar aprendizado de máquina automatizado (AutoML) em um conjunto de dados históricos de aluguel de bicicletas. O objetivo é treinar um modelo capaz de prever o número de aluguéis de bicicletas em um determinado dia, levando em consideração características sazonais e meteorológicas.

## Conjunto de Dados

- O conjunto de dados utilizado neste projeto é derivado do programa Capital Bikeshare e é utilizado de acordo com o contrato de licença de dados. O conjunto de dados consiste em detalhes históricos de aluguel de bicicletas.

- URL da Web :

[URL da Web](https://aka.ms/bike-rentals)

## Configuração no Azure Machine Learning Studio
- Para replicar o experimento, siga estes passos:

- Abra o Azure Machine Learning Studio e vá para a página de AutoML em Authoring.

## Crie um novo trabalho de AutoML com as seguintes configurações básicas:

- Nome do Trabalho: mslearn-bike-automl
- Novo Nome do Experimento: mslearn-bike-rental
- Descrição: Aprendizado de máquina automatizado para previsão de aluguel de bicicletas
- Marcadores: Nenhum


## Tipo de Tarefa e Dados:

- Selecione o Tipo de Tarefa: Regressão
- Selecione o Conjunto de Dados: Crie um novo conjunto de dados chamado "aluguel de bicicletas" com as configurações da fonte da web fornecidas.


## Configurações da Tarefa:

- Tipo de Tarefa: Regressão
- Conjunto de Dados: Aluguel de Bicicletas
- Coluna Alvo: Aluguéis (inteiro)


## Configurações Adicionais:

- Métrica Primária: Raiz do Erro Quadrático Médio Normalizado (nRMSE)
- Explicar Melhor Modelo: Não selecionado
- Usar Todos os Modelos Suportados: Desmarcado
- Modelos Permitidos: Selecionar apenas RandomForest e LightGBM


## Limites:

- Máximo de Testes: 3
- Máximo de Testes Simultâneos: 3
- Máximo de Nós: 3
- Limite de Pontuação da Métrica: 0,085
- Limite de Tempo: 15
- Limite de Tempo de Iteração: 15
- Habilitar Rescisão Antecipada: Selecionado


## Validação e Teste:

- Tipo de Validação: Divisão de Treino e Validação
- Porcentagem de Dados de Validação: 10
- Conjunto de Dados de Teste: Nenhum

## Cálculo:

- Selecione o Tipo de Computação: Sem Servidor
- Tipo de Máquina Virtual: CPU
- Camada de Máquina Virtual: Dedicada
- Tamanho da Máquina Virtual: Standard_DS3_V2 (ou qualquer tamanho disponível)
- Envie o trabalho de treinamento. Aguarde sua conclusão.

## Avalie o Melhor Modelo

- Após a conclusão do trabalho de AutoML, revise o resumo do melhor modelo treinado. Na guia Visão Geral, observe o resumo do modelo, destacando o nome do algoritmo.

- Selecione o nome do algoritmo para visualizar detalhes e vá para a guia Métricas para inspecionar os gráficos residuais e predito vs. verdadeiro para avaliar o desempenho do modelo.

## Implante e Teste o Modelo

- Ao estar satisfeito com o modelo, implante-o seguindo estas etapas:

- Na guia Modelo do melhor modelo treinado, selecione Implantar.

## Escolha a opção de Serviço Web para implantação com as seguintes configurações:

- Nome: prever-alugueis
- Descrição: Prever aluguel de bicicletas
- Tipo de Computação: Instância de Contêiner do Azure
- Habilitar Autenticação: Selecionado
- Aguarde o início da implantação, isso pode levar alguns segundos. O status será indicado como "Executando".

- Espere até que o status de implantação mude para "Concluído". Isso pode levar de 5 a 10 minutos.

## Teste o serviço implantado:

- No Azure Machine Learning, vá para Endpoints e abra o endpoint de previsão em tempo real para aluguel de bicicletas.

- Na página de teste, substitua o modelo JSON pelos dados de entrada fornecidos.

- No painel Dados de entrada para testar o endpoint , substitua o modelo JSON pelos seguintes dados de entrada:

```shell
 {
   "Inputs": { 
     "data": [
       {
         "day": 1,
         "mnth": 1,   
         "year": 2022,
         "season": 2,
         "holiday": 0,
         "weekday": 1,
         "workingday": 1,
         "weathersit": 2, 
         "temp": 0.3, 
         "atemp": 0.3,
         "hum": 0.3,
         "windspeed": 0.3 
       }
     ]    
   },   
   "GlobalParameters": 1.0
 }
 ```

- Clique em Testar e revise os resultados, incluindo o número previsto de aluguéis.

```shell
 {
   "Results": [
     444.27799000000000
   ]
 }
```
