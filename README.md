# Laboratório de Ciência de Dados - Dashboard Interativo

Repositório para projetos das aulas de Ciência de Dados do curso técnico de desenvolvimento de sistemas.

## Descrição

Este projeto propõe a criação de um dashboard interativo utilizando Python e Streamlit para análise exploratória de dados. O aplicativo realiza filtros, apresenta visualizações e calcula estatísticas sobre o conjunto de dados.

## Instalação e Execução

### Requisitos
- Python 3.8 ou superior
- pip (gerenciador de pacotes Python)

### Passo 1: Instalar as dependências
Abra o terminal e execute:
```bash
pip install -r requirements.txt
```

### Passo 2: Executar a aplicação
No mesmo terminal, execute:
```bash
python -m streamlit run app.py
```
streamlit run app.py

A aplicação será aberta automaticamente no navegador padrão.

## Funcionalidades

- Carregamento e exibição de dados a partir de arquivo CSV
- Filtro interativo de dados no painel lateral
- Tabela de dados dinâmica
- Visualizações gráficas dos dados
- Cálculo e exibição de estatísticas

## Atividades Propostas

### Atividade 1: Modificar cores do gráfico
- Abra o arquivo `app.py` e localize a linha com `color='#FF6B9D'`
- Substitua o código de cor por outra hexadecimal (exemplos: `'#00D9FF'` para azul, `'#00FF41'` para verde)
- Salve o arquivo e observe a atualização automática no aplicativo

```python
# Exemplo de alteração
ax.bar(df_filtrado['title'], df_filtrado['release_year'], color='#00D9FF')
```

### Atividade 2: Modificar o título da página
- Localize a linha `st.title()` no arquivo `app.py`
- Altere o texto do título conforme desejado
- Salve o arquivo para visualizar a mudança em tempo real

```python
# Exemplo de alteração
st.title("Dashboard: Análise de Dados")
```

### Atividade 3: Adicionar novo filtro de dados
- Implemente um novo filtro usando `st.sidebar.slider()` para filtrar por intervalo de valores
- Integre esse filtro à lógica de filtragem existente
- Teste a funcionalidade no aplicativo

```python
# Exemplo de novo filtro
nota_minima = st.sidebar.slider("Filtrar por nota mínima:", 0.0, 10.0, 5.0)
df_filtrado = df_filtrado[df_filtrado['rating'] >= nota_minima]
```

### Atividade 4: Integrar novo dataset do Kaggle

Esta atividade propõe a substituição ou adição de um novo dataset ao projeto, praticando a adaptação de código para diferentes estruturas de dados.

#### Procedimento:

1. **Selecionar dataset no Kaggle**
   - Acesse https://www.kaggle.com/datasets
   - Escolha um dataset que contenha dados de interesse (filmes, séries, músicas, esportes, etc.)
   - Faça download do arquivo CSV

2. **Integrar o dataset**
   - Copie o arquivo CSV para a pasta do projeto
   - Abra o arquivo `app.py` e identifique a linha que carrega os dados:
   ```python
   df = pd.read_csv('dataset.csv')
   ```
   - Substitua pelo novo arquivo:
   ```python
   df = pd.read_csv('novo_dataset.csv')
   ```

3. **Adaptar o código aos novos dados**
   - Inspecione as colunas do novo dataset:
   ```python
   print(df.columns)
   print(df.head())
   ```
   - Identifique as colunas que podem ser usadas para filtros e visualizações
   - Atualize os nomes das colunas no código conforme necessário

4. **Exemplos de adaptação**

   Suponha um novo dataset com colunas: `name`, `category`, `price`, `rating`
   
   - Altere o filtro:
   ```python
   filtro = st.sidebar.selectbox("Escolha a categoria:", ["Todos"] + df['category'].unique().tolist())
   if filtro == "Todos":
       df_filtrado = df
   else:
       df_filtrado = df[df['category'] == filtro]
   ```

   - Altere o gráfico:
   ```python
   fig, ax = plt.subplots(figsize=(10, 6))
   ax.bar(df_filtrado['name'], df_filtrado['price'], color='#4CAF50')
   ax.set_xlabel("Produto")
   ax.set_ylabel("Preço")
   plt.xticks(rotation=45, ha='right')
   plt.tight_layout()
   st.pyplot(fig)
   ```

   - Altere as estatísticas:
   ```python
   st.subheader("Estatísticas")
   col1, col2, col3 = st.columns(3)
   col1.metric("Preço Médio", f"R$ {df_filtrado['price'].mean():.2f}")
   col2.metric("Preço Mínimo", f"R$ {df_filtrado['price'].min():.2f}")
   col3.metric("Quantidade de Itens", len(df_filtrado))
   ```

## Estrutura do Projeto

```
/
├── README.md           # Este arquivo
├── app.py              # Aplicação Streamlit
├── dataset.csv         # Arquivo de dados
└── requirements.txt    # Dependências do projeto
```

## Tecnologias Utilizadas

- **Streamlit**: Framework para criação de aplicações web em Python
- **Pandas**: Biblioteca para manipulação e análise de dados
- **Matplotlib**: Biblioteca para criação de visualizações gráficas

## Referências

- Documentação Streamlit: https://docs.streamlit.io/
- Documentação Pandas: https://pandas.pydata.org/docs/
- Kaggle Datasets: https://www.kaggle.com/datasets
