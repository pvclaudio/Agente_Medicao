Agente de Compras - Auditoria Automatizada com IA
O Agente de Compras é um sistema completo de auditoria de pedidos de compras, desenvolvido com foco na detecção de fraudes, riscos operacionais e análise inteligente de compras corporativas. Utiliza Streamlit como interface, integração com banco Teradata e múltiplos agentes baseados em IA (via OpenAI GPT-4o), com suporte a análise de alçada, segregação de funções (SoD), valores fora da média, classificações de risco e muito mais.

 Arquitetura do Sistema
 Visão Geral
mermaid
Copiar
Editar
graph TD
    A[Usuário via Web App] --> B[Streamlit Interface]
    B --> C[Carregamento de dados (Teradata)]
    B --> D[Aplicação de Regras de Auditoria]
    D --> E[Classificação de Risco]
    D --> F[Detecção de Fraudes com IA (GPT-4o)]
    E --> G[Dashboard Interativo]
    F --> G
    G --> H[Exportação Excel/Word]
 Componentes
1. Interface de Usuário (Streamlit)
Menu lateral com navegação por páginas:

Upload e filtros

Regras de auditoria

Classificação de risco

Dashboard

Exportações

Upload opcional de arquivos locais

Filtros por período, centro de custo, tipo de material, etc.

2. Conexão com Teradata
Autenticação segura com caching de credenciais

Query dinâmica para obtenção dos dados:

Pedidos de Compra (PO)

Entradas MIGO/MIRO

Dados do autorizador/aprovador

Base de materiais e contratos

3. Engine de Regras de Auditoria
Aplicação automática das seguintes regras:

Duplicidade de pedidos (mesmo material, fornecedor e data)

Segregação de funções (SoD): autorizador = aprovador

Alçada de aprovação: valores acima da faixa aprovada

Valor fora da média: comparação com histórico

Pagamento sem MIGO ou MIRO

Cada regra gera uma coluna de flag_<nome_regra> no DataFrame.

4. Classificação de Risco
Categorização dos materiais (ex: estratégico, operacional, consumo)

Aplicação de pesos configuráveis

Score de risco total por pedido

Faixas de classificação: Baixo, Médio, Alto

5. Agentes de IA (OpenAI GPT-4o)
Dois agentes com prompts dedicados:

Agente de Análise de Red Flags

Justifica o motivo da marcação

Resume os principais riscos

Gera coluna de revisao_ia e motivo

Agente Consultor de Auditoria

Sugere plano de ação para os principais riscos

Utiliza frameworks (ex: COSO, COBIT, NIST) conforme o tipo de falha

Exporta o plano de ação em formato .docx

6. Dashboard
Visualizações com Plotly:

Distribuição por risco

Frequência de flags

Análise temporal

Heatmap de centros de custo

7. Exportação
Exportação dos resultados para:

Excel (com todas as colunas e filtros)

Word (com plano de ação da IA)


