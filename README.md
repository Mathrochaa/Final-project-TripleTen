# Telecom US: Análise de Eficiência Operacional e Gargalos Sistémicos

## Visão Geral do Projeto
Este projeto tem como objetivo realizar um diagnóstico profundo da infraestrutura de atendimento e do desempenho da equipa de operadores da operadora de telefonia virtual Telecom US. 

Através de uma abordagem estritamente baseada em dados, abandonámos metas arbitrárias e utilizámos metodologias estatísticas para isolar comportamentos anómalos de funcionários e descobrir falhas estruturais críticas no sistema de telefonia que geram alto risco de cancelamento de clientes (churn).

## Principais Descobertas

1. A Regra dos 30% (Identificação Dinâmica de Ineficácia):
   - Em vez de definir limites de forma arbitrária, aplicámos o Percentil 85 sobre a distribuição da operação.
   - Limites matemáticos encontrados: Espera Máxima de 342,1s e Taxa de Perda Máxima de 17,7%.
   - Resultado: 30,0% da equipa (328 operadores) foi sinalizada para intervenção cirúrgica dos Recursos Humanos por cruzar ao menos um destes dois limites.

2. O Gargalo Crítico do Plano A:
   - Um teste ANOVA comprovou que o plano tarifário impacta o tempo de espera.
   - O sistema do Plano A possui um gargalo estrutural grave, retendo clientes na fila por 599,75 segundos (~10 minutos), enquanto os planos B e C operam abaixo de 3 minutos.

3. O Desperdício em Campanhas Ativas (Outbound):
   - Um teste Qui-Quadrado rejeitou a igualdade entre a direção das chamadas.
   - O atendimento recetivo (Inbound) é altamente eficiente (apenas 5,3% de perda). Em contrapartida, as ligações ativas (Outbound) têm um desperdício crónico de 46,6%, indicando o uso de listas de contactos (leads) obsoletas.

## Metodologia e Técnicas Aplicadas

- Pré-Processamento Rigoroso: Tratamento de datas (fuso horário UTC), remoção de duplicatas exatas e retenção proposital de operator_id nulos para não mascarar as chamadas abandonadas na fila.
- Limiares Dinâmicos (P85): Lógica disjuntiva (OU) isolando as piores caudas da distribuição para mapeamento de RH.
- Testes de Hipóteses: 
  - ANOVA (F-Test) para análise de variância múltipla (Planos Tarifários).
  - Qui-Quadrado de Independência para dados categóricos/proporcionais (Direção da Chamada).
- Visualização de Dados: Gráficos de dispersão e barras (Seaborn/Matplotlib) e criação de painéis executivos no Tableau.

## Estrutura do Repositório

- telecom_dataset_us.csv e telecom_clients_us.csv: Conjuntos de dados brutos (entradas).
- notebook_analise_telecom.ipynb: Código fonte completo com a análise em Python.
- relatorio_executivo_final_30pct.pdf: Apresentação formal das conclusões formatada para a Diretoria.
