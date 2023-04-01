# Ferramentas de análise de dados
Este máterial tem objetivo de apresentar as principais ferramentas para análise de dados, 
mostrando bibliotecas e métodos essenciais para todo analista de dados.<br>
<br>

| Tutorial    | Descrição/Link  |
| --- | --- |
|   Phython - Pandas I  | [Aula I sobre pandas com muitas dicas iniciais para análise de dados usando pandas.](https://medium.com/@dev.daniel.amorim/python-pandas-24ab58577de5)

## Códigos Fontes com exemplos de utilização

* [Código 1 - Ferramentas Pandas essênciais](https://github.com/dev-daniel-amorim/Analise_de_dados-Ferramentas/blob/main/Pandas%20essenciais.ipynb)
* [Código 2 - Análise loja 01](https://github.com/dev-daniel-amorim/Analise_de_dados-Ferramentas/blob/main/An%C3%A1lise%20de%20dados%20(pandas).ipynb)

<br>
:construction: ESTE MATÉRIAL ESTÁ EM CONSTANTE ATUALIZAÇÃO :construction:


# Índice 

* [Biblioteca Pandas](#biblioteca-pandas)
* [Biblioteca Pathlib](#biblioteca-pathlib)
* [Conversão de dados](#conversão-de-dados)
* [Desenvolvedor](#desenvolvedor)

# Biblioteca Pandas

Pandas é uma das principais bibliotecas de manipulação de dados/tabelas do python.

#### Importando pandas:
    import pandas as pd
    
#### Criando uma tabela vazia:
    table = pd.DataFrame()
    
#### Lendo uma tabela:
    df = pd.read_csv(r'caminho do arquivo')
    
#### Ver informações de cada item da tabela (tipo de dados):
    df.info()
    
#### Lendo colunas específicas:
    df = df[['coluna 1', 'coluna 2' ...]]
<hr> 
<br>
   
## LOC[ ] 
localizar todas as linhas onde "coluna mes = janeiro":
    
    df.loc[df["coluna mes"] == "janeiro"]

Pegar o número do INDEX onde "coluna mes = janeiro":
    
    df.loc[df["coluna mes"] == "janeiro"].index
       
Localizar item pelo título do index e da coluna:

    db.loc[titulo da linha, titulo da coluna]
    
## ILOC[ ]
Localizar item pelo número do index e da coluna:

    db.iloc[numero da linha, numero da coluna]  
## ZIP()
Cria uma lista de tuplas com elemetos dos argumentos.<br>


    x = [1, 2, 3]
    y = [4, 5, 6]

    for t in zip(x, y):
        print(t)

    (1, 4)
    (2, 5)
    (3, 6)

<a href='http://devfuria.com.br/python/built-in-zip/'> Para mais sobre zip() clique aqui!</a>
      
## DROP()
Exclui linhas ou colunas deuma tabela.<br>
Parâmetros:
* labels: String ou lista de strings referentes ao nome de linhas ou colunas.
* axis: 0 ou 'index' para linhas, e 1 ou 'columns' para colunas.
* inplace: True, altera o dataframe original sem precisar atribuir ao próprio dataframe.

Removendo uma lista de colunas:
    
    df = df.drop(['coluna 1', 'coluna 2' ...], axis=1)
    
Removendo uma lista de index:
    
    df = df.drop([1, 3 ...], axis=0)
    
DESAFIO: Remover todas as linhas da coluna "Salario", onde salário <= 0:
    
    # pegaa lista de indexs onde salario <= 0
    indexs = df.loc[df['Salario']<=0].index   
    
    # para cada index na lista de index exclui a linha
    for index in indexs:
        df.drop(index=index, inplace=True)

## DROPNA()
Remove todos os valores nulos (NULL) de uma tabela por default.

    df = pd.read_csv('data.csv')
    newdf = df.dropna()
    
Excluindo valores vazios somente de uma coluna específica:<br>
Parâmetro:<br>
subset= ['Nome da coluna']<br>

    df = pd.read_csv('data.csv')
    df.dropna(subset= ['Nome da coluna'], inplace=True)
      
## FILLNA()
Remove ou substitui todos valores vazios de uma coluna ou tabela.<br>
Parâmetros: <br>
- Values = substitui todos os valores "vazios" por alguma valor indicado aqui (no exemplo abaixo por False).
- inplace: True, executa sem precisar atribuir a mesma tabela.
- axis: 0 linhas e 1 colunas.

Considerando uma coluna "tem filhos" (com dados True e False) as linhas vazias vão ser substituidas pelo valor False:

        df["Tem filhos"].fillna(value=False, inplace=True, axis=0)


## MERGE()
Podemos mesclar tabelas com o MERGE, para isso temos que ter em todas as 
tabelas a serem mescladas uma coluna com mesmo nome para todos (esse sera nosso ID):

    new_df = df1.merge(df2, on="coluna") 
    ** onde coluna = nome da coluna comum as duas tabelas (ID)
    
## RENAME()
Alterando nome de uma coluna

    df = df.rename(columns={'nome_antigo': 'novo_nome'})

## LISTA DE COLUNAS DE UMA TABELA

    lista = (df.columns)
    
## ANÁLISE EXPLORATÓRIA INICIAL
Dicas de comandos para análise exploratória inicial:

    df.dtypes # Mostra tipos de dados de uma tabela (ou df['col'].dtypes p/ coluna)
    df.info() # informações e total e nao null
    df.isnull().sum() #soma todos os nulos
    df.iloc[0] # mostra o primeiro dados de cada coluna
    df.describe # informações descritivas de cada coluna inclusive quartis
    df.shape # numero de linhas e de colunas da tabela
    
    # dica: calculo de % de dados faltantes nas colunas
    (df.isnull().sum() / df.shape[0] *100).sort_values()
    
    
## NUNIQUE()

Conta nos eixo 0 (linha) ou 1 (coluna) a quantidade de valores unicos.<br>
Parâmetros:<br>
axis= 0 'índice', 1 'colunas', padrão 0<br>
dropna= True, não inclui NaN nas contagens.<br>

    df = pd.DataFrame({"A":[14, 4, 5, 4, 1],
                       "B":[5, 2, 54, 3, 2],
                       "C":[20, 20, 7, 3, 8],
                       "D":[14, 3, 6, 2, 6]})
    df.nunique(axis = 1)
   
SAÍDA:<br>
![1-603](https://user-images.githubusercontent.com/115194365/211131770-cf428b15-2ece-4fd5-9e6c-9809c056b74c.png)
   
## UNIQUE()
Igual o NUNIQUE, porém ele mostra uma lista de quais são os dados que são únicos (sem repeti-los).
 
    df = pd.DataFrame({"A":[None, "olivia", "olivia", "", "amanda"]})
    print(df['A'}.unique()
 
SAÍDA:<br>
    [Nam, 'olivia', "", 'amanda']
    
## VALUE_COUNTS()
Parâmetros:
normalize=True, se definido esse parâmetro, mostra aporcentagem de cada valor.
Conta quantas vezes cada classe aparece numa coluna (imprescindível para balanceamento de classes).

    df['coluna'].value_counts()
    
## GROUPBY()
Agrupa classes de uma coluna, transformando-os em index da tabela e realizando uma ação com as demais colunas:<br>
Ações:
* .SUM(): Para somar os itens.
* .MEAN(): Para calcular a média dos itens.
* .COUNT(): Conta a quantidade de itens naquela coluna.

        db = db.groupby('nomedacoluna').sum()
    
## SORT_VALUES()
Ordena linhas de uma coluna:
* Crescente: ascending=True
* Decrescente: ascending=False
* by: Por coluna: df.sort_values(by='nome da coluna')

Exemplo:

    df = df.sort_values('nome da coluna a ordenar', ascending=True) 


## DESCRIBE()
Resumo estatístico do DataFrame, com quartis, mediana, etc.

    df.describe()
    
## MEDIAN()
Mediana dos valores

    df.median()
    
## MODE()[0]
Calcula a moda dos valores (valor que mais se repete)

    df['coluna'].mode()

## INDEX()
Pega o texto de um indexquando não numérico:

    db.index(0)

Pega o index de um item na coluna:

    df.loc[df['Funcionário'] = joao].index 
    
Cria uma lista de index onde salário é maior que 1000:

    indexs = df.loc[df['Salario'] > 1000].index  


## SET_INDEX()
Transformando coluna em linha:

    new_df = df.set_index('nome da coluna')
    
## MAX e MIN
Pega valor máximo e mínimo de uma coluna:

    df = max(df['coluna x'])
    df = min(df['coluna x'])
    
## APPLY()
Aplica uma função pré definida para cada item em uma coluna:

    def format(valor): #valor é cada item da coluna
        return valor.replace("gmail", "hotmail") #para vada item onde tem "gmail" substituir por "hotmail

    tabela['E-mail'] = tabela['E-mail'].apply(format) # aplica para cada item da coluna "E-mail" a função format
    display(tabela)

## Usando SHAPE, ISNULL e SUM para calcular porcentagem de dados nulos em uma tabela

### SHAPE
df.shape: Mostra a quantidadede total linhas e colunas de uma tabela.<br>
### ISNULL().SUM()
df.isnull().sum: Soma a qunatidade de valores nulos em cada coluna.<br>

ENTÂO, se eu tenho a quantidade de valores nulos, dividir pela quantidade total e multiplicar por 100, eu tenho a porcentagem de valores nulos em uma tabela, vamos pra prática!

    (tabela.isnull().sum() / tabela.shape[0] * 100).sort_values()
    
A saída vai ser um relatório com porcentagem de nulos em cada coluna da tabela.

## MAP()
Aplica uma função as linhas de uma coluna.
- Considerando uma coluna "Tem filhos" com valores TRUE e FALSE, vamos substituir por SIM e NAO:
    
        df["Tem filhos"] = df["Tem filhos"].map({False:"Não", True:"Sim"})

## Salvando uma tabela

    df.to_csv('caminho/arquivo.extensao', sep=';', encoding='latin1')
    
Tipos de encoding: encoding='utf-8', encoding='cp1252', encoding='latin1' ou encoding='ISO-8859-1'<br>
Sep: É o tipo de separador entre os dados, pode ser ponto, virgula etc.

## Transformando um dicionário em um data frame

    dict = {"carro": "corsa", "marca": "chevrolet"}
    df = pd.DataFrame.from_dict(dict, orient='index')
    
Parametro orient='index' transforma os nomes das colunas em nome dos index das linhas.<br>
![Captura de tela_20230104_165202](https://user-images.githubusercontent.com/115194365/210638089-8d949580-ddf3-4cb3-9cb9-c2bf83581ce9.png)
 
## Transformando uma lista de tuplas em data frame

    lista_tupla = [('nome', 'preco', 'link'), ('nome', 'preco', 'link')]
    nova_tabela = pd.DataFrame(lista_tupla, columns=['nome', 'preco', 'link'])
    
## Concatenando 2 tabelas(ou mais) em 1 tabela principal:

    tabela_principal = pd.DataFrame()
    tabela_principal = pd.concat([tabela_principal, tabela1])
    tabela_principal = pd.concat([tabela_principal, tabela2])
    # Feito isso juntamos 2 tabelas em uma só
    # os index irão meio bagunçado entao usamos reset_index para reordenar os index:
    # drop=True descarta os index antigos (bagunçados)
    tabela_principal = tabela_principal.reset_index(drop=True)

## Somando os valores de 2 colunas e colocando resposta em uma coluna não existente
Quando a gente faz referencia em uma tabela a uma coluna que não existe, o pandas cria essa coluna automaticamente, vejamos:<br>
Some o valor da coluna 'TotalPay' com os valores da coluna 'TotalPayBenefits', em uma coluna chamada 'Total geral' (não existente):

    tabela_sal_total['Total geral'] = tabela_sal_total['TotalPay'] + tabela_sal_total['TotalPayBenefits']
    display(tabela_sal_total)
    
IMPRIME:<br>
![Captura de tela_20230106_171513](https://user-images.githubusercontent.com/115194365/211092281-46eb7a86-0077-4350-a49f-baa9eb2ed8b0.png)

## Operações aritméticas em Series:

    s = pd.Series([1, 2, 3, 4, 5], index=['a', 'b', 'c', 'd', 'e'])
        
## Somando todos os valores presentes na Series por 2

    s.add(2)
    
## Subtraindo 2 de todos os valores

    s.sub(2)
    
## Multiplicando todos os valores por 2

    s.mul(2)
    
## Dividindo valores por 2

    s.div(2)


# Biblioteca Pathlib

Pathlib é uma biblioteca para manipulação de arquivos ou pastas no computador.<br>
* <a href="https://docs.python.org/3/library/pathlib.html">Ir para documentação Pathlib</a>

#### Importanto pathlib:

    import pathlib
    
Vamos supor que queremos ler todos os arquivos e pastas da área de trabalho do seu computador e depois criar a pasta "teste" e salvar dentro dela uma tabela ficticia (my_table) com nome de "minha tabela":<br>

Primeiro devemos definir o caminho da "área de trabalho"(desktop):

    caminho = pathlib.Path(r"c:/desktop")
    
<h5>ITERDIR()</h5> - Com esta classe pegamos todos os arquivos e pastas do caminho acima, então podemos colocar cada objeto numa lista (iterable), ou seja, uma lista no qual podemos iterar um valor de cada vez:

    arquivos_desktop = caminho.iterdir()

<h5>.NAME</h5> - Com .name iremos ler cada item da lista de objetos acima, e coloca-los em uma lista usando for:

    lista_itens = []
    for item in arquivos_desktop:
        lista_itens.append(item.name) # append adiciona o ".NAME" do item à lista
    print(lista_itens)
    
 IMPRIME:<br>
 
    ['lixeira', 'documents', 'minhas imagens'] # vai imprimir todos itens do seu desktop

<h5>MKDIR()</h5> Com mkdir podemos criar uma pasta no caminho específico:

    novapasta = caminho / teste #cria a pasta de nome "teste" no "caminho"
    novapasta.mkdir()
    
<h5>TO_CSV()</h5> Salvando a tabela "minha tabela" na pasta "teste" com formato CSV:
    
    my_table.to_csv("c:/desktop/teste/minha_tabela.csv")
    #supondo que "my_table" seja uma dataframe já existente, que será salva com nome "minha tabela"

# Conversão de dados

Ferramentas de conversão de dados.

#### Conversão de datas (TO_DATETIME())

Datas geralmente não são reconhecidas, pra isso temos que converter datas de uma tabela para 
datetime, o pandas faz isso com PD.TO_DATETIME():

    - df[nomedacoluna] = pd.to_datetime(df[nomedacoluna], format='%d/%m/%Y')
    
OBS: no format='%d/%m/%Y' temos que informar pro pandas qual formato "está formatada a tabela"
para assim ela fazer a conversão correta.<br>
Depois de convertida a data para datetime temos acesso ao metodo (.day), (.month) e (.ano)<br>
Exemplo como pegar o mês em um date time:

    - mes = df['data'].month
    * método .month extrai somente o mês da data.

    
# Desenvolvedor

| [<img src="https://user-images.githubusercontent.com/115194365/202005566-f6278b6c-4f75-416f-b01c-e79b8d04f02e.jpg" width=115><br><sub>Daniel de Souza Amorim</sub>](https://github.com/DaniellsamorimGit) |
| :---: | 
