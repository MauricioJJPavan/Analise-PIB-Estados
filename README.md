# Analise-PIB-Estados

import pandas as pd
import matplotlib.pyplot as plt
from matplotlib.backends.backend_pdf import PdfPages
import seaborn as sns

# arquivo CSV que eu quero analisar
nome_arquivo = 'Estados_POP_PIB.csv'

# carregar esses dados no meu DataFrame
df = pd.read_csv(nome_arquivo, delimiter=';')

# formatação dos números
df['Populacao_2021'] = pd.to_numeric(df['Populacao_2021'], errors='coerce')
df['PIB_PerCapita_2019'] = pd.to_numeric(df['PIB_PerCapita_2019'], errors='coerce')

# primeiras linhas do meu DataFrame
print("\nResumo das primeiras linhas do DataFrame:")
print(df.head())

# Algumas estatísticas desses dados
summary_stats = df.describe()

# criar um PDF pra salvar
with PdfPages('analise_completa_PibEstados.pdf') as pdf:

    # ajustar o tamanho dos gráficos
    plt.figure(figsize=(15, 40))

    # gráfico de barras pra mostrar a população de cada estado
    plt.subplot(4, 1, 1)
    sns.barplot(x='Populacao_2021', y='Estado', data=df, palette='viridis')
    plt.title('População em 2021')

    # gráfico de barras para mostrar o PIB per capita de cada estado
    plt.subplot(4, 1, 2)
    sns.barplot(x='Estado', y='PIB_PerCapita_2019', data=df, palette='viridis')
    plt.title('PIB Per Capita em 2019')

    # gráfico de dispersão
    plt.subplot(4, 1, 3)
    sns.scatterplot(x='Populacao_2021', y='PIB_PerCapita_2019', data=df, hue='Estado', palette='viridis')
    plt.title('Dispersão entre População e PIB Per Capita')

    # boxplot pra entender melhor a distribuição do PIB per capita
    plt.subplot(4, 1, 4)
    sns.boxplot(x='PIB_PerCapita_2019', y='Estado', data=df, palette='viridis')
    plt.title('Boxplot do PIB Per Capita')

    # adicionar gráficos no PDF
    pdf.savefig()

    # resumo estatístico no PDF
    plt.figure(figsize=(10, 6))
    plt.axis('off')
    plt.table(cellText=summary_stats.values,
              rowLabels=summary_stats.index,
              colLabels=summary_stats.columns,
              cellLoc='center', loc='center')
    pdf.savefig()

# Pronto
print("Análise completa salva em analise_completa_PibEstados.pdf")

![Screenshot_5](https://github.com/MauricioJJPavan/Analise-PIB-Estados/assets/132507042/69e85e0c-69ea-4d20-ad5e-81ff006491e0)

![Screenshot_1](https://github.com/MauricioJJPavan/Analise-PIB-Estados/assets/132507042/f3cfca48-5f6a-4c68-b332-168d2767e7ea)

![Screenshot_2](https://github.com/MauricioJJPavan/Analise-PIB-Estados/assets/132507042/6468f4fa-832e-497c-acbf-1d8c24638499)

![Screenshot_3](https://github.com/MauricioJJPavan/Analise-PIB-Estados/assets/132507042/f45b9053-a84c-47a6-a570-6db46eb44fdd)

![Screenshot_4](https://github.com/MauricioJJPavan/Analise-PIB-Estados/assets/132507042/38deb76c-f1d7-4f42-9e24-5e193e1745b1)

![Screenshot_6](https://github.com/MauricioJJPavan/Analise-PIB-Estados/assets/132507042/72c4f6e7-a176-4146-8030-16144f0bf30b)


