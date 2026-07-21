# 📊 Dashboard Analytics: Mapeamento de CNPJs no Brasil (Power BI)

![Power BI](https://img.shields.io/badge/Power_BI-F2C94C?style=for-the-badge&logo=powerbi&logoColor=black)
![DAX](https://img.shields.io/badge/DAX-00758F?style=for-the-badge&logo=databricks&logoColor=white)
![Power Query](https://img.shields.io/badge/Power_Query-00838F?style=for-the-badge&logo=microsoft&logoColor=white)
![Parquet](https://img.shields.io/badge/Parquet-563D7C?style=for-the-badge&logo=apache&logoColor=white)

---

## 📌 Visão Geral do Projeto

Este repositório contém a camada de **Modelagem Dimensional e Visualização de Dados (Power BI)** referente ao mapeamento dos estabelecimentos cadastrados na Receita Federal do Brasil.

> ⚡ **Nota de Metodologia e Performance:**  
> Para garantir uma experiência de navegação rápida, fluida e acessível na web — evitando lentidão no carregamento dos gráficos em dispositivos móveis e computadores —, este painel foi construído a partir de uma **amostra estatística representativa de 10%** dos dados da Receita Federal do Brasil do 1º semestre de 2026 (*mês de referência: Junho/2026*).  
> 
> Apesar de corresponder a 1/10 da base total, a amostragem abrange **mais de 4,5 milhões de registros reais**, volume mais do que suficiente para garantir alta precisão analítica na identificação de padrões, distribuições geográficas (UF/Municípios), porte de empresas e enquadramentos tributários.

---

## 📐 Arquitetura do Modelo Dimensional (Star Schema)

A modelagem de dados foi desenhada seguindo rigorosamente a metodologia **Kimball (Star Schema)**. A base tratada foi dividida em uma **Tabela Fato** e quatro **Tabelas Dimensão**, otimizando a memória do motor *VertiPaq* e acelerando o tempo de resposta do DAX.

```text
                  +-------------------+
                  |      dCNAE        |
                  | (Cod_CNAE - PK)   |
                  +---------+---------+
                            | 1
                            |
                            | *
+-------------------+     +-+-----------------+     +---------------------+
|     dEmpresa      | 1 * | fEstabelecimentos | * 1 |      dMunicipio     |
| (CNPJ_Basico-PK)  +-----+ (Fato Principal)  +-----+ (Cod_Municipio-PK)  |
+-------------------+     +-+-----------------+     +---------------------+
                            | *
                            |
                            | 1
                  +---------+---------+
                  |    dCalendario    |
                  | (Date - PK)       |
                  +-------------------+





