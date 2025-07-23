
---

### 🧱 Componentes

#### 1. Interface de Usuário (Streamlit)
- Navegação por abas: upload, regras, risco, IA, dashboard e exportações.
- Filtros por período, centro de custo, tipo de material, etc.

#### 2. Conexão com Teradata
- Autenticação via `st.secrets`
- Obtenção de:
  - Pedidos de Compra (PO)
  - MIGO / MIRO
  - Dados de aprovadores/autorizadores
  - Base de materiais e contratos

#### 3. Engine de Regras de Auditoria
Aplica automaticamente:
- Duplicidade de pedidos
- Segregação de funções (SoD)
- Alçada de aprovação
- Valor fora da média
- Pagamento sem MIGO/MIRO

Gera colunas `flag_<regra>` para facilitar análise.

#### 4. Classificação de Risco
- Classificação dos materiais (estratégico, consumo, etc)
- Score ponderado por regra e tipo de item
- Faixa final de risco: **Baixo**, **Médio**, **Alto**

#### 5. Agentes de IA (OpenAI GPT-4o)
- **Agente de Red Flags**: avalia os riscos e explica os motivos
- **Agente Consultor**: gera planos de ação específicos por follow-up
- Exportação dos resultados em `.docx`

#### 6. Dashboard
- Gráficos interativos com Plotly
- Visão temporal, por tipo de risco, centro de custo, etc.

#### 7. Exportação
- Excel com filtros e colunas adicionais
- Word com sumário executivo e planos de ação

---

## 🧠 Tecnologias Utilizadas

| Tecnologia | Função |
|------------|--------|
| **Python** | Backend principal |
| **Streamlit** | Interface web |
| **OpenAI API (GPT-4o)** | IA para análise e plano de ação |
| **Teradata** | Base de dados |
| **Pandas / Numpy** | Manipulação de dados |
| **Plotly** | Visualização |
| **Python-docx / openpyxl** | Exportações |

---

## 🚀 Como Executar Localmente

```bash
# 1. Clone o repositório
git clone https://github.com/SEU-USUARIO/agente-compras.git
cd agente-compras

# 2. Crie um ambiente virtual
python -m venv .venv
source .venv/bin/activate  # Windows: .venv\Scripts\activate

# 3. Instale as dependências
pip install -r requirements.txt

# 4. Configure o arquivo .env ou st.secrets.toml com as credenciais da OpenAI e Teradata

# 5. Execute o app
streamlit run app.py
