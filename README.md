Tech Challenge - Inteligência de Dados PNAD-COVID-19 🏥📊
Este repositório contém a solução desenvolvida para o Tech Challenge (Fase 3), simulando a contratação como Expert em Data Analytics para um grande centro hospitalar. O objetivo é analisar o comportamento populacional durante a pandemia para fundamentar o planejamento estratégico contra novos surtos.

🎯 O Problema de Negócio
O hospital necessita identificar indicadores clínicos, demográficos e econômicos que auxiliem na antecipação de demandas hospitalares. Utilizamos a base PNAD-COVID-19 do IBGE para responder:

Quais sintomas são os melhores preditores de internação?

Como a situação econômica (Home Office) afetou a taxa de contágio?

Qual o perfil demográfico mais vulnerável em nossa região?

🏗️ Arquitetura da Solução (Data Lakehouse)
Implementamos uma arquitetura escalável na nuvem AWS seguindo o padrão Medallion (Bronze, Silver e Gold).

Stack Tecnológica:
Linguagem: Python (PySpark), SQL.

EDA: Google Colab (Análise Exploratória Inicial).

Storage: Amazon S3 (Data Lake).

Catálogo: AWS Glue Crawler.

Processamento/ETL: AWS Athena (Presto SQL).

Visualização: Google Looker Studio.

🛠️ O Pipeline de Dados
1. Camada Bronze (Raw)
Ingestão dos microdados brutos do IBGE (Maio a Julho) no S3 em formato CSV.

Execução do AWS Glue Crawler para descoberta automática de schema e criação do catálogo no Data Lake.

2. Camada Silver (Refined & Cleaned)
Nesta fase, realizamos o tratamento crítico dos dados via AWS Athena.

Desafio Técnico: Identificamos um deslocamento de colunas (Schema Evolution) nos arquivos originais do IBGE. Variáveis de saúde (B009B) estavam desalinhadas com valores monetários.

Solução: Aplicamos um remapeamento manual via SQL (Data Wrangling), garantindo a integridade das 20 variáveis selecionadas.

Otimização: Conversão dos dados para tipos eficientes (BigInt, Double) e seleção de colunas estratégicas como idade, tem_falta_ar, resultado_swab e home_office.

3. Camada Gold (Analytics)
Os dados refinados alimentam dashboards executivos no Looker Studio, permitindo o cruzamento de dados clínicos com fatores socioeconômicos.

📋 Dicionário de Variáveis (Top 20)
Selecionamos 20 variáveis críticas divididas em 5 eixos:

Identificação: V1032 (Peso), V1013 (Mês), UF.

Demografia: A002 (Idade), A003 (Sexo), A004 (Raça), A005 (Escolaridade).

Clínico: B0011 (Febre), B0014 (Falta de Ar), B00111 (Odor/Sabor).

Saúde: B002 (Atendimento), B005 (Internação), B009B (Resultado SWAB).

Econômico: C001 (Ocupação), C013 (Home Office).

📈 Principais Insights
Falta de Ar como KPI: A variável B0014 mostrou-se o principal indicador antecedente para ocupação de leitos.

Impacto do Isolamento: Cruzamento entre C013 (Home Office) e B009B (Positividade) revelou a eficácia das medidas de trabalho remoto na redução da carga hospitalar.

Volume: Processamento de mais de 1.1 milhão de registros com 100% de integridade após tratamento.

👤 Autor
Joe Allan Zirn

LookerStudio: (https://www.linkedin.com/in/joe-allan-zirn-2bb0b62b1/)
LinkedIn: (https://www.linkedin.com/in/joe-allan-zirn-2bb0b62b1/)
