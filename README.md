# Especialização em Ciência de Dados
# Projeto Interdisciplinar - IFSP


## Professores:

Profa. Dra Bianca Pedrosa - bpedrosa@ifsp.edu.br

Prof. Dr Samuel Martins (Samuka) - @hisamuka


## Alunos:

Caio de Lima

Carlos Caetano de Almeida


# Introdução


Este trabalho é um projeto interdisciplinar do curso de Especialização em Ciência de Dados do Instituto Federal de São Paulo, englobando os conceitos estudados na disciplina de Tecnologias de Big Data e na disciplina de Aprendizagem de Máquina e Reconhecimento de Padrões. 

Educação foi o tema escolhido para o projeto, dada a sua importância e relevância, principalmente nos dias de hoje, sendo um direito fundamental garantido na Declaração Universal dos Direitos Humanos, contudo, garantir esse direito é em si um grande desafio e o Brasil se comprometeu em ir além, em um acordo com a UNESCO o país visa garantir uma educação inclusiva, equitativa e de qualidade. 

Apesar desse compromisso, os números da educação pública são preocupantes, de acordo com os dados mais recentes do [QEdu (2019)](https://qedu.org.br/brasil/aprendizado), somente 36\% dos alunos de português na nona série estão em um nível adequado de proficiência, essa situação se mostra ainda pior em matemática, onde somente 18\% dos alunos estão em um nível adequado. Devido aos preocupantes números e o compromisso firmado é necessário dedicar esforços para melhorar a educação, e para melhorar esse cenário podemos utilizar a tecnologia como ferramenta para auxiliar os profissionais da educação.

# Objetivo

O objetivo do trabalho é predizer possíveis reprovações dos alunos, tomando como base os resultados escolares obtidos na base de dados, aplicando modelos de aprendizagem de máquina e métricas como accuracy e recall para realizar o fine tuning dos modelos testados em ambientes distribuídos como Azure e AWS.


# Dados

Os dados selecionados para este trabalho são provenientes de um estudo realizado em Portugal. São dois conjuntos de dados referentes às disciplinas de matemática e português de duas escolas de ensino médio da região de Alentejo em Portugal, eles foram coletados entre 2005 e 2006 e são compostos por informações provindas dos relatórios escolares (i.e notas e quantidade de faltas) e dados de questionários com opções pré definidas, ao fim os conjuntos de dados contam com informações demográficas, sociais, referentes ao ambiente escolar e as notas dos estudantes. São 33 atributos modelados sob uma lógica binária e de 5 níveis de importância justamente para facilitar tarefas de Machine Learning como predição e classificação. Para este estudo foi selecionado o conjunto de dados referente à disciplina de Português que conta com dados de 649 estudantes. É importante salientar que os dados foram coletados há mais de 10 anos, uma diferença temporal significativa, além disso a pandemia de COVID-19 impactou, e continuará a impactar, a educação no mundo todo, para mais existem diferenças culturais, sociais e econômicas relevantes entre o Brasil e Portugal, dificultando a transferência de um modelo baseado nesses dados para a realidade brasileira pós COVID-19.
Os dados são tabulares e não seguem nenhum fenômeno temporal, cada linha da tabela corresponde a um estudante e todos os valores são numéricos, textuais ou binários, os valores binários também são textuais, mas são sempre referentes a duas categorias. Podemos agrupar os atributos da seguinte forma:

É importante reforçar que os dados disponíveis referentes a estudantes do ensino fundamental são escassos, e por isso os dados obtidos para esse estudo são referentes a Portugal, esse fator pode gerar um modelo não tão apropriado para a realidade brasileira. Além do fator regional o fator temporal pode ter impacto negativo na nossa pesquisa, os dados obtidos são referentes a 2008, de acordo com [Gupta e Jawanda (2020)](https://www.researchgate.net/profile/Sonia-Gupta-10/publication/342931049_The_impacts_of_COVID-19_on_children/links/5f682cb2a6fdcc008631d487/The-impacts-of-COVID-19-on-children.pdf) a pandemia de COVID-19 vai produzir impactos a longo prazo, apesar de algumas dessas mudanças serem positivas elas acreditam que os impactos negativos podem ser devastadores e que podem afetar milhões de crianças ao redor do mundo.

## Transformações nos dados

Como citado anteriormente a coleta e modelagem de dados foi pensada para tarefas de Machine Learning, então houve poucas alterações nos dados, as principais mudanças foram nos valores binários e de texto, que são qualitativos nominais. Os dados binários foram convertidos para valores binários "reais", 0 ou 1, e para os dados qualitativos nominais foram criadas variáveis auxiliares, i.e dummies variables, com valores de 0 ou 1 novamente, dessa maneira todos os dados presentes na base se tornaram numéricos. Além disso, se optou por não utilizar as colunas G1 e G2 para classificar se o aluno será aprovado ou não, pelo fato de existir uma correlação muito forte entre estas colunas e a aprovação do aluno. Por fim, se considerou que caso G3 seja maior ou igual 10 o aluno está aprovado.

## Dicionário de dados
|    | ATRIBUTO   | DESCRIÇÃO                         | VALORES                                                                                                           |
|----|------------|-----------------------------------|-------------------------------------------------------------------------------------------------------------------|
| 1  | school     | Qual escola o aluno pertence      | Gabriel pereira ou  Mousinho da Silveira                                                                          |
| 2  | sex        | Sexo do estudante                 | Feminino ou  Masculino                                                                                            |
| 3  | age        | Idade do estudante                | De 15 até 22 anos                                                                                                 |
| 4  | address    | Tipo de moradia do estudante      | Urbano ou Rural                                                                                                   |
| 5  | famsize    | Tamanho da família                | Menor ou igual a 3 ou Maior que 3                                                                                 |
| 6  | Pstatus    | Status dos pais                   | Morando Juntos ou Separados                                                                                       |
| 7  | Medu       | Nível de educação da mãe          | - Nenhum - Educação Primária completa (4ª série) - 5ª série a 9ª - Educação Secundária completa - Ensino Superior |
| 8  | Fedu       | Nível de educação do pai          | - Nenhum - Educação Primária completa (4ª série) - 5ª série a 9ª - Educação Secundária completa - Ensino Superior |
| 9  | Mjob       | Trabalho da mãe                   | - Professor(a) - Área da saúde - Funcionário público - Do lar - Outros                                            |
| 10 | Fedu       | Nível de educação do pai          | - Professor(a) - Área da saúde - Funcionário público - Do lar - Outros                                            |
| 11 | reason     | Razão para escolher esta escola   | - Próximo da casa - Reputação - Preferência de curso - Outro                                                      |
| 12 | guardian   | Responsável pelo estudante        | - Mãe - Pai- Outro                                                                                                |
| 13 | traveltime | Tempo de viagem até a escola      | - Menos que 15 minutos - De 15 a 30 minutos - De 30 minutos a 1 hora - Mais que 1 hora                            |
| 14 | studytime  | Tempo de estudo semanal           | - Menos que 2 horas - De 2 a 5 horas - De 5 a 10 horas - Mais que 10 horas                                        |
| 15 | failures   | Número de reprovações             | - 1 reprovação - 2 reprovações - Mais de duas reprovações                                                         |
| 16 | schoolsup  | Suporte extra para educação       | Sim ou Não                                                                                                        |
| 17 | famsup     | Suporte educacional familiar      | Sim ou Não                                                                                                        |
| 18 | paid       | Aulas extras para a matéria       | Sim ou Não                                                                                                        |
| 19 | activities | Atividades extra curriculares     | Sim ou Não                                                                                                        |
| 20 | nursery    | Já foi até a enfermaria da escola | Sim ou Não                                                                                                        |
| 21 | higher     | Deseja cursar ensino superior     | Sim ou Não                                                                                                        |
| 22 | internet   | Possui acesso a internet em casa  | Sim ou Não                                                                                                        |
| 23 | romantic   | Está em um relacionamento         | Sim ou Não                                                                                                        |
| 24 | famrel     | Qualidade da relação familiar     | De 1 até 5, sendo 1 muito ruim e 5 excelente                                                                      |
| 25 | freetime   | Tempo livre pós escola            | De 1 até 5, sendo 1 baixíssimo e 5 altíssimo                                                                      |
| 26 | goout      | Frequência que sai com amigos     | De 1 até 5, sendo 1 baixíssima e 5 altíssima                                                                      |
| 27 | Dacl       | Consumo de álcool diário          | De 1 até 5, sendo 1 baixíssimo e 5 altíssimo                                                                      |
| 28 | Walc       | Consumo de álcool semanal         | De 1 até 5, sendo 1 baixíssimo e 5 altíssimo                                                                      |
| 29 | health     | Estado atual de saúde             | De 1 até 5, sendo 1 muito ruim e 5 excelente                                                                      |
| 30 | absences   | Número de faltas escolares        | De 0 até 93                                                                                                       |
| 31 | G1         | Nota do primeiro período          | De 0 até 20                                                                                                       |
| 32 | G2         | Nota do segundo período           | De 0 até 20                                                                                                       |
| 33 | G3         | Nota final                        | De 0 até 20                                                                                                       |


# Arquitetura

O Diagrama da Arquitetura consiste na inserção da base de dados na nuvem, efetuando sua limpeza e tratamento dos dados, divisão da base de dados entre treino e teste, selecionando o modelo de regressão de aprendizado de máquina com a análise dos resultados da predição

 
 ![image](https://user-images.githubusercontent.com/41349325/206814391-541bff99-6186-4111-a41d-9b234737e555.png)




# Infraestrutura

A infraestrutura foi criada na região Brazil South e envolveu os seguintes recursos:

    •	Máquina Virtual Dedicada

    •	CPU

    •	2 Núcleos

    •	14GB de RAM

    •	28GB de Armazenamento


A seleção da infraestrutura pode ser vista na imagem abaixo:

![image](https://user-images.githubusercontent.com/41349325/206780267-25041d36-0f49-4652-8f65-3c198fd44a05.png)



# Setup

Para implementar o pipeline, foram utilizados os recursos do Azure, considerando o menor custo de utilização desses recursos, sendo instanciada a máquina virtual de menor valor, que equivale a 24 centavos de dólar por hora de utilização, dois núcleos dentre seis núcleos disponíveis, a configuração do Setup pode ser visto na imagem abaixo:


![image](https://user-images.githubusercontent.com/41349325/206780646-7c9aeb41-c795-4110-9714-be81504f4a1a.png)



# Pipeline/Metodologia

O Pipeline/metodologia no desenvolvimento do projeto, teve como base os seguintes procedimentos:

           •	Enquadramento do problema

           •	Obter dados

           •	Limpeza de dados

           •	Explorar os dados

           •	Preparar os Dados (Pré-processamento)

           •	Melhor modelo de treinamento (trabalho de treinamento, criação de modelo)

           •	Implantar no endpoint

           •	Dados de teste

           •	Modelo

           •	Predição

           •	Avaliação dos resultados
           
           
 ![image](https://user-images.githubusercontent.com/41349325/206810550-b3b700f1-50b2-41ca-b89a-def75fa01b92.png)



Os pipelines do Azure Machine Learning organizam várias etapas do aprendizado de máquina e do processamento de dados em um só recurso. Os pipelines permitem organizar, gerenciar e reutilizar fluxos de trabalho complexos de aprendizado de máquina entre projetos e usuários. O pipeline do projeto pode ser conferido nas imagens abaixo:



![image](https://user-images.githubusercontent.com/41349325/206780791-ab24d4fb-a0d0-4a94-b7b5-300fc5590831.png)


![image](https://user-images.githubusercontent.com/41349325/206781215-93c6f1f9-5c14-49ba-ad83-db5ad66ee5d8.png)



# CleanUp

Os recursos alocados no setup e na criação do endpoint têm que ser removidos ao final do projeto, caso contrário esses recursos são contabilizados desnecessariamente, devido a isso é muito importante a exclusão dos recursos utilizados e não mais necessários. Essa exclusão dos recursos foi feita, conforme imagens abaixo:


![image](https://user-images.githubusercontent.com/41349325/206781581-1849c2ea-b876-467e-9d1f-67397dd44f8f.png)


![image](https://user-images.githubusercontent.com/41349325/206781641-094adbb4-e732-4a13-8fdf-77e52f414acf.png)


![image](https://user-images.githubusercontent.com/41349325/206781705-98ec94d3-144e-4753-9700-79affedecc99.png)



# Resultados e conclusões


Dentre os modelos testados, o SVM apresentou melhor resultado, com predição com 95% de acurácia. As máquinas de vetores suporte (SVM), também conhecidas como
modelos de máxima margem, tem baixa complexidade, sua fronteira de decisão se assemelha a uma rodovia(hiperplano). Como o nome sugere, este modelo elege vetores suportes que nos ajudam a definir a qual classe cada elemento pertence.


Como melhorias deste trabalho, pretende-se desenvolver novos modelos de aprendizado de máquina, implementando processamento de linguagem natural e redes neurais convolucionais na melhoria da predição.

![image](https://user-images.githubusercontent.com/41349325/206805064-7ad358ca-96b4-4390-be25-7fddc4ea9ef2.png)



![image](https://user-images.githubusercontent.com/41349325/206805119-0225507e-35ff-4446-ada6-f67e74964fb1.png)



# Referências


Acesso seguro aos dados na nuvem v1 - Azure Machine Learning. https://learn.microsoft.com/pt-br/azure/machine-learning/v1/concept-data?source=recommendations


Configurar o AutoML com Python - Azure Machine Learning. https://learn.microsoft.com/pt-br/azure/machine-learning/v1/how-to-configure-auto-train-v1?source=recommendations



Entrada/saída do serviço Web: referência de componente - Azure Machine Learning. https://learn.microsoft.com/pt-br/azure/machine-learning/component-reference/web-service-input-output?source=recommendations


Hands-on machine learning with Scikit-Learn, Keras, and TensorFlow”, A. Géron (2019).


Machine Learning Project Checklist. @xavecoding. youtube.com/c/xavecoding


Treinar e implantar um exemplo no Jupyter Notebook - Azure Machine Learning. https://learn.microsoft.com/pt-br/azure/machine-learning/v1/tutorial-train-deploy-notebook?source=recommendations



Use o Azure Machine Learning para treinar e implantar um modelo de classificação de imagem com o Scikit-learn em um Jupyter Notebook do Python baseado em nuvem.https://learn.microsoft.com/pt-br/azure/machine-learning/v1/tutorial-train-deploy-notebook?source=recommendations


