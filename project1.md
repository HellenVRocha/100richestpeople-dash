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
```  SELECT DISTINCT Pais
from dbo.pais_origem;

---Selecionar os seguimentos distintos das empresas:
SELECT DISTINCT seguimento
FROM dbo.seguimento_empresa;

---Selecionar os seguimentos distintos das empresas:
SELECT SUM (patrimonio_liquido)
FROM dbo.patrimonio_liquido;

---União entre as tabelas pessoa e empresa:
SELECT top 10 pessoa, patrimonio_liquido, empresa
FROM dbo.pessoa as t1
LEFT JOIN dbo.empresa_pessoa as t2
ON t1.id_nome = t2.id_nome;

---Selecionar os seguimentos distintos das empresas:
SELECT top 10 pessoa, empresa, seguimento
FROM dbo.pessoa as t1
LEFT JOIN dbo.empresa_pessoa as t2
ON t1.id_nome = t2.id_nome
LEFT JOIN dbo.seguimento_pessoa as t3
ON t2.id_empresa = t3.id_empresa;





