# Documeto de Arquitetura

## 1. Introdução

### 1.1 Objetivo 

Este documento tem como finalidade mostrar uma visão geral sobre a arquitetura e ferramentas utilizadas no projeto Parlamentaqui.

### 1.2 Escopo

O Parlamentaqui tem como objetivo ser uma plataforma web responsiva que possibilite visualizar perfis de deputados contendo noticias, dados dos mesmos e coisas relevantes a um deputado, além de mostrar twittes recentes desses deputados caso possuam a rede social. 

### 1.3 Definições, Acrônimos e Abreviações

- API: Application Programming Interface.
- Framework: Conjuntos de funções e componentes pré definidos.
- ETL: Extract, Transform and Load

## 2. Representação de Arquitetura

O projeto foi modelado seguindo a arquitetura de microserviços utilizando API's para realizar a conexão entre os serviços e o frontend da aplicação. 

A arquitetura de microserviços foi escolhida por ser altamente escalável, pela acessibilidade para os desenvolvedores sendo mais fácil entender os serviços individualmente e por consequentcia os ciclos de desenvolvimentos poderem ser mais rapidos. Estes fatores já poderiam ser suficientes para a escolha desta arquitetura no projeto mas ainda resta a maior resiliencia do projeto, ou seja o projeto fica mais tolerante a falhas, um exemplo disso é caso ocorra alguma falha em um dos serviços isso não afeta os outros pois cada um deles funciona independente do outro.

Com todos os ambientes e coordenando-os, construimos uma arquitetura de Microserviços integrada realizando o processo de ETL de forma correta e assim ao fim do projeto sejam apresentados dados relevantes para o nosso usuário final.

### 2.1 Arquitetura de Microserviços

A arquitetura orientada a micro serviços foi escolhida para este projeto por motivo das suas vantagens levando em relação a estrutura monolítica, dentre elas estão:

- Resiliencia ou seja o projeto fica mais tolerante a falhas.
- Altamente escalável
- Otimização da utilização da infraestrutura.
- Diminuição da complexidade de manutenção.

### 2.2 Processo de ETL

O processo de etl (Extract, Transform and Load) em si é um processo de extração de dados, e após essa extração há um tratamento destes dados e por fim o carregamento deles em uma base de dados.

![2.2 Processo de ETL](./img/etl.png)

Na fase de extração os dados podem vir das mais diversas formas além de ocorrer casos onde existem mais de uma fonte de dados. Por esses motivos é necessário na fase seguinte que é transformar esses dados, pegando apenas a parte que é interessante para o nosso produto deizando livre de inconsistencias e assim deixando os dados compativeis com as regras de negócio que foram definidadas para o nosso projeto.

Com esse procedimento realizado corretamente somente deverá ocorrer o carregamento destes dados no banco de dados escolhido para a nossa aplicação.

### 2.3 Tecnologias 

- React
- Python Flask
- Docker
- PostgreSQL
- Travis CI
- Git

## 3. Metas e Restrições da Arquitetura

### 3.1 Metas do Software Parlamentaqui

- Dar acesso a uma home com as últimas interações de políticos no twiter / perfis de politicos e atividades relacionadas (ordenação de acordo com atividades recentes);
- Mostrar projetos votados recentemente, com informações sobre os projetos em seu perfil.
- Possibilitar o compartilhamento inteligente.

Para mais informações vá no documento redigido a partir do [lean inception](./lean_inceptio.md) que contém detalhadamente as metas do projeto.

### 3.2 Restrições da Arquitetura

- O deputado possuir a rede social do twiter.
- As noticias com o deputado citarem seu nome em algum trecho da noticia.

## 4. Arquitetura dos Serviços e visão de Implementação

### 4.1 Visão Geral

![4.1 Visão Geral](./img/arquitetura2.png)

### 4.2 Microserviços e camadas

A arquitetura e sua versão atual está particionada em:

- **Front-End**

O front-end é a fronteira é responsável por incorporar os dados armazenados fornecidos pelo Gateway apresentando  os mesmos para o usuário final.

- **Gateway**

Fronteira responsável pela  junção de todos os endpoints em somente um local,   é o local responsavel por persistir e manter os dados relevantes para o produto. Através de uma API, disponibiliza os dados para o Front-End.

- **Dados abertura camara**

O "Dados abertura camara" é a fronteira responsável por realizar o processo de ETL, pela extração dos dados da API **dados abertos da camaras**, tratamento e separação de dados relevantes, e carregamento no DB.

- **Twitter**

O "Dados abertura camara" é a fronteira responsável por realizar o processo de ETL, pela extração dos dados da API **Twitter**, tratamento e separação de dados relevantes, e carregamento no DB.

- **Noticias**

O "Dados abertura camara" é a fronteira responsável por realizar o processo de ETL, pela extração dos dados da API **Google News (Brasil) API**, tratamento e separação de dados relevantes, e carregamento no DB.


- **TSE**

O "Dados abertura camara" é a fronteira responsável por realizar o processo de ETL, pela extração dos dados da API **TSE**, tratamento e separação de dados relevantes, e carregamento no DB.


## 5 Visão de dados

### 5.1 Dados abertos camara

![Representação de Arquitetura](./img/dados/dados_abertos.png)

### 5.2 Twitter

![Twitter](./img/dados/twitter.png)


### 5.3 Noticias

![Noticias](./img/dados/noticias.png)


### Referências

Silva Gomes da Gama e Abreu, Fábio. DESMISTIFICANDO O CONCEITO DE ETL

 - http://www.fsma.edu.br/si/Artigos/V2_Artigo1.pdf

Newman, Sam. Building Microservices.

- https://www.nginx.com/wp-content/uploads/2015/01/Building_Microservices_Nginx.pdf

ETL (extrair, transformar e carregar)

- https://docs.microsoft.com/pt-br/azure/architecture/data-guide/relational-data/etl


Símbolos e notação de diagramas entidade-relacionamento:

- https://www.lucidchart.com/pages/pt/simbolos-de-diagramas-entidade-relacionamento

