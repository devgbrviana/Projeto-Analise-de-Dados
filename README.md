# 🛡️ Análise de Dados de Chamados e Logs de Cibersegurança

## Introdução

Este projeto consiste em uma análise completa de dados de segurança da informação, com o objetivo de centralizar informações dispersas em diferentes fontes (registros de usuários, logs de chamados, logs de ataques e lista de vulnerabilidades) para identificar padrões, tendências e os principais riscos.

O principal foco é transformar dados brutos em *insights* acionáveis para a área de Cibersegurança e TI, culminando na criação de dashboards analíticos.

## 🎯 Objetivo

O objetivo central é:
* Consolidar dados heterogêneos para ter uma visão unificada dos incidentes.
* Realizar Análise Exploratória de Dados (EDA) para identificar a distribuição de chamados por origem e por usuário.
* Classificar e categorizar os incidentes para entender os tipos de ameaça mais recorrentes, como 'Ataque Cibernético' e 'Engenharia Social'.
* Gerar visualizações gráficas que destaquem os *Top Usuários* e os incidentes mais urgentes.

## 🛠️ Tecnologias e Ferramentas

O projeto utiliza as seguintes tecnologias:

* **Python:** Linguagem principal para ETL (Extração, Transformação e Carga) e EDA (Análise Exploratória de Dados).
    * **Bibliotecas:** `pandas`, `matplotlib`, `seaborn`, e `numpy`.
* **Jupyter Notebook (`Script_Projeto_Cyber.ipynb`):** Ambiente para desenvolvimento e documentação do pipeline de análise.
* **Power BI/DataViz:** Utilizado para criar o painel interativo final (`Projeto Cyber Segurança.pbix`).

## 📁 Estrutura do Repositório

| Arquivo/Pasta | Descrição |
| :--- | :--- |
| `Script_Projeto_Cyber.ipynb` | Contém todo o código Python para a limpeza, consolidação e análise exploratória dos dados. |
| `dados/` | Diretório hipotético para armazenar os arquivos de dados brutos e tratados. |
| `visualizacoes/` | Diretório para salvar imagens e dashboards (e.g., `Top5_Usuarios_por_Chamados.png`). |
| `Projeto Cyber Segurança.pbix` | Arquivo do projeto final de dashboard (Power BI). |
| `usuarios.txt` | Dados brutos de usuários e seus respectivos departamentos. |
| `chamados.csv` | Logs de chamados de segurança. |
| `logs.csv` | Logs de ataques e atividades de rede. |
| `vulnerabilidades.txt` | Registros de vulnerabilidades descobertas nos sistemas. |
| `Chamados_Consolidados.xlsx` | Resultado final da união e tratamento dos dados de chamados e logs, incluindo a coluna **Categoria**. |

## 📊 Fontes de Dados

O projeto integrou informações de quatro fontes principais:

1.  **Dados de Usuários (`usuarios.txt`):** Contém `id_usuario`, `nome`, e `departamento`.
2.  **Logs de Chamados (`chamados.csv` / `Ofense.xlsx`):** Registros de incidentes internos, incluindo `id_chamado`, `id_usuario`, `data_abertura`, e `tipo_incidente`.
3.  **Logs de Segurança (`logs.csv`):** Registros de ataques, com `data_hora`, `ip_origem`, `pais_origem`, e `tipo_ataque`.
4.  **Vulnerabilidades (`vulnerabilidades.txt`):** Detalhes sobre falhas em sistemas, como `sistema`, `descricao`, `severidade`, e `data_descoberta`.

## ⚙️ Pipeline de Análise

O processo de análise foi estruturado em quatro grandes etapas, conforme documentado no `Script_Projeto_Cyber.ipynb` e no arquivo de documentação:

### 1. Preparação e Consolidação dos Dados (Aula 2)

* **Leitura e Padronização:** Importação dos arquivos CSV/Excel e renomeação de colunas para facilitar a unificação.
* **Tratamento de Datas:** Conversão do campo `Abertura` (ou `data_abertura`) para o tipo `datetime`.
* **Unificação de Dados:** Realização de um `merge` (junção) entre os diferentes DataFrames (`df_chamados` e `df_ofense`/`df_consolidado`) para criar uma única fonte de dados.
* **Tratamento de Logs:** Padronização da coluna `pais_origem` nos logs de ataque, corrigindo variações como 'Br' e 'Estados Unidos' para 'Brasil' e 'EUA', respectivamente.

### 2. Análise Exploratória (Aula 3)

* **Criação de Categorias:** Implementação de um dicionário de mapeamento para agrupar os diversos `Tipo_Incidente` em categorias de alto nível, como:
    * `Acesso Nao Autorizado` -> `Acesso Indevido`
    * `Tentativa de Invasao` -> `Ataque Cibernetico`
    * `Phishing` -> `Engenharia Social`
    * `Malware` -> `Software Malicioso`
    * `Desbloqueio`, `Manutenção em Grupo`, `Permissionamento` -> `Inclusão de Acesso`
* **Exploração Inicial:** Contagem de chamados por `Origem` e por `Codigo_Usuario`.

### 3. Visualização e DataViz (Aulas 4, 5 e 6)

* **Análise por Período:** Visualização da quantidade de chamados abertos ao longo do tempo (por dia e por mês).
* **Análise por Categoria:** Distribuição total dos incidentes por `Categoria`.
* **Top Usuários:** Identificação e visualização dos 5 usuários que mais abriram chamados, detalhando as categorias de incidentes que eles reportaram.

## 🖼️ Principais Resultados

O gráfico abaixo, gerado durante a análise, exemplifica a capacidade de identificar os usuários de alto risco e o tipo de problema que mais os afeta:

![Gráfico Top 5 Usuários por Chamados](devgbrviana/projeto-analise-de-dados/Projeto-Analise-de-Dados-fb18bbcdd5d05a6131f7a4556f7a226c9bdd43a6/Top5_Usuarios_por_Chamados.png)

* O **Usuário 4** é o que mais abriu chamados (26 no total) e concentra a maioria dos incidentes de 'Acesso Indevido'.
* O **Usuário 11** possui o maior volume de chamados de 'Inclusão de Acesso' (cerca de 18), possivelmente indicando a necessidade de revisão de permissões ou processos de suporte.

## 🔑 Como Iniciar

1.  **Clone o repositório:**
    ```bash
    git clone [URL_DO_SEU_REPOSITORIO]
    ```
2.  **Instale as dependências (se ainda não as tiver):**
    ```bash
    pip install pandas matplotlib seaborn numpy
    ```
3.  **Execute o Notebook:** Abra o arquivo `Script_Projeto_Cyber.ipynb` em um ambiente Jupyter e execute as células sequencialmente para replicar a análise.
4.  **Visualize o Dashboard:** Abra o arquivo `Projeto Cyber Segurança.pbix` no Power BI Desktop para interagir com os resultados finais.
