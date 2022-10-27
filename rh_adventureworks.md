### **ANALISE DE DADOS DE RH DAADVENTURE WORKS. ABORDANDO CONHECIMENTO EM POWER BI**

#### **1.INTRODUÇÃO**

A base de dados foi cedida durante as aulas do curso de Data Analytics pela Coder House e foi escolhida para realizar análise em Power BI, para demonstração de habilidade em DAX e criação de Dashboard.

##### **1.1 OBJETIVO**
O dashboard é destinado aos líderes de Recursos Humanos da AdventureWorks que precisam conhecer o status da organização para poder solicitar oportunamente mudanças à gerência no comitê de operações.  Este trabalho tem por objetivo explorar e responder às seguintes questões:

**Aba 1. Funcionários.**
* Quantidade total
* Quantidade por gênero (M, F)
* Quantidade por gerência
* Número de funcionários por turno
* Número de contratações por ano

**Aba 2. Salários.**
* Soma total
* Média total
* Número de funcionários por cargo e faixa salarial
* Salário médio por gerência.


 #### **2.ANALISANDO A BASE DE DADOS NO POWER B.I**

Foi acrescentada a tabela Calendário, tendo como referência à tabela principal de informações através da data principal (data de entrada), sendo construído as colunas de Data, ano e mês, onde foi possível gerar o Relacionamento entre as tabelas abaixo:

![e-r adventure](https://user-images.githubusercontent.com/112497138/196554255-b413bf52-6384-4827-8c9e-2e0524f201ff.jpeg)

**2.1  MEDIDAS CALCULADAS (DAX)**

**Tabela CALENDAR:**
* Para uma melhor análise dos dados em relação ao tempo, foi criada a tabela CALENDÁRIO, possuindo as colunas de data_entrada:
`CALENDARIO = 
CALENDAR(
MIN(
'RH ADVENTUREWORKS'[DATA_ENTRADA]),
MAX('RH ADVENTUREWORKS'[DATA_ENTRADA])
)`
 
* Ano: `ANO = YEAR(CALENDARIO[Date])`

* E Mês: `MES = MONTH(CALENDARIO[Date])`

**Função SUM:**
* Para o cálculo da soma do salário dos funcionários, código: 
`SomaSalarios = SUM('RH ADVENTUREWORKS'[SALARIO])`
 
* Cálculo da quantidade total de funcionários, código: 
`TotalFunc = SUM('RH ADVENTUREWORKS'[N_ID])`

**Função AVERAGE:**
* Para o cálculo da média dos salários por Gerência, código: 
`MedSalarioporGerencia =
 AVERAGEX(
'RH ADVENTUREWORKS',
'RH ADVENTUREWORKS'[SALARIO]
)`

**Função SWICTH:**
* Para o ter a descrição dos meses por extenso, código : 
`MESPOREXTENSO = SWITCH([MES], 
    1, "Janeiro", 
    2, "Fevereiro",
    3, "Marco", 
    4, "Abril",
    5, "Maio", 
    6, "Junho",
    7, "Julho",
    8, "Agosto", 
    9, "Setembro",
     10, "Outubro", 
    11, "Novembro",
     12, "Dezembro",
    "nao definido"
    )`
    
 * Para o ter a descrição dos meses por extenso, código 
 `TURNOPOREXTENSO = SWITCH(
 'RH ADVENTUREWORKS'[TURNO],
"Day","Dia",
"Night","Noite",
"Evening","Tarde"
)`

**Função IF:**
* Para enterdermos se aos funcionários deveriam receber adicional noturno ou não, código 
`Adicional Noturno = IF(
    'RH ADVENTUREWORKS'[TURNOPOREXTENSO]= 
    "Noite", "Deveria receber adicional noturno", "Não há necessidade de adicional"
    )`

   
**DASHBOARD**

O modelo para a base do dashboard foi baixado no site da comunidade do Power BI (https://community.powerbi.com/t5/Themes-Gallery/Nowalls-Analytics/td-p/772564) e o escolhido foi Nowalls Analytics.

**ABA 1: Funcionários**

* Filtro com o ano, gênero e turno;
* KPI apresentando a soma total de funcionários
* Gráfico de barras empilhadas apresentando a quantidade de funcionários por turno;
* Gráfico de  pizza apresentando a quantidade de funcionários por gênero;
* Gráfico de barras empilhadas apresentando a quantidade de funcionários por gerência 
* Gráfico de linha demonstrando o número de contratações por ano.

![aba1 adventure](https://user-images.githubusercontent.com/112497138/197027992-a3e77dcb-5e0b-4f99-bf2a-e9418e2c324b.jpeg)


**ABA 2: Salários**

* Filtro com o ano, gênero e turno;;
* Cartões apresentando soma e média de salários.
* Gráfico de barras apresentando o salário médio por gerência
* Tabela listando a média salarial e quantidade de funcionários por departamento;


![ABA2-ADVETURE](https://user-images.githubusercontent.com/112497138/197030923-24c9ad6b-5096-4463-974a-98d4265c9fb3.jpeg)


