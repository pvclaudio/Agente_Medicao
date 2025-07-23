Agente de Compras - Auditoria Automatizada com IA
O Agente de Compras é um sistema completo de auditoria de pedidos de compras, desenvolvido com foco na detecção de fraudes, riscos operacionais e análise inteligente de compras corporativas. Utiliza Streamlit como interface, integração com banco Teradata e múltiplos agentes baseados em IA (via OpenAI GPT-4o), com suporte a análise de alçada, segregação de funções (SoD), valores fora da média, classificações de risco e muito mais.
________________________________________
📐 Arquitetura do Sistema
⚙️ Visão Geral
mermaid
CopiarEditar
graph TD
    A[Usuário via Web App] --> B[Streamlit Interface]
    B --> C[Carregamento de dados (Teradata)]
    B --> D[Aplicação de Regras de Auditoria]
    D --> E[Classificação de Risco]
    D --> F[Detecção de Fraudes com IA (GPT-4o)]
    E --> G[Dashboard Interativo]
    F --> G
    G --> H[Exportação Excel/Word]
________________________________________
🧱 Componentes
1. Interface de Usuário (Streamlit)
•	Menu lateral com navegação por páginas:
o	Upload e filtros
o	Regras de auditoria
o	Classificação de risco
o	Dashboard
o	Exportações
•	Upload opcional de arquivos locais
•	Filtros por período, centro de custo, tipo de material, etc.
2. Conexão com Teradata
•	Autenticação segura com caching de credenciais
•	Query dinâmica para obtenção dos dados:
o	Pedidos de Compra (PO)
o	Entradas MIGO/MIRO
o	Dados do autorizador/aprovador
o	Base de materiais e contratos
3. Engine de Regras de Auditoria
Aplicação automática das seguintes regras:
•	Duplicidade de pedidos (mesmo material, fornecedor e data)
•	Segregação de funções (SoD): autorizador = aprovador
•	Alçada de aprovação: valores acima da faixa aprovada
•	Valor fora da média: comparação com histórico
•	Pagamento sem MIGO ou MIRO
Cada regra gera uma coluna de flag_<nome_regra> no DataFrame.
4. Classificação de Risco
•	Categorização dos materiais (ex: estratégico, operacional, consumo)
•	Aplicação de pesos configuráveis
•	Score de risco total por pedido
•	Faixas de classificação: Baixo, Médio, Alto
5. Agentes de IA (OpenAI GPT-4o)
Dois agentes com prompts dedicados:
•	Agente de Análise de Red Flags
o	Justifica o motivo da marcação
o	Resume os principais riscos
o	Gera coluna de revisao_ia e motivo
•	Agente Consultor de Auditoria
o	Sugere plano de ação para os principais riscos
o	Utiliza frameworks (ex: COSO, COBIT, NIST) conforme o tipo de falha
o	Exporta o plano de ação em formato .docx
6. Dashboard
•	Visualizações com Plotly:
o	Distribuição por risco
o	Frequência de flags
o	Análise temporal
o	Heatmap de centros de custo
7. Exportação
•	Exportação dos resultados para:
o	Excel (com todas as colunas e filtros)
o	Word (com plano de ação da IA)

