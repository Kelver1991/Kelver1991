# 🍽️ Raízes do Nordeste API

<div align="center">

![Python](https://img.shields.io/badge/Python-3.14-3776AB?style=flat-square&logo=python&logoColor=white)
![FastAPI](https://img.shields.io/badge/FastAPI-009688?style=flat-square&logo=fastapi&logoColor=white)
![MySQL](https://img.shields.io/badge/MySQL-8.0-4479A1?style=flat-square&logo=mysql&logoColor=white)
![JWT](https://img.shields.io/badge/JWT-Auth-000000?style=flat-square&logo=jsonwebtokens&logoColor=white)
![SQLAlchemy](https://img.shields.io/badge/SQLAlchemy-ORM-D71F00?style=flat-square&logo=python&logoColor=white)
![Swagger](https://img.shields.io/badge/Swagger-Docs-85EA2D?style=flat-square&logo=swagger&logoColor=black)
![Status](https://img.shields.io/badge/Status-Em%20desenvolvimento-yellow?style=flat-square)

**API REST completa para gestão de rede de restaurantes.**  
Autenticação JWT · Controle por perfil (RBAC) · Conformidade LGPD

</div>

---

## 📋 Sobre o projeto

Sistema back-end desenvolvido para a rede de restaurantes **Raízes do Nordeste**, com suporte a múltiplas unidades, gestão de produtos, pedidos multi-canal, controle de estoque, pagamentos e programa de fidelidade.

A API foi construída seguindo boas práticas de segurança, com autenticação via **JWT**, autorização por perfil (**RBAC**) e **consentimento LGPD** obrigatório no cadastro de usuários.

---

## 🚀 Tecnologias

| Categoria | Tecnologia |
|---|---|
| Linguagem | Python 3.14 |
| Framework | FastAPI |
| Banco de Dados | MySQL 8.0 |
| ORM | SQLAlchemy |
| Autenticação | JWT (python-jose) + bcrypt (Passlib) |
| Validação | Pydantic |
| Servidor | Uvicorn (ASGI) |
| Documentação | Swagger / OpenAPI 3.1 |
| Testes | Postman |
| Versionamento | Git / GitHub |

---

## 🔐 Autenticação & Autorização

O sistema utiliza autenticação stateless com **JWT** (expiração de 60 minutos) e controle de acesso baseado em perfis **(RBAC)**:

| Perfil | Descrição |
|---|---|
| `ADMIN` | Acesso total ao sistema |
| `GERENTE` | Gestão de unidades, produtos e relatórios |
| `COZINHA` | Visualização e atualização de pedidos |
| `ATENDENTE` | Criação de pedidos e atendimento |
| `CLIENTE` | Pedidos, pagamentos e fidelidade |

> ⚠️ O consentimento LGPD é obrigatório no cadastro de usuários.

---

## 📡 Endpoints

### 🔑 Autenticação
| Método | Rota | Descrição | Auth |
|---|---|---|---|
| `POST` | `/auth/registrar` | Cadastro de usuário | ❌ |
| `POST` | `/auth/login` | Login e geração de token | ❌ |
| `GET` | `/auth/perfil` | Dados do usuário logado | ✅ |

### 🏪 Unidades
| Método | Rota | Descrição | Auth |
|---|---|---|---|
| `GET` | `/unidades/` | Listar unidades | ❌ |
| `POST` | `/unidades/` | Criar unidade | ✅ |
| `GET` | `/unidades/{id}` | Buscar unidade | ❌ |
| `PUT` | `/unidades/{id}` | Atualizar unidade | ✅ |

### 🍽️ Produtos
| Método | Rota | Descrição | Auth |
|---|---|---|---|
| `POST` | `/produtos/` | Criar produto | ✅ |
| `GET` | `/produtos/` | Listar produtos | ❌ |
| `GET` | `/produtos/{id}` | Buscar produto | ❌ |
| `PUT` | `/produtos/{id}` | Atualizar produto | ✅ |
| `DELETE` | `/produtos/{id}` | Deletar produto | ✅ |

### 📦 Estoque
| Método | Rota | Descrição | Auth |
|---|---|---|---|
| `POST` | `/estoque/entrada` | Entrada de estoque | ✅ |
| `POST` | `/estoque/saida` | Saída de estoque | ✅ |
| `GET` | `/estoque/unidade/{unidade_id}` | Consultar estoque por unidade | ❌ |

### 📋 Pedidos
| Método | Rota | Descrição | Auth |
|---|---|---|---|
| `POST` | `/pedidos/` | Criar pedido | ✅ |
| `GET` | `/pedidos/` | Listar pedidos | ✅ |
| `GET` | `/pedidos/{id}` | Buscar pedido | ✅ |
| `PATCH` | `/pedidos/{id}/status` | Atualizar status | ✅ |
| `PATCH` | `/pedidos/{id}/cancelar` | Cancelar pedido | ✅ |

> Canais suportados: `APP` · `TOTEM` · `BALCÃO` · `PICKUP` · `WEB`

### 💳 Pagamentos
| Método | Rota | Descrição | Auth |
|---|---|---|---|
| `POST` | `/pagamentos/processar` | Processar pagamento | ✅ |
| `GET` | `/pagamentos/{pedido_id}` | Consultar pagamento | ✅ |

### ⭐ Fidelidade
| Método | Rota | Descrição | Auth |
|---|---|---|---|
| `GET` | `/fidelidade/saldo` | Consultar saldo de pontos | ✅ |
| `POST` | `/fidelidade/resgatar` | Resgatar pontos | ✅ |
| `GET` | `/fidelidade/admin/todos` | Listar todos (admin) | ✅ |

---

## ⚙️ Como executar localmente

### Pré-requisitos
- Python 3.14+
- MySQL 8.0+
- Git

### 1. Clone o repositório
```bash
git clone https://github.com/Kelver1991/raizes-do-nordeste.git
cd raizes-do-nordeste
```

### 2. Crie e ative o ambiente virtual
```bash
python -m venv venv

# Windows
venv\Scripts\activate

# Linux/Mac
source venv/bin/activate
```

### 3. Instale as dependências
```bash
pip install -r requirements.txt
```

### 4. Configure as variáveis de ambiente
Crie um arquivo `.env` na raiz do projeto:
```env
DATABASE_URL=mysql+pymysql://usuario:senha@localhost:3306/raizes_db
SECRET_KEY=sua_chave_secreta
ALGORITHM=HS256
ACCESS_TOKEN_EXPIRE_MINUTES=60
```

### 5. Execute o servidor
```bash
uvicorn app.main:app --reload
```

### 6. Acesse a documentação
```
http://localhost:8000/docs
```

---

## 📁 Estrutura do projeto

```
raizes-do-nordeste/
├── aplicativo/
│   ├── main.py
│   ├── database.py
│   ├── models/
│   ├── schemas/
│   ├── routers/
│   └── services/
├── postman_collection.json
├── .env.example
├── requirements.txt
└── README.md
```

---

## 👤 Autor

**Kelver Mendes**  
[![LinkedIn](https://img.shields.io/badge/LinkedIn-kelver--mendes-0077B5?style=flat-square&logo=linkedin&logoColor=white)](https://linkedin.com/in/kelver-mendes-51250930a)
[![Gmail](https://img.shields.io/badge/Gmail-kelvermendes1991@gmail.com-D14836?style=flat-square&logo=gmail&logoColor=white)](mailto:kelvermendes1991@gmail.com)

---

<div align="center">

*Projeto desenvolvido com foco em boas práticas de API REST, segurança e arquitetura escalável.*

</div>
