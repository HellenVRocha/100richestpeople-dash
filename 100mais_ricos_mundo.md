## *Trabalho realizado para conclusão do curso de **Data Analytics** pela CoderHouse em Novembro/2022*
---

### **1.INTRODUÇÃO**

Segundo a edição 2022 da Forbes (revista estadunidense de negócios e economia) foram encontrados mais de 1.000 bilionários mais ricos do que eram há um ano atrás. A Forbes utilizou os preços das ações e as taxas de câmbio de 11 de março de 2022 para calcular os patrimônios líquidos dos dados apresentados. Neste trabalho serão analisadas somente as 100 pessoas mais ricas em 2022.

#### **1.1 Objetivo**
Este trabalho tem por objetivo explorar e responder às seguintes questões:
* A soma do patrimônio líquido das 100 pessoas;
* A média de idade entre eles;
* Quantidade de bilionários por gênero;
* Qual o país que mais e menos possui bilionários, separados por gênero; 
* Quantidade distinta de empresas e seguimentos;
* Qual o seguimento que os bilionários mais e o que menos estão envolvidos.

### **2.ENTENDENDO A BASE DE DADOS**

#### **2.1 Entidade Relacionamento**

![entidade-relacionamento](https://user-images.githubusercontent.com/112497138/193289706-f4dd7955-e745-464b-a708-473b5084ee36.jpeg)

#### **2.2 Tabelas**
![tabela](https://user-images.githubusercontent.com/112497138/193289916-e6d1497c-12ba-44bd-aeb3-e1f78c3f6687.jpeg)

### **3.BASE DE DADOS NO SQL SERVER**

A base de dados escolhida foi baixada pelo site Kaggle, que pode ser encontrada em https://www.kaggle.com/datasets/tarundalal/100-richest-people-in-world .

#### **3.1 *Queries* realizadas em SQL para entender a base de dados utilizada**

* Obter a média das idades:
```
SELECT AVG (idade)
from dbo.nomes;
```

* Selecionar os países distintos:
``` 
SELECT DISTINCT Pais
from dbo.pais_origem;
```

* Selecionar os seguimentos distintos das empresas:
```
SELECT DISTINCT seguimento
FROM dbo.seguimento_empresa;
```

* Selecionar os seguimentos distintos das empresas:
```
SELECT SUM (patrimonio_liquido)
FROM dbo.patrimonio_liquido;
```

* União entre as tabelas pessoa e empresa:
```
SELECT top 10 pessoa, patrimonio_liquido, empresa
FROM dbo.pessoa as t1
LEFT JOIN dbo.empresa_pessoa as t2
ON t1.id_nome = t2.id_nome;
```

* União entre as tabelas pessoa, empresa e seguimento:
```
SELECT top 10 pessoa, empresa, seguimento
FROM dbo.pessoa as t1
LEFT JOIN dbo.empresa_pessoa as t2
ON t1.id_nome = t2.id_nome
LEFT JOIN dbo.seguimento_pessoa as t3
ON t2.id_empresa = t3.id_empresa;
```
 ### **4.BASE DE DADOS NO POWER B.I**

#### **4.1 Transformação dos Dados (Power Query)**

**Tabela 1 - Pessoa:** Foi acrescentada a coluna gênero; Ajuste do tipo de dado da Coluna patrimonio_liquido para número decimal fixo, de forma que os valores ficaram em um mesmo formato.

Nas demais tabelas, as primeiras linhas foram aplicadas como cabeçalho, pois os nomes das colunas estavam como um dado.

Sem mais transformações, foi gerado o Relacionamento entre as tabelas abaixo:

![e-r powwr bi](https://user-images.githubusercontent.com/112497138/193326959-1d7b2491-6cb3-486e-8b2f-3b9affafaaac.jpeg)

#### **4.2  MEDIDAS CALCULADAS (DAX)**

**Função DIVIDE:**
* Foi utilizado para divisão do patrimônio líquido, entender qual seria o patrimônio líquidos das pessoas por mês mediante o valor total apresentado em 2022, código:
`patrimonio_mes = DIVIDE(Pessoa[patrimonio_liquido],12);`
* e por dia, código:
`patrimonio_dia = DIVIDE(Pessoa[patrimonio_liquido],365);`

**Medida DISTINCT COUNT:**
Utilizado para uma contagem distinta das empresas, código 
`empresa_distinta = DISTINCTCOUNT(Empresa[empresa]);`
* seguimento das empresas, código
`seg_distinto = DISTINCTCOUNT(Seguimento[seguimento];`
* países de origem da empresa, código
`pais_distinto = DISTINCTCOUNT(Pais[id_pais]).`


**Função IF:**
* Na tabela País_Origem, foi possível verificar quais empresas são americanas (a maioria) e quais não são, código:
`nacionalidade_empresa = IF(Pais_Origem[pais] = "United States", "Americana","Outra Nacionalidade");`
* Na tabela Pessoa foi utilizado para entender quais bilionários são idosos (na classificação brasileira de maiores de 65 anos), código:
`Idoso_Bilionario = IF(Pessoa[idade] > 65, "Idoso Bilionario", "Não é idoso, mas é Bilionario")
nacionalidade_empresa = IF(Pais_Origem[pais] = "United States", "Americana","Outra Nacionalidade");`


### **5.DASHBOARD**

O modelo para a base do dashboard foi baixado no site da comunidade do Power BI (https://community.powerbi.com/t5/Themes-Gallery/Seppirus-Dark-Mode-Theme/td-p/891059 ) e o escolhido foi Seppirus Dark.

ABA 1: Pessoa - Patrimônio  

* Filtro com os países distintos e o gênero;
* KPI’s apresentando a soma dos patrimônios líquidos e a média da idade das pessoas;
* Gráfico de  pizza apresentando a quantidade de bilionários do gênero feminino e masculino;
* Gráfico de barra apresentando o nome das 100 pessoas e seu patrimônio líquido;
* Inserção do logo da Coder House.

![aba1-powebi](https://user-images.githubusercontent.com/112497138/193327826-4eb55386-efee-4cee-afe0-1c105655ab1c.jpeg)

ABA 2: Pessoa - Empresa

* Filtro com os países distintos e o gênero;
* Inserção do logo da Coder House.
* Gráfico de seguimento de empresa, apresentando os tipos de seguimentos e  quantidade de pessoas para cada um;
* Tabela listando o nome das empresas e seus respectivos proprietários
* KPI’s apresentando a quantidade distinta de empresas e seguimentos das empresas. 

![aba3-powerbi](https://user-images.githubusercontent.com/112497138/193327919-59eb385d-81f2-42b7-bd32-28c34004566f.jpeg)

ABA 3: Pessoa - País

* Filtro com os países distintos e o gênero;
* Tabela listando os países e quantidade de pessoas ricas por gênero;
* Gráfico de mapa apresentando os continentes e demarcando os países com mais bilionários.

![aba3-powerbi](https://user-images.githubusercontent.com/112497138/193328174-78859b25-3d73-45fc-9897-d23ea9ebc55a.jpeg)




