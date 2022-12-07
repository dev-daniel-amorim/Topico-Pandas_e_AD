# Análise de dados (Pandas)
 Análise de dados em Python usando Pandas e Jupyter Notebook.

# Índice 

* [Descrição do Projeto](#descrição-do-projeto)
* [Desenvolvedor](#desenvolvedor)
* [Lista de comandos](#Lista-de-comandos)
* [Calculadora IMC](#Calculadora-IMC)

# Descrição do projeto
 O intuito deste material é fazer uma análise didática de uma base de dados de uma empresa usando a biblioteca Pandas, que permite manipular,
 e analisar diversas fontes de dados (excel, csv, pdf etc).
 Neste tutorial iremos usar dados fictícios de uma empresa, para com base nessas informações extrair algumas perguntas que podem
 contribuir para o sucesso da organização.

# Desenvolvedor

| [<img src="https://user-images.githubusercontent.com/115194365/202005566-f6278b6c-4f75-416f-b01c-e79b8d04f02e.jpg" width=115><br><sub>Daniel de Souza Amorim</sub>](https://github.com/DaniellsamorimGit) |
| :---: | 

# Lista de comandos

Segue a lista e descrição dos comandos da biblioteca Pandas que iremos aprender neste tutorial:

#### Importando pandas:
    - import pandas as pd
#### Lendo um arquivo:
    - df = pd.read_csv(r'caminho do arquivo')
#### Ver informações de cada item da tabela (tipo de dados):
    - df.info()
#### Lendo colunas específicas:
    - df = df[['coluna 1', 'coluna 2' ...]]
#### pegando valor max e min de uma coluna:
    - df = max(df['coluna x'])
    - df = min(df['coluna x'])
#### Comando .loc[...] localiza item com base num parametro:
    - df.loc[df["coluna mes"] == "janeiro"]
#### Removendo colunas(axis=1) ou linhas(axis=0) específicas .drop():
    - df = df.drop(['coluna 1', 'coluna 2' ...], axis=1)
    
    
    
    
    
    
    
    
    
    
    
    
    
