# Sistema de Gestão de Campeonatos de Futebol

Este repositório contém a implementação de um sistema de banco de dados para gestão de campeonatos de futebol, desenvolvido como parte de um trabalho acadêmico. O projeto consiste em um estudo comparativo de modelagem de dados, apresentando uma implementação completa em **SQL (Relacional)** e diversos cenários de migração e modelagem em **NoSQL (MongoDB)**.

## Estrutura do Projeto

O projeto está organizado em três módulos principais:

```bash
├── 📁 Projeto Conceitual    # Modelagem Teórica
│   ├── Diagrama_mer.jpg     # Modelo Entidade-Relacionamento (MER)
│   └── Lógico.pdf           # Modelo Lógico Relacional e Dicionário de Dados
│
├── 📁 sql                   # Implementação Relacional (SQLite)
│   ├── criacao_das_tabelas.py  # DDL: Schema e Constraints
│   ├── dados1.py               # DML: Carga inicial de dados
│   ├── dados2.py               # DML: Carga massiva para testes de performance/queries
│   └── consultas.py            # DQL: Relatórios e Consultas Complexas
│
└── 📁 MongoDB               # Implementação NoSQL (PyMongo)
    ├── Bernardo.py          # Modelagem Temporal (Datas x Campeonatos)
    ├── mongo.py (Lucas)     # Auto-relacionamento (Clube x Rival)
    ├── projeto.py (Marcos)  # Relacionamento 1:N (Clube x Jogadores - PE)
    ├── projeto_rafael.py    # Entidade Associativa/Eventos (Gols e Assistências)
    └── 📁 Theo              # Relacionamento 1:N (Clube x Jogadores - RJ/SP)
        ├── 1referencia.py
        ├── 2embutido.py
        ├── 3array.py
        └── 4docembdoc.py

```

---

## Parte 1: Banco de Dados Relacional (SQL)

A implementação relacional foi feita utilizando **SQLite** e **Python**. O modelo destaca-se pelo uso de conceitos avançados de modelagem:

* **Herança/Generalização:** Implementação da superclasse `Pessoa` especializada em `Jogador`, `Técnico`, `Árbitro` e `Presidente`.
* **Entidade Fraca:** A tabela `Súmula` depende estritamente da `Partida`.
* **Relacionamentos Complexos:**
** Histórico de Clubes (`Clubes_anteriores`).
** Patrocínio vinculado à participação no campeonato (`Patrocinado`).


* **Consultas Implementadas (`consultas.py`):**
** Junções (Inner, Left Outer).
** Subconsultas (Escalar, Linha e Tabela).
** Operações de Conjunto (Union).
** Semi-Join e Anti-Join (via `EXISTS` / `NOT EXISTS`).



---

## Parte 2: Banco de Dados NoSQL (MongoDB)

Para a etapa NoSQL, a equipe implementou **4 cenários de modelagem** distintos para atender aos requisitos acadêmicos, comparando estratégias de **Referência (Normalização)** versus **Embutimento (Desnormalização)**.

Cada integrante ficou responsável por modelar um aspecto específico do domínio:

### 1. **Bernardo**

* **Foco:** Datas e Campeonatos.
* **Objetivo:** Analisar como armazenar calendários esportivos.
* **Cenários:** Comparou referenciar datas em campeonatos versus embutir o calendário completo no documento do campeonato.

### 2. **Lucas**

* **Foco:** Rivalidade (Clube x Clube).
* **Objetivo:** Resolver um auto-relacionamento N:N sem tabela associativa.
* **Destaque:** Utilização de Arrays de Referências para listar rivais (ex: Sport x Náutico x Santa Cruz).

### 3. **Marcos**

* **Foco:** Clube e Jogadores (Dados de Pernambuco).
* **Objetivo:** Modelagem 1:N.
* **Destaque:** Testes com dados locais (Sport, Náutico, Santa Cruz) e ídolos (Diego Souza, Magrão).

### 4. **Rafael**

* **Foco:** Gols, Autores e Assistências.
* **Objetivo:** Modelar eventos de partida.
* **Destaque:** Tratamento de *Extended Reference* (duplicar nome/posição do autor no gol para leitura rápida) e aninhamento de detalhes do gol.

### 5. **Theo**

* **Foco:** Clube e Jogadores (Dados do Eixo Rio-SP).
* **Objetivo:** Implementação didática dos 4 padrões fundamentais.
* `1referencia.py`: Jogador aponta para Clube (SQL-like).
* `2embutido.py`: Jogador contém dados do Clube (Leitura rápida).
* `3array.py`: Clube contém lista de IDs dos Jogadores (Parent Referencing).
* `4docembdoc.py`: Clube contém lista de documentos dos Jogadores (Parent Embedding).



---

## Como Executar

### Pré-requisitos

* Python 3.x
* MongoDB (Rodando localmente na porta `27017`)
* Bibliotecas Python:
```bash
pip install pymongo

```


*(O SQLite já é nativo do Python)*

### Executando o SQL

Para recriar o banco e rodar as consultas:

```bash
cd sql
python criacao_das_tabelas.py
python dados1.py
python dados2.py  # Popula com massa de dados histórica
python consultas.py

```

### Executando os Cenários NoSQL

Cada script é independente e limpa suas próprias coleções antes de rodar. Exemplo:

```bash
cd MongoDB
python projeto_rafael.py
# Siga o menu interativo no terminal para escolher o cenário (1-4)

```

---

## Autores

Trabalho desenvolvido pela equipe:

* **Bernardo Siqueira Batista**
* **Lucas de Morais Malheiro Tavares**
* **Marcos Antonio de Queiroz Veiga Neto**
* **Rafael Mendes Bezerra Xavier**
* **Theo Gusmão Simões Barza**
