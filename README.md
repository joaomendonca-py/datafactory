# Documentação do Projeto de Ingestão e Processamento de Dados - Brewery ETL

## Visão Geral do Projeto
Este projeto visa implementar um pipeline de ETL (Extração, Transformação e Carregamento) para processar dados relacionados à empresa, utilizando as ferramentas do Azure como Databricks, Data Factory, e Azure Storage Account. Os dados são extraídos, transformados e armazenados em diferentes camadas (“bronze”, “silver” e “gold”), cada uma representando um estágio de maturidade no processamento dos dados.

## Arquitetura do Pipeline
O pipeline foi construído utilizando:
- **Azure Data Factory (ADF)** para orquestração das execuções dos notebooks Databricks.
- **Azure Databricks** para implementar a lógica ETL.
- **Azure Data Lake Storage (ADLS)** para armazenar os dados em diferentes camadas: “bronze”, “silver” e “gold”.

O pipeline é acionado pelo ADF, que executa notebooks Databricks que realizam a extração de dados de APIs, o processamento e a persistência dos resultados em ADLS.

## Configuração do Azure Data Lake Storage (ADLS)
O **Brewery Data Lake** foi configurado com as seguintes camadas:
- **Bronze**: Dados brutos extraídos da fonte sem manipulação ou tratamento.
- **Silver**: Dados tratados e normalizados, com transformações de limpeza aplicadas.
- **Gold**: Dados prontos para serem usados em análises e visualizações.

A hierarquia do armazenamento foi configurada conforme mostrado abaixo:
- Containers:
  - **bronze**
  - **silver**
  - **gold**

A configuração do ADLS inclui performance padrão, replicação local e utilização do StorageV2.

## Azure Databricks
### Notebooks Utilizados
No Azure Databricks, foram criados dois notebooks principais:
1. **pipeline brewery**: Responsável pelo processamento ETL das camadas bronze, silver e gold.
2. **Testes**: Utilizado para validação dos dados e execução de casos de teste para garantir a qualidade dos dados.

Os dados de cada camada foram armazenados no schema “brewery”, com as seguintes tabelas:
- **bronze_breweries**
- **silver_breweries**
- **gold_breweries**

A configuração do Azure Databricks foi feita no recurso “pipelinedatabricks”.

## Configuração do Azure Data Factory (ADF)
O **Azure Data Factory** foi utilizado para orquestrar o pipeline. Os principais elementos configurados foram:
- **Pipeline para execução dos notebooks Databricks**.
- **Triggers para execução automática do pipeline**, garantindo execuções periódicas e automatizadas.
- **Alertas e métricas** para monitorar a execução do pipeline e notificar em caso de falhas. Os alertas foram configurados para enviar e-mails sempre que houver uma falha em um pipeline.

## Monitoramento e Alertas
No Azure Data Factory, foi implementado um sistema de **alertas e monitoramento** que abrange:
- **Alertas para falhas no pipeline**: Configurado para disparar e-mails em caso de erro em qualquer etapa do pipeline.
- **Métricas monitoradas**: Incluem a execução dos pipelines e atividades específicas, para garantir que falhas sejam detectadas e tratadas.

Os alertas incluem condições como “falha de execução de pipeline”, severidade, e lógica de alerta que considera falhas superiores a zero ocorrências.

## Testes e Validações
O notebook **Testes** foi utilizado para realizar validações dos dados após o processamento:
- **Testes unitários** para verificar se os dados foram carregados conforme esperado.
- **Validação dos resultados** nas camadas bronze, silver e gold, garantindo a consistência dos dados entre as camadas.

## Considerações Finais
Este projeto é um exemplo de como utilizar os recursos do Azure para criar um pipeline de dados escalável e automatizado, com foco em qualidade e monitoramento. Cada etapa foi cuidadosamente planejada para garantir a qualidade dos dados e a facilidade de manutenção e expansão no futuro.

## Imagens e Capturas de Tela
Para maior clareza e facilitar a compreensão da configuração dos recursos, é recomendado incluir imagens e capturas de tela das seguintes partes:
- Configuração do Azure Data Lake Storage (containers bronze, silver, gold).
  ![datalake](https://github.com/user-attachments/assets/20e53abc-5e7a-4253-bd22-7a6996a6f674)
  ![silver](https://github.com/user-attachments/assets/13e3a1c5-e64b-477b-8b40-a7390231a7f3)
![gold](https://github.com/user-attachments/assets/f822015d-e550-4c9b-ba4d-cf7965294207)
![bronze](https://github.com/user-attachments/assets/675b4bed-94d7-468a-8fad-dc803ff0b2df)

- Visão geral do Azure Databricks (notebooks e tabelas).
  ![schema-tables](https://github.com/user-attachments/assets/459b5db0-aba5-4e46-bc83-a402645c04bf)
![notebooks-databricks](https://github.com/user-attachments/assets/71be11a1-3460-415e-8e4d-59c406911e36)

- Configuração do Azure Data Factory (pipelines, triggers, alertas).
  ![datafactoryActivityLog](https://github.com/user-attachments/assets/27671bd2-6ef3-43c9-a69d-a1728e1a1346)

![triggerRuns](https://github.com/user-attachments/assets/dab559ac-c99e-41a4-a31b-adef2da5e629)
![pipelineTriggers](https://github.com/user-attachments/assets/bf62691b-cb3f-4e94-b2f7-3a70d7ed6fd9)
![pipelineDebug](https://github.com/user-attachments/assets/c5f3d7fb-22c8-4623-a167-57f1251e5d8f)
![pipeline04](https://github.com/user-attachments/assets/b9ea8843-128e-4598-bdba-2f0c7799b2e8)
![pipeline03](https://github.com/user-attachments/assets/28171b4d-7293-42b1-9516-d4f6c0308d8d)
![pipeline02](https://github.com/user-attachments/assets/2f69602e-aa19-4d95-902c-5a5fb37224d9)
![pipeline01](https://github.com/user-attachments/assets/54c06a69-ceef-4ed6-8521-8347bbf044b9)
![AlertsRules](https://github.com/user-attachments/assets/8f284431-3b77-4bd5-8cf9-61e7f55e1a3d)
![AlertsEmail2](https://github.com/user-attachments/assets/9f59d3cd-ba67-417e-be49-9ca23572a132)
![AlertsEmail](https://github.com/user-attachments/assets/9f46ebe3-71dc-4330-86ac-b67b637d370d)

![Alerts](https://github.com/user-attachments/assets/c67d9326-27a3-49e5-8090-7616ec7d1086)



