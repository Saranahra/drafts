# Aprendendo Python

**Lógica de Programação**
**Passo a passo de solução do desafio

- Passo 0: Entender o desafio que você quer resoler.

- Passo 1: Percorrer todos os arquivos da pasta base de dados (Pasta Vendas).
  
import os

lista_arquivo = os.listdir("/content/drive/MyDrive/01-15 - Curso de Python - Aula 1-20230713T190721Z-001(1) (1)/01-15 - Curso de Python - Aula 1/Vendas")

print(lista_arquivo)

- Passo 2: Importar as bases de dados de vendas. (Estrutura de repetição e Format)
  (for intem in lista_itens:)

  
lista_arquivo = os.listdir("/content/drive/MyDrive/01-15 - Curso de Python - Aula 1-20230713T190721Z-001(1) (1)/01-15 - Curso de Python - Aula 1/Vendas") 
print(lista_arquivo)
for arquivo in lista_arquivo: 
  print(arquivo)
  print(f"/content/drive/MyDrive/01-15 - Curso de Python - Aula 1-20230713T190721Z-001(1) (1)/01-15 - Curso de Python - Aula 1/Vendas/{arquivo}")
  

- Passo 3: Tratar / Compilar as bases de dados.

# Lógica de Programação
import os
import pandas as pd
#pd é abreviação de pandas

lista_arquivo = os.listdir("/content/drive/MyDrive/01-15 - Curso de Python - Aula 1-20230713T190721Z-001(1) (1)/01-15 - Curso de Python - Aula 1/Vendas") 
print(lista_arquivo)
tabela_total = pd.DataFrame()
for arquivo in lista_arquivo: 
  if "Vendas" in arquivo:
  # if "vendas" in arquivo.lower(): (para deixar todas as letras minúsculas)
    tabela = pd.read_csv(f"/content/drive/MyDrive/01-15 - Curso de Python - Aula 1-20230713T190721Z-001(1) (1)/01-15 - Curso de Python - Aula 1/Vendas/{arquivo}")
    tabela_total = tabela_total.append(tabela)
    display(tabela_total)

- Passo 4: Calcular o produto mais vendido (em quantidade).
  Queremos agrupar uma coluna da tabela (coluna de produtos) e somar a quantidade vendida:
  
tabela_produtos = tabela_total.groupby('Produto').sum()
tabela_produtos = tabela_produtos[["Quantidade Vendida", "Preco Unitario"]].sort_values(by="Quantidade Vendida", ascending=True)
display(tabela_produtos)

- Pasos 5: Calcular o produto que mais faturou (em faturamento).
Criar uma nova coluna de Quantidade Vendida x Preco Unitario:

tabela_total['Faturamento'] = tabela_total['Quantidade Vendida'] * tabela_total['Preco Unitario']
tabela_faturamento = tabela_total.groupby('Produto').sum ()
tabela_faturamento = tabela_faturamento[["Faturamento"]].sort_values(by="Faturamento", ascending = True)
display(tabela_faturamento)

- Passo 6: Calcular a loja / cidade que mais vendeu (em faturamento) - criar um gráfico / dashboard.

  
tabela_lojas = tabela_total.groupby('Loja').sum()
tabela_lojas = tabela_lojas[['Faturamento']]
display(tabela_lojas)

# Para criar gráficos usando Pyton:
import plotly.express as px

grafico = px.bar(tabela_lojas, x=tabela_lojas.index, y='Faturamento')
grafico.show()
