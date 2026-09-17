# AulaSempre — Banco de Dados MySQL 8.x

Repositório oficial da modelagem e scripts do banco de dados da plataforma **AulaSempre** (Sistema Inteligente de Substituição de Professores).

---

## 📁 Estrutura do Projeto

```text
aulasempre/
├── .github/
│   └── workflows/
│       └── test-database.yml   # CI/CD: Validação automática do banco no GitHub
├── aulasempre.sql              # Script SQL completo (DDL + DML + DQL)
├── docker-compose.yml          # Ambiente MySQL pronto para rodar via Docker
└── README.md                   # Documentação do projeto
```

---

## 🚀 Como Rodar Localmente

### Opção 1: No MySQL Workbench (Interface Gráfica)

1. Abra o **MySQL Workbench** e conecte-se à sua instância local do MySQL.
2. No menu superior, clique em **File → Open SQL Script...** (ou pressione `Ctrl + Shift + O`).
3. Selecione o arquivo [`aulasempre.sql`](./aulasempre.sql).
4. Clique no ícone do **Raio** no canto superior esquerdo (ou tecle `Ctrl + Shift + Enter`) para executar todo o script.
5. Na barra lateral esquerda (**Schemas**), clique com o botão direito e escolha **Refresh All**. Você verá o schema `aulasempre` com todas as 13 tabelas criadas e populadas.
6. **Para ver o Diagrama ER**:
   - Vá em **Database → Reverse Engineer...** (`Ctrl + R`).
   - Siga o assistente, selecione o banco `aulasempre` e conclua.
   - O diagrama interativo com todas as tabelas e relacionamentos será gerado automaticamente.

---

### Opção 2: Via Docker (Sem precisar instalar MySQL na máquina)

Se você tem o **Docker Desktop** instalado:

1. Abra o terminal na pasta do projeto e execute:
   ```bash
   docker compose up -d
   ```
2. O container iniciará e executará automaticamente o script `aulasempre.sql` no primeiro carregamento.
3. Para conectar pelo MySQL Workbench ou API:
   - **Host:** `localhost`
   - **Porta:** `3306`
   - **Usuário:** `root`
   - **Senha:** `root`
   - **Database:** `aulasempre`
4. Para parar o container:
   ```bash
   docker compose down
   ```

---

### Opção 3: Via Terminal / Prompt de Comando (MySQL CLI)

Se o cliente `mysql` estiver no seu PATH:

```bash
mysql -u root -p < aulasempre.sql
```

Digite sua senha e o script executará a criação, inserts e as consultas de teste.

---

## 🐙 Como Subir e Rodar no GitHub (CI/CD Automático)

Este repositório já inclui o arquivo [`.github/workflows/test-database.yml`](./.github/workflows/test-database.yml). Ele executa um container oficial do MySQL 8.0 no GitHub Actions a cada `push`, testando se o script roda sem erros.

### Passo a passo para criar o repositório no GitHub:

1. **Crie um novo repositório no GitHub**:
   - Acesse [github.com/new](https://github.com/new)
   - Nome do repositório: `aulasempre-db` (ou o nome de sua preferência)
   - Escolha **Público** ou **Privado**
   - **Não** marque a opção de adicionar README (já criamos os arquivos locais)
   - Clique em **Create repository**

2. **No terminal do seu computador (na pasta do projeto)**:
   ```bash
   git init
   git add .
   git commit -m "feat: banco de dados completo aulasempre com ci github actions"
   git branch -M main
   git remote add origin https://github.com/SEU_USUARIO/aulasempre-db.git
   git push -u origin main
   ```

3. **Verificando a execução no GitHub Actions**:
   - Abra a página do seu repositório no GitHub.
   - Clique na aba **Actions**.
   - Você verá o fluxo de trabalho **Test MySQL Database** sendo executado.
   - Clique nele para acompanhar a subida do container MySQL 8, execução do script SQL e validação das tabelas com selo verde de sucesso (✅).
