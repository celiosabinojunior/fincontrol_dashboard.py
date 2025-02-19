import streamlit as st
import pandas as pd
import matplotlib.pyplot as plt

# Dados fictícios de exemplo
data = {
    'Categoria': ['Alimentação', 'Transporte', 'Lazer', 'Saúde', 'Moradia', 'Educação'],
    'Despesa': [500, 300, 200, 150, 1000, 400],
    'Receita': [2000, 2000, 2000, 2000, 2000, 2000]
}

df = pd.DataFrame(data)

# Título do dashboard
st.title('Dashboard de Controle Financeiro - FinControl')

# Exibição das receitas e despesas
st.header('Resumo Financeiro')

total_despesas = df['Despesa'].sum()
total_receitas = df['Receita'].sum()

st.write(f'Total de Despesas: R$ {total_despesas}')
st.write(f'Total de Receitas: R$ {total_receitas}')
st.write(f'Saldo: R$ {total_receitas - total_despesas}')

# Gráfico de despesas por categoria
st.header('Gráfico de Despesas por Categoria')
fig, ax = plt.subplots()
ax.bar(df['Categoria'], df['Despesa'])
ax.set_xlabel('Categoria')
ax.set_ylabel('Valor (R$)')
st.pyplot(fig)

# Metas de Investimento (exemplo simples)
st.header('Metas de Investimento')
investimento_objetivo = st.number_input('Defina seu valor objetivo de investimento:', min_value=100, value=1000)
investido_ate_agora = st.number_input('Valor já investido:', min_value=0, value=500)

st.write(f'Seu progresso até o momento: {investido_ate_agora}/{investimento_objetivo}')

# Barra de progresso
st.progress(investido_ate_agora / investimento_objetivo)

# Detalhamento das entradas e saídas
st.header('Detalhamento de Entradas e Saídas')
st.write(df)

# Função para exportação de dados (futuramente implementada)
# Caso queira salvar os dados para exportar em Excel ou PDF
st.header('Exportar Relatório')
exportar = st.button('Exportar Relatório como CSV')

if exportar:
    df.to_csv('relatorio_fincontrol.csv', index=False)
    st.success('Relatório exportado com sucesso!')

