# alura-store-analise-dados
# Projeto de Análise de Dados — Alura Store

## Descrição

Este projeto tem como objetivo aplicar conceitos de análise de dados em Python para extrair insights sobre as vendas dos produtos da Alura Store. Através da manipulação de dados, cálculos de faturamento, filtragem por avaliação e visualização gráfica, foi possível identificar os produtos mais vendidos e melhor avaliados.

## Funcionalidades Implementadas

- Carregamento dos dados a partir de arquivo CSV com leitura usando `csv.DictReader`.
- Cálculo do faturamento total considerando preço e quantidade vendida.
- Identificação de produtos com avaliação mínima para destacar os bem avaliados.
- Geração de gráfico de barras com os 5 produtos mais vendidos usando `matplotlib`.

## Tecnologias e Bibliotecas Utilizadas

- Python 3.x
- Biblioteca `matplotlib` para visualização gráfica

## Instruções para Execução

1. Clone este repositório:

   ```bash
   git clone https://github.com/SEU_USUARIO/alura-store-analise-dados.git

Codigo 

import csv
import matplotlib.pyplot as plt

def carregar_dados(nome_arquivo):
    produtos = []
    with open(nome_arquivo, newline='', encoding='utf-8') as csvfile:
        leitor = csv.DictReader(csvfile)
        for linha in leitor:
            linha["preco"] = float(linha["preco"])
            linha["avaliacao"] = float(linha["avaliacao"])
            linha["vendidos"] = int(linha["vendidos"])
            produtos.append(linha)
    return produtos

def calcular_faturamento(produtos):
    total = 0
    for produto in produtos:
        total += produto["preco"] * produto["vendidos"]
    return total

def produtos_bem_avaliados(produtos, nota_minima=4.0):
    bons = []
    for produto in produtos:
        if produto["avaliacao"] >= nota_minima:
            bons.append(produto)
    return bons

def plotar_mais_vendidos(produtos):
    produtos_ordenados = sorted(produtos, key=lambda p: p["vendidos"], reverse=True)
    nomes = [p["nome"] for p in produtos_ordenados[:5]]
    vendidos = [p["vendidos"] for p in produtos_ordenados[:5]]

    plt.figure(figsize=(10, 5))
    plt.bar(nomes, vendidos, color='blue')
    plt.title("Top 5 Produtos Mais Vendidos")
    plt.xlabel("Produto")
    plt.ylabel("Quantidade Vendida")
    plt.show()

if __name__ == "__main__":
    produtos = carregar_dados("produtos.csv")
    faturamento_total = calcular_faturamento(produtos)
    bons_produtos = produtos_bem_avaliados(produtos)

    print(f"Faturamento total: R$ {faturamento_total:.2f}")
    print("Produtos bem avaliados:")
    for produto in bons_produtos:
        print(f"{produto['nome']} - Nota: {produto['avaliacao']}")

    plotar_mais_vendidos(produtos)



