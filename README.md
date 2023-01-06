# Ferramentas de análise de dados
Este máterial tem objetivo de apresentar as principais ferramentas para análise de dados, 
mostrando bibliotecas e métodos essenciais com objetivo de criar uma consulta rápida.<br>
<br>
:construction: ESTE MATÉRIAL ESTÁ EM CONSTANTE ATUALIZAÇÃO :construction:


# Índice 

* [Pandas](#pandas)
* [Pathlib](#Pathlib)
* [Conversão de dados](#conversão-de-dados)
* [Desenvolvedor](#desenvolvedor)

# Pandas

Pandas é uma das principais bibliotecas de manipulação de dados/tabelas do python.

#### Importando pandas:
    - import pandas as pd
    
#### Criando uma tabela (preparação inicial)
    - table = pd.DataTable()
    # Feito isso criamos uma tabela chamada "table" vazia
    
#### Lendo um arquivo:
    - df = pd.read_csv(r'caminho do arquivo')
    
#### Ver informações de cada item da tabela (tipo de dados):
    - df.info()
    
#### Lendo colunas específicas:
    - df = df[['coluna 1', 'coluna 2' ...]]
    
#### Pegando valor max e min de uma coluna:
    - df = max(df['coluna x'])
    - df = min(df['coluna x'])
    
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
    
      
## DROP()
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


## MERGE()
Podemos mesclar tabelas com o MERGE, para isso temos que ter em todas as 
tabelas a serem mescladas uma coluna com mesmo nome para todos (esse sera nosso ID):

    new_df = df1.merge(df2, on="coluna") 
    ** onde coluna = nome da coluna comum as duas tabelas (ID)
    
## RENAME()
Alterando nome de uma coluna

    df = df.rename(columns={'nome_antigo': 'novo_nome'})
    
## VALUE_COUNTS()
Contando quantas vezes um item aparece na tabela.
No caso abaixo vai mostrar quantas vezes cada cliente comprou já que cada compra de cada cliente fica registrada.

    - compras_cada_cliente = df_vendas['compra cliente'].value_counts()
    
## GROUPBY()
Agrupa itens de uma coluna, transformando os itens em index e realizando uma ação com seus valores:<br>
Ações:
* .SUM(): Para somar os itens.
* .MEAN(): Para calcular a média dos itens.

    - db = db.groupby('nomedacoluna').sum()
    
## SORT_VALUES()
Ordena linhas de uma coluna:
* Crescente: ascending=True
* Decrescente: ascending=False
Exemplo:

    df = df.sort_values('nome da coluna a ordenar', ascending=True) 

## SET_INDEX()
Transformando coluna em linha:

    new_df = df.set_index('nome da coluna')
    
#### Localizando index de texto INDEX[]

    - db.index(0)
    # Pega o texto do index de posição zero
    
#### Manipulando itens de uma tabela aplicando uma função

    def format(valor): #valor é cada item da coluna
        return valor.replace("gmail", "hotmail") #para vada item onde tem "gmail" substituir por "hotmail

    tabela['E-mail'] = tabela['E-mail'].apply(format) # aplica para cada item da coluna "E-mail" a função format
    display(tabela)
    
#### Salvando uma tabela

Atenção aos parametros: encoding='utf-8', encoding='cp1252', encoding='latin1' ou encoding='ISO-8859-1'
    
    - dataframe.to_csv('nome do qrquivo.extensao', sep=';', encoding='latin1')

#### Transformando um dict em um data frame

dict = {"carro": "corsa", "marca": "chevrolet"}
Atenção, o parametro orient='index' transforma os nomes das colunas em nome dos index das linhas.

    - df = pd.DataFrame.from_dict(dict, orient='index')
    
![Captura de tela_20230104_165202](https://user-images.githubusercontent.com/115194365/210638089-8d949580-ddf3-4cb3-9cb9-c2bf83581ce9.png)
 
#### Transformando uma lista de tuplas em data frame
lista_tupla = [('nome', 'preco', 'link'), ('nome', 'preco', 'link')]

    - nova_tabela = pd.DataFrame(lista_tupla, columns=['nome', 'preco', 'link'])
    
#### Concatenando 2 tabelas(ou mais) em 1 tabela principal:

    tabela_principal = pd.DataFrame()
    tabela_principal = pd.concat([tabela_principal, tabela1])
    tabela_principal = pd.concat([tabela_principal, tabela2])
    # Feito isso juntamos 2 tabelas em uma só
    # os index irão meio bagunçado entao usamos reset_index para reordenar os index:
    # drop=True descarta os index antigos (bagunçados)
    tabela_principal = tabela_principal.reset_index(drop=True)
    

# Pathlib

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
