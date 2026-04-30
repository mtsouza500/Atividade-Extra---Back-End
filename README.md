# 🐍🐘 PostgreSQL + SQLAlchemy + Alembic com Docker

Projeto de exemplo com configuração completa de banco de dados PostgreSQL via Docker, mapeamento de tabelas com SQLAlchemy e controle de migrations com Alembic.

---

## 📁 Estrutura do Projeto

```
meu_projeto/
├── docker-compose.yml      # Container PostgreSQL
├── requirements.txt        # Dependências Python
├── .gitignore
├── models.py               # Modelos/tabelas SQLAlchemy
├── alembic.ini             # Configuração do Alembic
└── alembic/
    ├── env.py              # Ambiente do Alembic (configurado)
    ├── script.py.mako      # Template de migration
    └── versions/           # Migrations geradas
```

---

## 🚀 Passo a passo

### 1. Subir o banco de dados

```bash
docker-compose up -d
```

Verificar se está rodando:

```bash
docker ps
```

---

### 2. Criar ambiente virtual e instalar dependências

```bash
python -m venv venv
source venv/bin/activate      # Linux/Mac
venv\Scripts\activate         # Windows

pip install -r requirements.txt
```

---

### 3. Gerar a migration e aplicar no banco

> O `alembic.ini` e o `alembic/env.py` já estão configurados para conectar no banco do Docker.

Gerar migration a partir dos models:

```bash
alembic revision --autogenerate -m "cria tabela usuarios"
```

Aplicar no banco:

```bash
alembic upgrade head
```

---

## 🗃️ Configurações do Banco

| Parâmetro  | Valor       |
|------------|-------------|
| Host       | localhost   |
| Porta      | 5432        |
| Usuário    | admin       |
| Senha      | admin123    |
| Banco      | meu_banco   |

---

## 🛠️ Comandos úteis do Alembic

```bash
alembic current        # Versão aplicada atualmente
alembic history        # Histórico de migrations
alembic downgrade -1   # Desfaz a última migration
alembic downgrade base # Desfaz TODAS as migrations
alembic upgrade head   # Aplica todas as migrations pendentes
```

---

## 📦 Dependências

| Biblioteca        | Versão  | Finalidade                    |
|-------------------|---------|-------------------------------|
| sqlalchemy        | 2.0.30  | ORM / mapeamento de tabelas   |
| alembic           | 1.13.1  | Controle de migrations        |
| psycopg2-binary   | 2.9.9   | Driver PostgreSQL para Python |
| python-dotenv     | 1.0.1   | Leitura de variáveis `.env`   |
