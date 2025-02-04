---
title: RELATÓRIO DE CUMPRIMENTO DO OBJETO ETAPA II - Ecossistemas de Software Livre - Abril 2018
author: Carla Silva Rocha Aguiar (Coordenadora do Projeto)
date: 02 de Maio de 2018
geometry: "left=3cm,right=3cm,top=2cm,bottom=2cm"
colorlinks: true
---

# Introdução

O presente relatório apresenta o acompanhamento do trabalho realizado no
projeto "Ecossistemas de Software Livre", Termo de Cooperação para
Descentralização de Crédito, Processo Ofício No 0646/2017/FUB-UnB, Vigência
Outubro 2017 à Outubro 2019. O relatório apresentado é referente aos avanços
realizados na Etapa II (Janeiro 2018 à Março 2018), de acordo com o cronograma
do Plano de Trabalho.

Toda alteração no cronograma proposto foi realizada  a partir de renegociação
com a CGTEC do Ministério da Cultura, e tais alterações estão descritas no
relatório.

## FASE DE PLANEJAMENTO/EXECUÇÃO

O período de Janeiro 2018 à Março de 2018 contemplou as fases de
planejamento e execução. Abaixo serão apresentados, brevemente, os principais
avanços alcançados no período. Toda a documentação e acompanhamento do projeto
está disponibilizado e pode ser acessado na organização do laboratório
[lappis-unb](https://github.com/lappis-unb), e no
repositório específico do projeto
[lappis-unb/EcossistemasSWLivre](https://github.com/lappis-unb/EcossistemasSWLivre).
Todo o planejamento e execução das tarefas podem ser acompanhados tanto nas
_issues_ quanto nas páginas _wiki_.

Abaixo serão apresentados os principais avanços alcançados no período, por
pacote de trabalho (de acordo com o Plano de Trabalho),
de acordo com o cronograma, no período citado.

### Legado em Software Livre <!-- {{{ -->

Os repositórios presentes na organização MinC não possuem uma padronização:
muitos deles tem pouca ou nenhuma documentação, alguns nem possuem licenças de
software, testes automatizados, integração contínua, métricas de qualidade de
código. A pouca conformidade com os modelos seguidos por comunidades de
software livre, dificulta ou limita a contribuição de interessados em coloborar
com os sistemas MinC.

Muitos sistemas legados carecem de testes automatizados, boa documentação e
práticas de desenvolvimento contínuo, o que dificulta enormemente qualquer
forma de evolução. Estes também são fatores críticos na curva de aprendizado de
novos desenvolvedores e criam uma barreira para a existência de comunidades de
software livre/aberto colaborando com tais sistemas. Vários projetos mantidos
pelo Ministério da Cultura possuem as características acima citados.

Durante a primeira etapa do projeto foi priorizado a visão "legacy in the box" (legado
em uma caixa, tradução literal), no qual o foco foi isolar alguns projetos
mantidos pelo Ministério da Cultura por meio de Docker[^docker]. Essa solução gera o
benefício de criar ambientes de desenvolvimento e produção estáveis, fazendo
com que diminua o tempo de configuração de ambiente. Essa abordagem traz um
grande benefício pois possibilita o uso de práticas DevOps mesmo em sistemas
legados. Esse modelo de isolar pacotes de software legados através de containers Docker possibilita um pipeline de
entrega contínua, deploy contínuo, e diminui a fronteira entre a equipe de
infraestrutura e equipe de desenvolvimento.
Já foram observados benefícios dessa abordagem, principalmente em feedback de
desenvolvedores e mantenedores da infraestrutura, feito de forma espontânea.
Pretende-se ainda fazer tanto uma avaliação qualitativa quanto quantitativa
dessa abordagem.

[^docker]: Docker fornece uma camada adicional de abstração e automação de virtualização de nível de sistema operacional. [http://www.docker.com](http://www.docker.com)

Nessa segunda etapa do projeto, usamos uma segunda forma de lidar com software
legado, sempre com o intuito de aplicar técnicas modernas de Engenharia de
Software e padrões de comunidade de software livre, a fim de viabilizar o uso
desses projetos legados em outros contextos e em pipelines
automatizados. O foco então foi transformar um software legado em software
livre, a partir de técnicas de refatoração de código, e suite de testes
automatizados.

Com isso, abordamos um dos objetivos do pacote que é "Pesquisa em
metodologias de refatoração de sistemas legados", adotando padrões de
comunidades de software livre: desde
documentação técnica, quanto código de qualidade (respeitando métricas de
qualidade de software), cobertura de testes, suite de testes automatizado,
ferramenta de integração contínua, e pipeline de deploy contínuo. Para que
pudéssemos alcançar esses objetivos, foi escolhido a API do Salic como estudo
de caso, uma vez que esse é um sistema relativamente pequeno, de grande
relevância e impacto no ecossistema Salic. A compreensão da API do Salic também
auxilia no pacote de trabalho "Aprendizado de Máquina Lei Rouanet", uma vez que
grande parte do trabalho consiste em acessar e processar dados providos da API
(e demanda de dados geram demandas para a evolução da mesma).

As ações programadas para esta etapa de acordo com o plano de trabalho foram:

- [x] Realizar Estudos de conteinerização;
- [x] Realizar Estudo de refatoração em software legado;
- [x] Realizar Estudos sobre práticas de DevOps aplicada a software legado.

Grande parte do time foi alocado por dois meses nessa grande tarefa de
refatorar a API do Salic, e os principais avanços alcançados nessa etapa foram:

1. Adicionada instalação automazada do ambiente de desenvolvimento através do
   Virtualenv[^venv] e do Docker, a documentação está no [README](https://github.com/lappis-unb/salic-api/blob/master/README.rst).
1. A qualidade do código foi melhorada através das seguintes atividades:
    * Os SQL's em forma de textos foram refatorados, agora é utilizado o
      SQLAlchemy[^sqlalchemy]. Essa refatoração melhora a manutenibilidade[^manutenibilidade] do código e
      também permite que a API do Salic funcione com qualquer banco de dados que o
      SQLAlchemy oferece suporte;
    * O Python utilizado no projeto foi atualizado para a versão 3
      (originalmente era utilizado a versão 2 do Python);
    * Utilização do Flake8[^flake] para melhorar a estrutura do código;
    * Adicionado banco de dados local para o ambiente de desenvolvimento;
    * Classificação no Code Climate foi de "F" para "A", resultado da redução
      do débito técnico;
    * Criados testes para os endpoints da API, onde é testado se os dados das
      requisições são recebidos corretamente;
    * Adicionada integração, build e deploy contínuo;
    * Documentação do projeto atualizada.

[^manutenibilidade]: Manutenibilidade é uma característica de produtos de software referente à facilidade, precisão, segurança e economia na execução de ações de manutenção. [https://pt.wikipedia.org/wiki/Manutenibilidade](https://pt.wikipedia.org/wiki/Manutenibilidade)

[^venv]: Virtualenv é um simulador de ambientes virtuais isolados para projetos Python. [http://virtualenv.pypa.io/](http://virtualenv.pypa.io/)
[^sqlalchemy]: SQLAlchemy é uma biblioteca Python de mapeamento objeto-relacional SQL. [http://www.sqlalchemy.org/](http://www.sqlalchemy.org/)
[^flake]: [http://flake8.pycqa.org](http://flake8.pycqa.org)

A mudança da utilização de strings SQL para o código Python usando SQLAlchemy
ocorreu para que além de melhorar a manutenção do código, o SQLAlchemy possui
otmizações e suporte para se conectar com outros sistemas de banco de dados,
por exemplo, caso o Salic passe a utilizar o PostgreSQL todo o sistema da
API Salic continuará funcionando corretamente.

O Flake8 é uma ferramenta de análise estática de código que confere algumas
normas que deixam o código mais legível, padronizado e manutenível, a
refatoração do código utilizando o Flake8 visou melhorar a manutenção do
API adequando o código as normas do Flake8.

Antes da refatoração não era possível levantar um ambiente de desenvolvimento,
pois era necessário estar conectado ao banco de dados do Salic, porém agora,
com o banco de dados local quem quiser contribuir com o projeto pode levantar
o ambiente em seu próprio computador e usar um banco SQLite local, além disso,
para se conectar a um banco de dados basta setar algumas variáveis de ambiente
e o desenvolvedor pode conectar a um banco de dados remoto, como
por exemplo um banco de dados de homologação.

Foi utilizado o Code Climate, um sistema que analisa a qualidade do
código-fonte e atribui uma classificação ao projeto, essa ferramenta verifica
diversas métricas de qualidade de software, como por exemplo duplicação de código informando em quais pontos estão estas duplicações.

Os testes da API foram criados para que ao realizar manutenção no código
seja possivel ter uma garantia de que não foi introduzido bugs no sistema,
anteriormente era difícil saber se o
sistema está funcionando corretamente após o término de uma manutenção. Também
foram criados testes que comparam os resultados das requisições ao novo projeto de API
refatorado com a API original que está atualmente em produção, para se ter uma
garantia de que ao atualizar para a nova versão em produção os sistemas que usam a API
irão continuar funcionando.

Afim de facilitar a adição de novas funcionalidades ao
sistema em produção de forma mais rápida e prática, foi criado uma pipeline de
deploy contínuo, onde é executado os testes do projeto, é checado se a build
está sendo gerada corretamente e depois é feito o deploy para o servidor.

Todas as melhorias implementadas acima, fez com que o projeto da API do Salic
atendesse os padrões de comunidades de software livre, além de atender os
requisitos de DevOps para entrega e deploy contínuo (build de testes). Para
tal, foram realizados ao total 300 commits (no qual foi aberto um pull request
para o projeto no repositório do MinC). A API foi  então colocado em um
ambiente de homologação no laboratório Lappis, e após todos testes passarem nesse
periodo de homologação, o projeto será entregue para o Ministério.

O acompanhamento do projeto realizado pode ser encontrado em
[https://github.com/lappis-unb/salic-api](https://github.com/lappis-unb/salic-api).

<!-- }}} -->

### Catálogo de Softwares Culturais <!-- {{{ -->

O principal objetivo nessa etapa é exercitar em todo ciclo de projeto a
experimentação e inovação contínua, de forma a subsidiar a pesquisa realizada
na Etapa 5. Nesse período foram abordados dois objetivos desse pacote:
"Aplicação de práticas de experimentação e inovação contínua no desenvolvimento
do projeto de Catálogo de Software Culturais", e "Transferência de conhecimento
e capacitar a equipe de servidores e técnicos do MinC em práticas de gestão e
desenvolvimento de software aberto, colaborativo e contínuo".

Ações programadas para esta etapa de acordo com o plano de trabalho estão
listados abaixo:

- [x] Realizar Estudos de tecnologias e práticas devops;
- [x] Realizar Estudos repositórios MinC;
- [x] Elaborar Relatório de Resultado dos Estudos;
- [ ] Realizar estudos sobre funcionalidades de catálogo de software.



Grande parte do objetivo de transferência de conhecimento e capacitação da
equipe de servidores técnicos do MinC foi concentrado nesse período em práticas
DevOps. Para tal, além de encontros técnicos para apresentação das práticas
experimentadas no laboratório, alguns documentos técnicos foram elaborados para
tal fim. Grande parte do time ficou focado em amadurecer o pipeline devops, atualizar
o pipeline dos softwares do Minc trabalhados no laboratório (Salic API, Salic, Mapas culturais), além de
gerar a documentação técnica do conhecimento adquirido.
 Toda a documentação foi disponibilizada no repositório do laboratório em
[https://gitlab.com/lappis-unb/docs](https://gitlab.com/lappis-unb/docs),
disponibilizada também como anexo no final deste documento, os documentos
cobrem tanto a primeira quanto a terceira meta do período.

Foi elaborado documentação/relatório descrevendo todo o pipeline usado para
deploy contínuo no laboratório com os seguintes tutoriais, que podem ser aplicados em diversos contextos:

1. GitLab CI/CD: Guia relacionado ao uso da Integração Contínua e Deploy
   contínuo no Gitlab;
1. Overview e exemplo básico(pt-br): Um guia que ensina como usar o gitlab
   CI/CD para gerar integração contínua e deploy contínuo em um projeto básico;
1. Usando Docker Compose (pt-br): Um guia que ensina como usar o GitLab CI/CD
   para gerar integração contínua com o Docker Compose em um projeto ágil;
1. Integrando GitLab CI/CD com projeto GitHub(pt-br): Um procedimento que
   possibilita o uso do GitLab CI/CD no projeto GitHub.

Toda a documentação foi realizada em português e disponibilizada para acesso.

Referente à segunda meta "Realizar Estudos repositórios MinC" nesse período foram finalizadas
o checklist dos projetos/repositórios priorizados pelo ministério e também aprofundado o estudo sobre
 as funcionalidades do Salic e como a execução da lei
Rouanet é realizada no Salic. Foram realizadas diversas reuniões técnicas com a
equipe da SEFIC, desde a equipe responsável pela admissibilidade até a equipe
responsábel pela avaliação de resultados. Os objetivos dessas reuniões foram:
(a) compreender o processo (fases, etapas) da Lei Federal de Incentivo à Cultura, (b) identificar
os principais envolvidos/stakeholders em cada etapa, (c) levantar os principais
pontos de melhoria. A partir desses levantamentos, vamos na próxima etapa,
propor melhorias, ou por meio do assistente virtual (chatbot) ou por meio de
algoritmos de aprendizagem de máquinas ou mesmo por meio de novos requisitos para o Salic.

Referente à última meta "Realizar estudos sobre funcionalidades de catálogo de
software", foi feito um levantamento, juntamente com a CGTEC, da necessidade de se desenvolver um catálogo de software
como previsto no plano de trabalho. Foram levantados como alguns governos lidam com o portifólio de projetos software livre, tais como as iniciativas do governo inglês de trabalhar majoritamente com software livre
[https://governmenttechnology.blog.gov.uk/2016/12/15/next-steps-for-open-source-in-government/](https://governmenttechnology.blog.gov.uk/2016/12/15/next-steps-for-open-source-in-government/), e manter seu catálogo de software na própria organização github [http://gds-operations.github.io/](http://gds-operations.github.io/). Observamos também uma tendência mundial do uso de software livre no governo (egovernment - [http://www.egov4dev.org/success/definitions.shtml](http://www.egov4dev.org/success/definitions.shtml)), com uma quantidade crescente de adesão [https://government.github.com/community/](https://government.github.com/community/), [https://github.com/g0v](https://github.com/g0v). Observamos que o próprio repositório, organização, e wiki do repositório são utilizados para compor o catálogo de software. Como o principal objetivo dessa etapa é executar um ciclo completo de projeto, de comum acordo com a CGTEC, decidimos não desenvolver o catálogo de software, como previsto no calendário. Para atender o objetivo principal da etapa, o ciclo completo de projeto será realizado no pacote de trabalho "Aprendizado de Máquina Lei Rouanet". A equipe devops manteve na frente catálogo, e os demais integrantes da frente foram realocados para o pacote de trabalho "Aprendizado de Máquina Lei Rouanet". Essa última mudança foi motivada pela prioridade e importância dadas tanto pela CGTEC quanto SEFIC em relação ao chatbot e à frente aprendizagem de máquina. Isso fez com que o cronograma de entregas fossem encurtados, justificando o aumento das equipes para garantir tais entregas. Porém, não houveram alterações no processo administrativo dos membros das equipes, e como visto na análise financeira, parte da equipe manteve alocada no pacote de trabalho "Catálogo de Softwares Culturais".


<!-- }}} -->

### Práticas de gestão colaborativa <!-- {{{ -->

Nessa etapa será realizada uma pesquisa exploratória tendo como objeto de
estudo os movimentos, organizações, desenvolvedores e demais stakeholders que
atuam na gestão colaborativa de software livre. O principal objetivo do
trabalho de gestão colaborativa dessas comunidades de software livre é manter
um conjunto de ações de governança digital e comunicação que aproveite ao
máximo esse potencial em favor das necessidades do órgão e das metas comuns às
organizações parte das comunidades. Esse esforço envolve um trabalho de
mapeamento de atores de cada comunidade (atuais e potenciais futuros),
assessoria para planejamento conjunto, facilitação de fluxos de comunicação e
mobilização, realização de atividades conjuntas para integração, identificação
de oportunidades externas, assessoria para comunicação e divulgação ao público
externo à comunidade e apoio para solução de conflitos.

Ações programadas para esta etapa de acordo com o plano de trabalho:

- [x] Realizar Estudos sobre processo de planejamento conjunto;
- [x] Identificar grupos de opinião.

Todas as atividades relacionadas as ações listadas acima foram 100% finalizada.
Nessa etapa, foi focado na estratégia de colaboração entre os laboratórios de
pesquisa que contribuem para os repositórios MinC:

1. Frente de metodologias ágeis e DevOps: Por ser uma prática comum ao Lappis,
   oriunda da própria história do laboratório e reforçada pelas disciplinas
   práticas da FGA/UnB, é um ativo que pode ser compartilhado na comunidade de
   laboratórios;
    - Oficinas para intercâmbio de método de trabalho (funcionamento das
      sprints, wikis, decisão sobre pull requests etc) - Maio ou junho/2018;
    - Evento prático de DevOps para apresentar o resultado da pesquisa e fazer
      intercâmbio prático;
1. Frente de tecnologias livres para chatbots: Pela carência de tecnologias
   livres desse tipo e as inúmeras aplicações na qualificação dos serviços
   públicos essa pode ser uma oportunidade para os outros laboratórios. O Lappis
   pode auxiliar a incorporação dessa tecnologia nos serviços digitais em
   desenvolvimento pelos outros laboratórios, assim como já está fazendo com o
   Salic e pode fazer com o Mapas Culturais;
    - Lançamento da tecnologia no MinC e Workshop técnico na semana seguinte
      para os interessados em conhecer/colaborar na tecnologia;
    - Incorporação de metas estratégicas conjuntas para DevOps e chatbots em
      outros serviços digitais do MinC;
    - Implementação de boas práticas para governança da comunidade em torno
      desse ativo tecnológico (chatbots) visando aumento da contribuição de
      desenvolvedores externos ao Lappis, com foco nos times dos laboratórios
      parceiros;
1. Frente de Governança de Comunidades: Essa frente envolve pesquisa e
   realização de eventos conjuntos com temas estratégicos para a colaboração
   aberta nas tecnologias desenvolvidas e mantidas pelo Estado.

Intercâmbio de pesquisa através do compartilhamento de referências e produção
conjunta de artigos - Seminário Interno com UFG - Jul/2018 à Out/2018.

Realização de eventos conjuntos sobre o tema da Governança de Comunidades Open
Source com adesão do Estado e Contratação Pública de TICs - Maio ou junho/2018.

<!-- }}} -->

### Aprendizado de Máquina Lei Rouanet <!-- {{{ -->

O principal objetivo é o estudo de técnicas de Aprendizado de Máquina que
possam apoiar o sistema de recomendação e fiscalização da Lei Federal de Incentivo à Cultura (Lei Rouanet). Nessa
etapa será realizada uma pesquisa exploratória em técnicas de aprendizado de
máquina e processamento de linguagem natural. Tais técnicas e algoritmos serão
aplicados para melhorar a experiência de usuário (UX) por meio da proposta de
chatbots como interface entre os proponentes na Lei Rouanet e o Ministério da
Cultura.

Além disso, técnicas de aprendizado de máquinas serão estudadas para
automatizar processos nas trilhas de auditorias, tanto na etapa de habilitação
e aprovação, quanto na etapa de prestação de contas. O objetivo é auxiliar
auditores a encontrar erros, inconsistências e detectar anomalias nas
submissões.

Ações programadas para esta etapa de acordo com o plano de trabalho:

- [x] Realizar Estudo Lei Rouanet/SALIC;
- [x] Realizar Estudo de aprendizado de máquina;
- [x] Realizar Estudo processamento linguagem natural;
- [x] Realizar Estudos de chatbots.

Todas as atividades relacionadas as ações listadas acima foram 100%
finalizadas. Segue resumo da execução das atividades:

Foi desenvolvido uma versão inicial do bot -- versão 0.1 (beta) -- com o
framework Hubot Natural[^hubot], o desenvolvimento aconteceu após estudos sobre
ferramentas para criação de chatbots. Decidiu-se utilizar o Rocket.Chat como
interface para o chatbot, compondo a solução em conjunto com o Hubot Natural.

[^hubot]: Hubot Natural é um chatbot de Processamento de Linguagem Natural para o Rocket.Chat. [https://github.com/RocketChat/hubot-natural](https://github.com/RocketChat/hubot-natural)

Realizou-se evolução do projeto Hubot Natural, com contribuições da equipe ao
repositório oficial do projeto. Além de colaboração com os desenvolvedores core
do projeto Rocket.Chat para avaliação do melhor caminho para futuras evoluções.

Esta primeira versão foi treinada com uma base de conhecimento criada a partir
de documentos disponibilizados pela ouvidoria da SEFIC, importante destacar que
neste primeiro treinamento foi incluido especialmente conhecimentos avançados
sobre a lei de incentivo, deixando de fora da base conhecimento básicos
necessários para responder adequadamente questões mais básicas.

Levantou-se um ambiente de homologação em [https://rouana.lappis.rocks](https://rouana.lappis.rocks), incluindo uma landing page da Rouana
com instruções de como validar e homologar o assistente virtual, onde através
da base de conhecimento criada a partir dos documentos disponibilizados pela
ouvidoria da SEFIC, avaliou-se a eficácia do chatbot através de testes de
usuários incluindo servidores do MinC, pesquisadores e alunos do Lappis.

Os testes realizados com chatbot versão 0.1 (beta) em ambiente de homologação
revelaram que o assistente virtual com as tecnologias selecionadas atende
perfeitamente as necessidades do projeto, indicando que o caminho trilhado até
o momento está em sintonia com a missão final de proporcionar um novo canal
aos cidadãos para compreender e tirar dúvidas sobre a lei Rouanet.

Os dados coletados e feedback dos usuários durante a fase de homologação serão
utilizados para direcionar a evolução e melhorias, identificou-se inicialmente
que a base de conhecimento necessita de evolução, especialmente com questões
mais simples.

Contribuimos com a documentação do repositório do Hubot Natural, incluindo
documentar o processo de configuração do LiveTransfer, tradução da documentação
do Hubot Natural para o inglês e adoção de solução de documentação para o
Hubot Natural.
Foi feito também levantamento de práticas e ferramentas para instrumentalização
com ferramentas para análise estática como Coffeelint e
Codeclimate, além de integração contínua ao projeto.

Realizou-se também pesquisa e implementação de melhores práticas de UX para
interfaces conversacionais, necessária para melhoria na experiência do usuário
ao utilizar o assistente virtual da lei Rouanet.

Em paralelo a todo este trabalho, estudou-se tecnologias para criação de uma
nova versão do bot, incluindo frameworks para criação de chatbots mais
inteligentes, exemplos: Rasa, AIVA, Botpress, IBM blue mix, Seq2seq,
Hubot-playbook e Neo4j.  Estes frameworks foram avaliados na prática e algumas
tecnologias foram analisadas em detalhes, como: Rasa-NLU + BotPress +
RocketChat e Rasa-core + Rasa-nlu.

A implementação da nova versão do bot foi iniciada em paralelo ao
desenvolvimento da versão 0.1 (beta) citada anteriormente, já utilizando uma
abordagem mais poderosa de desenvolvimento de bots; escolha de mudança de
arquitetura e tecnologias a serem usadas para a próxima versão do chat.

Em complemento ao desenvolvimento do chatbot realizamos estudos para
compreensão do processo de projetos incentivados via Lei Rouanet, incluindo
estudo de tecnologias de aprendizado de máquina a fim de auxiliar o processo de
admissão e prestação de contas do Salic.

Neste sentido, iniciou-se estudos e testes de algoritmos para detecção de
anomalias em itens das planilhas orçamentárias de projetos submetidos ao Salic,
utilizando técnicas de aprendizado de máquina, tanto na extração de
características relevantes para o problema (_Exploratory Data Analysis_ e _Data
Wrangling_), quanto na classificação de novos dados (usando modelos básicos de
regressão do módulo _Scikit-learn_).

São dois os objetivos dessa frente de trabalho:

1. Auxiliar o processo de admissão e prestação de contas do Salic: automatizar
   tarefas simples e repetitivas de tais processos para otimizar da criação à
   conclusão de projetos culturais;
2. Fornecer insumos para um sistema de transparência do Salic: fornecer
   métricas utilizadas para mapear as categorias e regiões de maior incentivo e
   para incentivar novos produtores culturais.

A frente está trabalhando na criação de uma API que deve se comunicar, a
princípio, com o Salic. Contudo, futuramente novos sistemas também podem
realizar requisições à API para extrair métricas sobre projetos culturais.

O desenvolvimento desta frente está sendo feito com o levantamento de hipóteses
e evolução da API. A metodologia utilizada é a _Hypothesis-Driven Development_,
focada em criação e validação contínua de hipóteses de aprendizado de máquina,
seguida de implementação na API das hipóteses confirmadas na etapa de
validação.

A API está em desenvolvimento em Python, utilizando-se o framework Django. Três
hipóteses já foram levantadas e estão sendo validadas:

1. Relação entre o tempo e a mudança dos preços de itens da planilha
   orçamentária de um projeto;
2. Identificação de itens superfaturados a partir do histórico de projetos
   aprovados e recusados e;
3. Categorização e identificação de similaridade de um projeto a partir de sua
   planilha orçamentária vigente.

Caso as hipóteses se confirmem, serão implementadas e será possível verificar,
para cada projeto, se sua planilha orçamentária contém itens possivelmente
superfaturados e quais os projetos mais similares com o projeto em questão.

<!-- }}} -->

### Aferição e aceitação de produtos de software <!-- {{{ -->

O objetivo geral desta frente de pesquisa é auxiliar os times de
desenvolvimento e gestores de TI do MinC a aprimorarem sua capacidade em tomar
decisões acerca da qualidade das versões dos produtos de software entregues por
seus fornecedores.

Ações programadas para esta etapa de acordo com o plano de trabalho:

- [x] Revisão da área;
- [x] Diagnóstico sobre as práticas atualmente adotadas pelo MinC de garantia da qualidade de produto;
- [ ] Elaborar Plano de Pesquisa-Ação.

Nessa etapa foram aplicadas surveys com os gestores do MinC e desenvolvedores
seniores do Lappis e MinC. O objetivo do survey foi fazer uma análise
qualitativa sobre o projeto e sobre práticas devops e práticas de comunidades
de software livre.

Nesse período também foi realizado a análise do survey aplicado aos alunos. O
resultado é apresentado em anexo.

<!-- }}} -->

# Acompanhamento Financeiro

![Detalhamento da execução do repasse na Etapa II.](figs/valores_executados_E2.png)

O valor do repasse referente à Etapa II foi de R$202.600,00. Todo esse repasse
foi na rubrica 30.90.20, referente à auxílio Financeiro a Pesquisa (Bolsas).
Desse repasse, um total de R$190.635,90 foi executado na Etapa II, representando
na prática que o orçamento foi consumido apenas na categoria mão-de-obra. Todo
esse valor foi executado no pagamento das bolsas do time, e o valor gasto por
frente do projeto pode ser visto na Figura 2 abaixo.

![Neste gráfico é possível observar a representação do percentual do custo da mão-de-obra incidido em cada equipe do projeto. A maior alocação de recursos encontram-se nas equipes do Catálogo de Softwares Culturais(representado pela cor azul), uma vez que grande parte das  funcionalidades desenvolvidas são providas através desta frente, e a equipe do Aprendizado de máquina(representado pela cor verde), que desenvolveu o chatbot.](figs/bolsas_E2.png){width=400px}

# Assinatura

Responsável pela Execução:
---
Nome:  Carla Silva Rocha Aguiar
             (Coordenadora do Projeto)

Assinatura:
![assinatura](figs/assinatura.png)

Data: 06/04/2018

# Anexo I - GitLab CI/CD <!-- {{{ -->

Este _doc_ tem por objetivo capacitar um _dev_ em utilizar o **GitLab CI/CD**
em projetos que exigem estruturas básicas de configuração. Para um melhor
aproveitamento deste _doc_ é recomendável ter realizado com completude o [guia
básico](guides/DevOps/GitLab-CI-CD/Overview-and-Basic-Example-(pt_br)).

## Introdução

[Docker Compose](https://docs.docker.com/compose/) é uma ferramenta para
definição e execução de aplicações de múltiplos _containers_ **Docker**.
Através de um arquivo de configuração [YAML](http://yaml.org/) é possível
definir os serviços da aplicação e suas interações. Esse arquivo é utilizado
como entrada em um CLI capaz de iniciar os serviços configurados em um simples
comando.

Enquanto o **Docker** permite a definição e o gerenciamento de um único
_container_, **Docker Compose** define e gerencia múltiplos _containers_ e suas
interações.

Dentre os principais benefícios, incluem:

* Facilidade de definição dos serviços;
* Uma vez definido o arquivo de configuração, o uso de simples comandos inicia a aplicação e todos os seus serviços (_containers_), incluindo suas interações;
* Ideal para desenvolvedores configurarem o ambiente local;
* É uma das camadas de configuração em orquestradores de _containers_ como [Kubernetes](https://kubernetes.io/) e [Cattle](https://github.com/rancher/cattle) (Orquestrador do [Rancher](https://rancher.com/))

Se o projeto da aplicação que estiver desenvolvendo utiliza **Docker Compose**
para definição do ambiente em nível de teste, desenvolvimento e/ou produção,
utilizar **Docker Compose** na integração contínua é uma opção.

# Utilizando Docker Compose no GitLab CI/CD

Para exemplificar o uso do **Docker Compose** no **GitLab CI/CD**, foi criado
um simples respositório chamado
[_characters_](https://gitlab.com/lappis-unb/internal/guides/examples/characters)
consolidando o uso das duas ferramentas no estágio de teste. Ao fim da leitura
deste exemplo você será capaz de reproduzir o uso do **Docker Compose** no
**CI/CD** do seu projeto.

## Projeto Modelo

O sistema _characters_ é um pequeno projeto
[Phoenix](http://phoenixframework.org/) com banco de dados em
[PostgreSQL](https://www.postgresql.org/) que define uma
[API](https://en.wikipedia.org/wiki/Application_programming_interface)
[RESTful](https://www.vinaysahni.com/best-practices-for-a-pragmatic-restful-api)
de uma única entidade chamada `Character`, conforme descrito no
[README](https://gitlab.com/lappis-unb/internal/guides/examples/characters/blob/master/README.md)
do projeto:

```javascript
// curl -X GET -H "Accept: application/json" {HOST}:{PORT}/api/v1/characters/1
"data": {
  "id": 1,
  "first_name": "Jon",
  "last_name": "Snow",
  "age": 14,
  "origin": "A Song of Ice and Fire"
}
```

### Rotas da API

As rotas, conforme especificado no comando `mix phx.routes`, são:

```javascript
// Apresenta todos os Characters
Rota: "GET /api/v1/characters",
Modelo de cURL: `curl -X GET -H "Accept: application/json" {host}:{port}/api/v1/characters`
Exemplo de resultado: {
  "data": [
    {
      "id": 1,
      "first_name": "Jon",
      "last_name": "Snow",
      "age": 14,
      "origin": "A Song of Ice and Fire"
    }, {
      "id": 2,
      "first_name": "Walter",
      "last_name": "White",
      "age": 50,
      "origin": "Breaking Bad"
    }, {
      "id": 3,
      "first_name": "Locke",
      "last_name": "Cole",
      "age": 25,
      "origin": "Final Fantasy VI"
    }, {
      "id": 4,
      "first_name": "Arthas",
      "last_name": "Menethil",
      "age": 24,
      "origin": "Warcraft III"
    }, {
      "id": 5,
      "first_name": "Dominick",
      "last_name": "Cobb",
      "age": 37,
      "origin": "Inception"
    }, {
      "id": 6,
      "first_name": "Vincent",
      "last_name": "Vega",
      "age": 27,
      "origin": "Pulp Fiction"
    }
  ]
}

// Apresenta o Character de id com o valor {:id}
Rota: "GET /api/v1/characters/:id"
Modelo de cURL: `curl -X GET -H "Accept: application/json" {host}:{port}/api/v1/characters/{:id}`
Exemplo de resultado: {
  "data": {
    "id": 1,
    "first_name": "Jon",
    "last_name": "Snow",
    "age": 14,
    "origin": "A Song of Ice and Fire"
  }
}

// Cria um novo Character
Rota: "POST /api/v1/characters"
Modelo de cURL: `curl -X POST -H "Accept: application/json" -H "Content-Type: application/json" -d '{"character":{"first_name":"{first_name}","last_name":"{last_name}","age":{age},"origin":"{origin}"}}' {host}:{port}/api/v1/characters`
Exemplo de dado: {
  "character": {
    "first_name": "Jon",
    "last_name": "Snow",
    "age": 14,
    "origin": "A Song of Ice and Fire"
  }
}
Exemplo de resultado: {
  "data": {
    "id": 1,
    "first_name": "Jon",
    "last_name": "Snow",
    "age": 14,
    "origin": "A Song of Ice and Fire"
  }
}

// Atualiza parcialmente o Character de id com o valor {:id}
Rota: "PATCH /api/v1/characters/:id"
Modelo de cURL: `curl -X PATCH -H "Accept: application/json" -H "Content-Type: application/json" -d '{"character":{"first_name":"{first_name}"}}' {host}:{port}/api/v1/characters/{:id}`
Exemplo de dado: {
  "character": {
    "last_name": "Stark"
  }
}
Exemplo de resultado: {
  "data": {
    "id": 1,
    "first_name": "Jon",
    "last_name": "Stark",
    "age": 14,
    "origin": "A Song of Ice and Fire"
  }
}

// Substitui o Character de id com o valor {:id}
Rota: "PUT /api/v1/characters/:id"
Modelo de cURL: `curl -X PUT -H "Accept: application/json" -H "Content-Type: application/json" -d '{"character":{"first_name":"{first_name}","last_name":"{last_name}","age":{age},"origin":"{origin}"}}' {host}:{port}/api/v1/characters/{:id}`
Exemplo de dado: {
  "character": {
    "first_name": "João",
    "last_name": "das Neves",
    "age": 15,
    "origin": "As Crônicas de Gelo e Fogo"
  }
}
Exemplo de resultado: {
  "data": {
    "id": 1,
    "first_name": "João",
    "last_name": "das Neves",
    "age": 15,
    "origin": "As Crônicas de Gelo e Fogo"
  }
}

// Remove o Character de id com o valor {:id}
Rota: "DELETE /api/v1/characters/:id"
Modelo de cURL: `curl -X DELETE -H "Accept: application/json" {host}:{port}/api/v1/characters/{:id}`
```

## Configuração do Docker Compose

Convencionalmente, projetos que utilizam **Docker Compose** mantêm 3 arquivos
de configuração:

1. `docker-compose.test.yml` (ou `test.yml`): Configura a aplicação para seu ambiente de teste. Utilizada pelos _devs_ para testes isolados localmente ou em ferramentas de integração contínua que suportam **Docker Compose**;
1. `docker-compose.dev.yml` (ou `local.yml`): Configura a aplicação para seu ambiente de desenvolvimento. Utilizada apenas pelos _devs_ para uso do sistema localmente;
1. `docker-compose.prod.yml` (ou `production.yml`): Configura a aplicação para seu ambiente de produção.

Cada tipo de configuração pode exigir _containers_, variáveis de ambiente e
comandos diferentes. Portanto, é comum existir uma pasta `compose` na raíz do
projeto com as configurações de cada ambiente.

### Executando o Projeto Localmente

O arquivo de configuração
[`docker-compose.dev.yml`](https://gitlab.com/lappis-unb/internal/guides/examples/characters/blob/master/docker-compose.dev.yml)
define os serviços **api** e **db**, como pode ser visto a seguir:

```yaml
version: '3.3'

services:
  api:
    container_name: characters-api-dev
    build:
      context: .
      dockerfile: ./compose/dev/api/Dockerfile
    depends_on:
      - db
    env_file:
      - ./compose/dev/db.env
      - ./compose/dev/api.env
    ports:
      - 4000:4000
    volumes:
      - ./api:/code

  db:
    container_name: characters-db-dev
    env_file:
      - ./compose/dev/db.env
    image: postgres
    volumes:
      - ./postgres/dev/data:/var/lib/postgresql/data
```

O arquivo [`./compose/dev/api/Dockerfile`](https://gitlab.com/lappis-unb/internal/guides/examples/characters/blob/master/compose/dev/api/Dockerfile) define o _container_ do serviço **api**, como pode ser visto a seguir:

```docker
FROM elixir

RUN mix local.hex --force && \
    mix local.rebar --force && \
    mix archive.install --force \
    https://github.com/phoenixframework/archives/raw/master/phx_new.ez

COPY ./compose/dev/api/entrypoint.sh /entrypoint.sh
COPY ./compose/dev/api/start.sh /start.sh
COPY ./api /code

WORKDIR /code

EXPOSE 4000

ENTRYPOINT ["/entrypoint.sh"]

CMD ["/start.sh"]
```

E os respectivos _scripts_ [`entrypoint.sh`](https://gitlab.com/lappis-unb/internal/guides/examples/characters/blob/master/compose/dev/api/entrypoint.sh) e [`start.sh`](https://gitlab.com/lappis-unb/internal/guides/examples/characters/blob/master/compose/dev/api/start.sh):

```bash
#!/usr/bin/env bash

cmd="$@"

printf "\n## Mix Version\n\n"
mix -v
mix phx.new -v

printf "\n## Updating Dependencies\n\n"
mix deps.get
mix deps.compile

printf "\n## Creating Database\n\n"
mix ecto.create
mix ecto.migrate

exec $cmd
```

```bash
printf "\n## Initializing API\n\n"
mix phx.server
```

Por fim, os arquivos [`api.env`](https://gitlab.com/lappis-unb/internal/guides/examples/characters/blob/master/compose/dev/api.env) e [`db.env`](https://gitlab.com/lappis-unb/internal/guides/examples/characters/blob/master/compose/dev/db.env) contendo as variáveis de ambiente dos serviços:

```bash
MIX_ENV=dev
POSTGRES_HOST=db
```

```bash
POSTGRES_USER=characters_dev
POSTGRES_PASSWORD=characters_dev
```

A API ficará disponível na porta `4000` de seu `localhost` e os dados do
**PostgreSQL** ficarão armazenados em `./postgres/dev/data`.

Para iniciar os serviços da API em modo de desenvolvimento, execute:

```bash
docker-compose -f docker-compose.dev.yml up
```

Para acessar a **API**, utilize o _browser_ para as rotas `GET` ou qualquer
outro programa que possa definir e executar **REST**. Por exemplo:

```bash
curl -X GET -H "Accept: application/json" localhost:4000/api/v1/characters
```

Irá listar todos os _characters_ definidos. Como o banco de dados está vazio, a
**API** irá retornar o seguinte **json**:

```json
{
  "data": []
}
```

Para semear o banco com dados de exemplo, execute:

```bash
docker-compose -f docker-compose.dev.yml exec api mix run priv/repo/seeds.exs
```

Ao executar novamente o comando para listar os _characters_, a **API** irá
retornar o seguinte **json**:

```json
{
  "data": [{
    "origin": "A Song of Ice and Fire",
    "last_name": "Snow",
    "id": 1,
    "first_name": "Jon",
    "age": 14
  }, {
    "origin": "Breaking Bad",
    "last_name": "White",
    "id": 2,
    "first_name": "Walter",
    "age": 50
  }, {
    "origin": "Final Fantasy VI",
    "last_name": "Cole",
    "id": 3,
    "first_name": "Locke",
    "age": 25
  }, {
    "origin": "Warcraft III",
    "last_name": "Menethil",
    "id": 4,
    "first_name": "Arthas",
    "age": 24
  }, {
    "origin": "Inception",
    "last_name": "Cobb",
    "id": 5,
    "first_name": "Dominick",
    "age": 37
  }, {
    "origin": "Pulp Fiction",
    "last_name": "Vega",
    "id": 6,
    "first_name": "Vincent",
    "age": 27
  }]
}
```

Para desativar a aplicação e seus serviços, execute:

```bash
docker-compose -f docker-compose.dev.yml down
```

Para remover os volumes e as imagens locais geradas, execute o comando com as
seguintes flags adicionais:

```bash
docker-compose -f docker-compose.dev.yml down --rmi local -v
```

### Executando a Aplicação em Ambiente de Teste

O arquivo de configuração
[`docker-compose.test.yml`](https://gitlab.com/lappis-unb/internal/guides/examples/characters/blob/master/docker-compose.test.yml)
define os serviços **api** e **db** em ambiente de teste, como pode ser visto a
seguir:

```yaml
version: '3.3'

services:
  api:
    container_name: characters-api-test
    build:
      context: .
      dockerfile: ./compose/test/api/Dockerfile
    depends_on:
      - db
    env_file:
      - ./compose/test/db.env
      - ./compose/test/api.env
    volumes:
      - ./api:/code

  db:
    container_name: characters-db-test
    env_file:
      - ./compose/test/db.env
    image: postgres
    volumes:
      - ./postgres/test/data:/var/lib/postgresql/data
```

As diferenças entre o arquivo de teste e o de desenvolvimento são:

* Os nomes dos _containers_ estão sinalizadas como _test_;
* A referência do **Dockerfile** é o de teste;
* As variáveis de ambiente são as de teste;
* O diretório do **PostgreSQL** é o de teste.

O arquivo [`./compose/test/api/Dockerfile`](https://gitlab.com/lappis-unb/internal/guides/examples/characters/blob/master/compose/test/api/Dockerfile) define o _container_ do serviço **api**, como pode ser visto a seguir:

```docker
FROM elixir

RUN mix local.hex --force && \
    mix local.rebar --force && \
    mix archive.install --force \
    https://github.com/phoenixframework/archives/raw/master/phx_new.ez

COPY ./compose/test/api/entrypoint.sh /entrypoint.sh
COPY ./compose/test/api/test.sh /test.sh
COPY ./api /code

WORKDIR /code

EXPOSE 4000

ENTRYPOINT ["/entrypoint.sh"]

CMD ["/test.sh"]
```

As diferenças entre o **Dockerfile** de teste e o de desenvolvimento são:

* O caminho do _entrypoint_ é o de teste;
* O _script_ de execução é o de teste.

E os respectivos _scripts_ [`entrypoint.sh`](https://gitlab.com/lappis-unb/internal/guides/examples/characters/blob/master/compose/test/api/entrypoint.sh) e [`test.sh`](https://gitlab.com/lappis-unb/internal/guides/examples/characters/blob/master/compose/test/api/test.sh):

```bash
#!/usr/bin/env bash

cmd="$@"

printf "\n## Mix Version\n\n"
mix -v
mix phx.new -v

printf "\n## Updating Dependencies\n\n"
mix deps.get

exec $cmd
```

```bash
#!/usr/bin/env bash

printf "\n## Performing Tests\n\n"
mix test
```

As diferenças entre os _scripts_ de teste e o de desenvolvimento são:

* O _entrypoint_ não compila as dependências;
* O _entrypoint_ não cria o banco de dados e nem migra;
* O comando roda a suíte de testes ao invés de iniciar o servidor da **API**.

Por fim, os arquivos [`api.env`](https://gitlab.com/lappis-unb/internal/guides/examples/characters/blob/master/compose/test/api.env) e [`db.env`](https://gitlab.com/lappis-unb/internal/guides/examples/characters/blob/master/compose/test/db.env) contendo as variáveis de ambiente dos serviços:

```bash
MIX_ENV=test
POSTGRES_HOST=db
```

```bash
POSTGRES_USER=characters_test
POSTGRES_PASSWORD=characters_test
```

A API não ficará disponível na porta `4000` de seu `localhost`, pois o arquivo
de configuração não faz a configuração de portas. Para executar a aplicação em
ambiente de teste, utilize o seguinte comando:

```bash
docker-compose -f docker-compose.test.yml run --rm api
```

**Docker Compose** irá inicializar o serviço **api** e todos os serviços
associados à ele (no caso: **db**) e executará o comando padrão da imagem (`mix
test`). Os resultados dos testes devem ser:

```markdown
## Performing Tests

.................

Finished in 0.1 seconds
17 tests, 0 failures
```

Para remover os volumes e as imagens locais geradas, execute o comando:

```bash
docker-compose -f docker-compose.dev.yml down --rmi -v
```

## Configuração do GitLab CI/CD

O arquivo de configuração **GitLab CI/CD** ([`.gitlab-ci.yml`](https://gitlab.com/lappis-unb/internal/guides/examples/characters/blob/master/.gitlab-ci.yml)) do projeto é definido:

```yaml
image: docker
services:
  - docker:dind

stages:
  - test
  - update-registry

variables:
  STAGING_IMAGE: $CI_REGISTRY_IMAGE:staging
  LATEST_IMAGE: $CI_REGISTRY_IMAGE:latest

test:
  stage: test
  before_script:
    - apk add --no-cache py-pip
    - pip install docker-compose
  script:
    - docker-compose -f docker-compose.test.yml run --rm api

push staging image:
  stage: update-registry
  script:
    - docker login -u "gitlab-ci-token" -p "$CI_JOB_TOKEN" $CI_REGISTRY
    - docker build -f compose/dev/api/Dockerfile -t $STAGING_IMAGE .
    - docker push $STAGING_IMAGE
  only:
    - /develop/
  tags:
    - docker

push latest image:
  stage: update-registry
  script:
    - docker login -u "gitlab-ci-token" -p "$CI_JOB_TOKEN" $CI_REGISTRY
    - docker build -f compose/prod/api/Dockerfile -t $LATEST_IMAGE .
    - docker push $LATEST_IMAGE
  only:
    - /master/
  tags:
    - docker
```

O _job_ em destaque para este guia é o `test`.

Sua imagem `docker` é herdada da configuração raíz e o serviço `docker:dind`
(**dind** significa _docker in docker_) permite a utilização do CLI do
**Docker**.

A configuração definida em `before_script` adiciona
[pip](https://pypi.python.org/pypi/pip) e instala o **Docker Compose**.

A configuração definida em `script`, por fim, executa as configurações do
serviço `api` definida no arquivo `docker-compose.test.yml`.

As pipelines executadas no projeto podem ser vistas nos seguintes _links_:

* [Primeiro pipeline da _branch_ test](https://gitlab.com/lappis-unb/internal/guides/examples/characters/pipelines/18027322);
* [Segundo pipeline da _branch_ test](https://gitlab.com/lappis-unb/internal/guides/examples/characters/pipelines/18027402);
* [Pipeline da _branch_ develop](https://gitlab.com/lappis-unb/internal/guides/examples/characters/pipelines/18027406);
* [Pipeline da _branch_ master](https://gitlab.com/lappis-unb/internal/guides/examples/characters/pipelines/18027409).

<!-- }}} -->

# Anexo II - Estudo sobre ferramenta de chatbots <!-- {{{ -->

## Introdução

A fim de identificar as ferramentas mais adequadas ao contexto do MINC, foram
analisadas as seguintes ferramentas:

* Botpress
* RASA
* IBM Bluemix

Levando em conta os seguintes critérios:

* Vantagens e Limitações
* Licença
* Analytics (indicadores e dados coletados sobre as interações com o bot)

## Botpress

![botpress](https://raw.githubusercontent.com/botpress/botpress/HEAD/assets/shot_01.png)

### Vantagens
* Permite que o bot faça perguntas ao usuário
* Permite que sejam enviadas opções para que o usuário selecione
* Possui ferramenta de análise
* Possibilita integração externa

### Limitações
* Não há NLP (Natural Language Processing) nativo, entretanto é fácil a integração com módulos com NLP, como RASA, API.AI (Dialogflow), WIT.AI, entre outros.
* Apesar de possibilitar integração externa, é necessária a criação de um conector. Há conectores tanto oficiais, quanto criados pela comunidade. Já existe um conector para páginas web criado pela comunidade, porém em versão alpha, ainda não contemplando o envio de imagens, vídeos, áudios e etc.

### Licença
O bot utiliza duas licenças: [AGPLv3](https://github.com/botpress/botpress/blob/master/licenses/LICENSE_AGPL3) e a [Botpress Proprietary License](https://github.com/botpress/botpress/blob/master/licenses/LICENSE_BOTPRESS).

A Botpress Proprietary License permite que os módulos sejam usados apenas para a construção de chatbots, não podendo ser utilizados para construção de outras plataformas comerciais, como uma própria plataforma de desenvolvimento de chatbots, sem permissão prévia da Botpress.

O core e os módulos utilizados em um projeto devem utilizar a mesma licensa.

Para mais detalhes, acesse o [FAQ](https://botpress.io/faq).

### Analytics
O botpress oferece uma dashborad onde é possível visualizar as seguintes informações:

* Número total de usuários por plataforma
* Uso por gênero
* Quantidade de usuários ativos nas últimas duas semanas
* Média de interações que os usuários têm com o bot em um dia
* Retenção por dia
* Horas em que o bot esteve ocupado para os últimos sete dias

### Exemplos

#### Integração com páginas web

Para integração do bot com páginas web é necessária a instalação do módulo botpress-web através do seguinte comando:

```
npm install botpress-web@next
```

Inclua o código abaixo dentro da tag `<body>` da página a qual você quer integrar o chat:

```javascript
<script>
    window.botpressSettings = {
        hostname: "localhost:3000" // <<-- Mude para o hostname do seu bot
    };
</script>
<script>
    !function() {
        function t() {
	    var t = n.createElement("script");
	    t.type="text/javascript", t.async=!0,t.src="http://"+a.hostname+"/api/botpress-web/inject.js";
	    var e = n.getElementsByTagName("script")[0];
	    e.parentNode.insertBefore(t,e)
        }

	var e = window, a = e.botpressSettings,n = document;
	e.attachEvent ? e.attachEvent("onload",t): e.addEventListener("load",t,!1)
    }();
</script>
```
Se a URL do host não for https, dentro do diretório do seu projeto, vá até o diretório **node_modules/botpress-web/bin** e no arquivo **node.bundle.js** troque a URL da definição do host para http.

Reinicie a aplicação do bot e a janela de chat deverá aparecer na página web.

#### Integração com wit.ai

Para adicionar NLP ao bot é necessária a integração com algum módulo que forneça essas funcionalidades. A seguir será mostrado um exemplo de integração com o WIT.AI.

Primeiramente é necessária a instalação do módulo através do seguinte módulo:

```
botpress install wit
```

Crie uma aplicação no WIT.AI e cadastre os contextos com suas respectivas questões, conforme este [este tutorial](https://wit.ai/docs/quickstart).

Copie o **Service Access Token** na aba **Settings** do WIT.AI e cole no campo **Access Token** da opção Wit.ai no Botpress, marcando a opção Understanding.

[[images/witi-set.png]]

Neste exemplo, no arquivo content.yml foram configuradas as respostas para cada contexto definido no WIT.AI:

```yaml
projetos:
  - typing: true
    text: |
      Para a Pessoa Física e para o Empresário Individual – EI com enquadramento em Microempresário Individual – MEI o valor máximo é de R$ 700.000,00 (setecentos mil reais).
      Para os demais enquadramentos de Empresário Individual – EI o valor máximo é de R$ 5.000.000,00 (cinco milhões de reais).
      Para a Empresa Individual de Responsabilidade Limitada – EIRELI, Sociedades Limitadas – Ltda. e demais Pessoas Jurídicas o valor máximo é de R$ 10.000.000,00 (dez milhões de reais). Referência inciso II e suas alíneas, da IN 01/17.

ingressos:
  - typing: true
    text: |
      A comercialização dos ingressos ou outros produtos culturais resultantes do projeto não possui teto de valor unitário, observando que esses valores estarão sempre sujeitos à aprovação do MinC com vistas a assegurar a democratização.
      O preço médio do produto cultural a ser vendido a critério do proponente referente à cota de 50% da tiragem total de produtos é que deve ser no máximo de três vezes o valor mensal do Vale-Cultura, o que hoje representa R$ 150,00.
      Rege a matéria o art. 53 da IN 01/17, em especial a alínea “e“ do inciso I e os §s 4º e 5º.
```

E por fim, foi feita a configuração para que quando o WIT.AI retornar que a frase feita pelo usuário representa um contexto, o bot identifique e retorne as respostas definidas para o contexto retornado:

```javascript
module.exports = function(bp) {

  bp.hear({'wit.entities.intent[0].value': 'ingressos'}, (event, next) => {
    event.reply('#ingressos')
  })

  bp.hear({'wit.entities.intent[0].value': 'projetos'}, (event, next) => {
    event.reply('#projetos')
  })
}
```

Teste o bot:

[[images/bot.png]]

Há ainda módulos prontos para a integração com outras ferramentas, além do [Botpress NLU](https://github.com/botpress/botpress-nlu) que permite a integração com o RASA ou LUIS de forma que possam ser configurados pela própria interface do Botpress:

## IBM Watson Conversation

O [watson conversation](https://watson-conversation.ng.bluemix.net)
é a solução da IBM para chatbots. Há um
[curso online](https://cognitiveclass.ai/courses/how-to-build-a-chatbot/)
que dá uma breve introdução sobre os chatbots e o IBM watson

O fluxo de trabalho no Watson é:

1. Criar as `intents`: que são intenções que o usuário possui. Cada intenção é
formada por um conjunto de perguntas / frases, no mínimo 5, e um título identificador da
intenção. Nesta etapa é bom prever muitas variações das perguntas e possíveis erros
gramaticais que o usuário pode cometer para melhorar a acuracia do treinamento;
1. Criar as `entities`: repsentam partes elementares de uma mensagem, por exemplo,
um local, uma data ou um tipo de relação pessoal. Cada entidade possui um texto que
representa ela, e vários sinônimos;
1. Criar o diálogo: O diálogo é um fluxo de conversa com os passos em que ocorre um
fluxo natural de conversa real. Ele é descrito como uma sequencia de estatos, e
cada estado possui: intent ou ação, uma série de respostas para mostrar pro usuário,
uma ação que deve ser tomada ao fim daquele estado. A ação do fim pode ser pular para
um estado específico, pedir input para o o usuário, entre outras. Cada estado pode
ter sub-estados.

### Vantagens

* Tem integração por padrão com o Slack e o Facebook Messenger
* É possível integrar com outras aplicações
* Inteface simples e agradável
* Suporte a analytics, com poucas métricas

### Limitações

* Reconhecimento semi-automatico de entidades. Você precisa pré-cadastrar as opções
* Código fechado e precificação por uso

### Licença

Copyright - código fechado da IBM.

O Pricing é baseado no número de conversas feitas por mês.

### Analytics

O IBM Watson extrai as seginte métricas:

- Gráfico de número de chats por hora
- Número total de chats
- Número de mensagens sem classificação (não identificou intenção ou entidade)
- Top 3 intenções e entidades

## Rasa NLU e Rasa Core

### Rasa NLU

O [Rasa NLU](https://nlu.rasa.ai/) é uma ferramenta open source para processamento de linguagem natural, sendo focada em classificação de intenções e extração de identidades.
Rasa é um conjunto de API's para construção de um parser que utiliza as bibliotecas de NLP e ML existentes. Sendo que, este pode ser utilizado como uma alternativa à ferramentas como: `wit`,`LUIS`,`Dialog Flow`, e etc.

Segundo o estudo [Evaluating Natural Language Understanding Services for Conversational Question Answering Systems](http://www.sigdial.org/workshops/conference18/proceedings/pdf/SIGDIAL22.pdf), é possível perceber que o Rasa possui um desempenho muito bom comparado às principais ferramentas comerciais de processamento de linguagem natural, tanto em relação à desempenho quanto à acurácia da extração de entidades e intenções.

### Utilizando o Rasa NLU

Para utilizar o Rasa basta instalar o pacote do Rasa NLU, escolher o modelo de backend que melhor se aplica ao contexto em questão, e seguir o [tutorial de instalação](https://nlu.rasa.ai/installation.html). Como o Rasa utiliza bibliotecas python de ML para processamento, tanto o rasa_nlu quanto o backend podem ser instalados utilizando o `pip`.

Os dados para treinamento do Rasa NLU seguem um padrão que consiste na entrada de texto a ser processada, definição da intenção correspondente àquela entrada e das entidades presentes. Os arquivos de treinamento ficam no diretório `data`.

Para selecionar o pipeline de backend a ser utilizado, para isso o Rasa NLU utiliza um arquivo `JSON` que define o pipeline a ser utilizado, o diretório onde estão os arquivos para treinamento, onde devem ser criados os modelos gerados a partir do treinamento e outros metadados. Todas as possíveis configurações que podem ser utilizadas no arquivo de configuração podem ser encontradas na [documentação oficial](https://nlu.rasa.ai/config.html#section-configuration). Se o pipeline sendo utilizado for o do `SPACY + SKLEARN` por exemplo, pode-se criar um arquivo chamado `config_spacy.json`.

Depois de especificar o arquivo de configuração bastará rodar a linha de comando para treinar os modelos, e em seguida subir o server do rasa. A partir daí já será possível processar textos e o Rasa NLU devolverá um `JSON` com a classificação da intenção e as entidades identificadas.
Para um melhor entendimento da execução desses passos, basta seguir as instruções de construção de um [bot básico](https://nlu.rasa.ai/tutorial.html).

### Rasa Core

O [RASA Core](https://core.rasa.ai/) é uma ferramenta livre para construção de sistemas de conversação, como Messengers e Chat Bots.

### Utilizando o Rasa Core

Para utilização do Rasa Core, além das dependências instaladas para utilização do Rasa NLU, é necessário instalar apenas o seu pacote, seguindo a [documentação](https://core.rasa.ai/installation.html).

É preciso ter um arquivo `domain.yml` que define o universo de atuação do bot. Dentro desse arquivo são especificadas as intenções e ações a serem utilizadas durante a execução do bot.

Dentro do diretório `data` deve existir um arquivo `nlu.md` que define os textos relacionados à cada intenção. E um arquivo `stories.md` que descreve os contextos de conversação esperados a partir das intenções.

Na pasta raiz do projeto é necessário um arquivo de configuração como o utilizado no Rasa NLU, que defina as configurações da pipeline a ser utilizada.

Por último, é necessário executar os comandos para treinar o Rasa NLU e o Rasa Core. São nesses passos onde serão gerados os modelos e os arquivos de treinamento que o bot consumirá. E então, executar o comando para subir o server do Rasa Core.
Para mais informações a respeito da execução destes passos, basta seguir os passos para [construção de um bot básico usando o Rasa Core](https://core.rasa.ai/tutorial_basics.html).

### Vantagens
  * Livre e grátis;
  * Todos os serviços citados acima não informações relevantes à respeito das tecnologias usadas(algoritmos de ML e datasets), diferentemente do RASA, que é mais flexível e te permite facilmente escolher às ferramentas a serem utilizadas no módulo de backend;
  * O Rasa apresenta performance similar ou superior aos serviços acima citados;
  * Possui funcionalidade de importar dados em lote;

### Limitações
  * Uma das desvantagens em relação aos serviços NLU que são baseados em nuvem é que o Rasa não é tão facilmente escalável;
  * O Rasa possui uma pequena base para treinamento inicial. Por exemplo, para o backend usando o MITIE, o Rasa vem com um modelo de linguagem inicial de aproximadamente 300 MB. Enquanto que as outras ferramentas, por serem comerciais, são alimentadas com grandes entradas de dados;

### Licença

Tanto o Rasa NLU como o Rasa Core utilizam a licença permissiva **Apache License 2.0** - [Rasa NLU license](https://github.com/RasaHQ/rasa_nlu/blob/master/LICENSE.txt)/[Rasa Core license](https://github.com/RasaHQ/rasa_core/blob/master/LICENSE.txt).

### Analytics

Ambas as bibliotecas, Rasa core e Rasa NLU, não oferecem nativamente suporte à extração e análise de métricas.

## Integração dos serviços: BotPress + Rasa NLU + Spacy

### Utilização do BotPress

É preciso instalar o pacote do BotPress através do npm.
```bash
  npm install -g botpress
```

Para iniciar um projeto com o BotPress é preciso utilizar o comando abaixo indicando o nome do seu projeto.

```bash
  botpress init my-bot
```

Por último basta iniciar o serviço do BotPress.

```bash
  botpress start
```

Após a execução dos passos anteriores, o BotPress estará rodando por padrão na porta 5000.

Para o BotPress se comunicar com o rasa é preciso instalar o Middleware do rasa, utilizando o comando abaixo.

```bash
  botpress install rasa
```
Em seguida, na aba `Rasa NLU` no dashboard à esquerda é necessário configurar o endereço do host onde o seu Rasa NLU está rodando no campo `Rasa Address`. Se o servidor do Rasa estiver rodando no mesmo host basta apontar para a respectiva porta, que por padrão é a porta 5000.
Também é preciso definir no campo `Project Name` o nome da pasta de projeto onde estão os modelos do rasa, que por padrão é a pasta `default`.

Se o servidor do Rasa NLU estiver rodando corretamente o Botpress já estará conectado corretamente e para utilizar o Rasa como backend basta configurar uma resposta que utilize o Middleware do Rasa no arquivo `index.js`. Como no exemplo abaixo, em que sempre que o Rasa NLU indentificar a intenção `greet` o Botpress usará uma das respostas definidas na tag 'greet_response', dentro do arquivo 'content.yml'.

```javascript
bp.hear({'rasa_nlu.intent.name': 'greet'}, (event) => {
  event.reply('#greet_response')
})
```
### Utilização do Rasa NLU

É possível instalar o Rasa NLU diretamente pelo pip. No contexto desenvolvimento é mais interessante clonar o [repositório do Rasa](https://github.com/RasaHQ/rasa_nlu) uma vez que provavelmente vários arquivos serão modificados.

Uma vez configurados os arquivos de acordo com o contexto em questão, é necessário executar o comando abaixo para treinar os modelos com o backend em questão.

```bash
python -m rasa_nlu.train -c sample_configs/config_spacy.json
```
E então basta subir o servidor do Rasa.

```bash
python -m rasa_nlu.server -c sample_configs/config_spacy.json
```

### Utilizando Botpress web

O [Botpress web](https://github.com/botpress/modules/tree/master/packages/botpress-channel-web) permite a utilização do chat de duas formas, com um iframe que pode ser utilizado embutido em qualquer página, ou como um web-app na tela inteira.
Para utilizar o Botpress web é necessário instalar o pacote via botpress ou npm:
```bash
botpress install botpress-platform-webchat
```
Uma vez instalado o Middleware web, é possível ver se este está ativado na aba Middleware no menu principal do Botpress, à esquerda no dashboard.  

Para utilizar a `view mobile` basta acessar o link a seguir a partir do seu hostname:
 ${HOSTNAME}/lite/?m=platform-webchat&v=fullscreen (e.g http://localhost:3000/lite/?m=platform-webchat&v=fullscreen

Para embutir o chat em uma página qualquer basta adicionar o código abaixo ao final da tag `<body>` em qualquer arquivo html.

```html
<script src="<host>/api/botpress-platform-webchat/inject.js"></script>
<script>window.botpressWebChat.init({ host: '<host>' })</script>
```

## Integração dos serviços: Rasa NLU + Rasa Core

Para a instalação do Rasa Core através do [pip](https://pip.pypa.io/en/stable/installing/), utilize o comando abaixo:

```bash
  pip install rasa_core
```

Para a instalação do Rasa NLU, utilize o comando abaixo ou instale através do repositório conforme descrito no tópico anterior (Integração dos serviços: BotPress + Rasa NLU + Spacy).

```bash
  pip install rasa_nlu
```
É possível utilizar o sklearn, spaCy e MITIE como backend para o Rasa NLU. Para utilização do spaCy, execute os seguintes comandos:

```bash
pip install rasa_nlu[spacy]
python -m spacy download en_core_web_md
python -m spacy link en_core_web_md en
```

O tutorial do [Rasa Core](https://core.rasa.ai/tutorial_basics.html) descreve um passo a passo para a criação de um bot simples utilizando estas tecnologias.

<!-- }}} -->

# Anexo III - Planejamento Estratétigo <!-- {{{ -->

Planejamento referente à Etapa II do projeto (Março 2018 à Junho 2018)

## Metas Estratégicas

* Transformar softwares culturais abrindo-os para práticas colaborativas e abertas ([meta estratégica 1](https://github.com/lappis-unb/EcossistemasSWLivre/wiki/Metas#meta-1-transforma%C3%A7%C3%A3o-de-software-legado-em-comunidades-de-software-aberto))
* Estruturar a equipe e definir os primeiros passos da frente Governança ([meta estratégica 3](https://github.com/lappis-unb/EcossistemasSWLivre/wiki/Metas#meta-3-estudos-sobre-pr%C3%A1ticas-de-gest%C3%A3o-colaborativa-em-comunidades-de-software-aberto))
* Refatorar e re-escrever chatbot usando tecnologias mais "inteligentes", iniciando a modelagem de um produto lappis de assistentes virtuais para serviços públicos ([meta estratégica 4](https://github.com/lappis-unb/EcossistemasSWLivre/wiki/Metas#meta-4-aprendizado-de-m%C3%A1quina-para-apoiar-a-fiscaliza%C3%A7%C3%A3o-da-lei-rouanet))
* Coleta de dados para estudo sobre melhoria das práticas de gestão e desenvolvimento de software livre ([meta estratégica 3](https://github.com/lappis-unb/EcossistemasSWLivre/wiki/Metas#meta-3-estudos-sobre-pr%C3%A1ticas-de-gest%C3%A3o-colaborativa-em-comunidades-de-software-aberto))
* Primeitos passos para estudos sobre processos técnicos e gerenciais para aferição e aceitação de produtos de software ([meta estratégica 6](https://github.com/lappis-unb/EcossistemasSWLivre/wiki/Metas#meta-6-estudos-dos-processos-t%C3%A9cnicos-e-gerenciais-minc-para-aferi%C3%A7%C3%A3o-e-aceita%C3%A7%C3%A3o-de-produtos-de-software))

## Épicas

### Governança
* Sistematizar colaboração entre os atores internos e externos ao minc
* Realizar e fomentar colaboração em software livre nos projetos do minc

### Chatbot
* Chat em produção com respostas sobre a lei e sobre o sistema salic
* Evolução do bot com tecnologias mais inteligentes para refinamento de contexto

### Plataforma
* Modelo de processo multidisciplinar da equipe
* Protótipos da solução VerSalic

### Salic-ML
* Sistematizar modelo de processo e trabalho com machine learning
* Desenhar arquitetura da solução ML

### Pesquisa/Paulo
* Análise qualitativa da execução do modelo e fluxo de colaboração entre lappis/minc
* Revisão sistemática sobre devops e mapa conceitual

<!-- }}} -->

# Anexo IV - Resultados Pesquisa Devops Pesquisa Survey de Acompanhamento

Abaixo segue o resultado da análise do survey realizado com os alunos participantes do projeto.

O formulário enviado para os alunos pode ser acessado em:

[https://docs.google.com/forms/d/1SpZMX8qYLZGl7q6nTO4JPpI4eFbMHAJHP5NivG-jMhw/prefill](https://docs.google.com/forms/d/1SpZMX8qYLZGl7q6nTO4JPpI4eFbMHAJHP5NivG-jMhw/prefill)
