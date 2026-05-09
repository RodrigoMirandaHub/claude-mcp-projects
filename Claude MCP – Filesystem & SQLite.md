# Claude MCP – Filesystem & SQLite
**Autor:** Rodrigo Miranda  
**GitHub:** github.com/RodrigoMirandaHub  
**LinkedIn:** linkedin.com/in/rodrigo-h-miranda

---

## O que é MCP?

**Model Context Protocol (MCP)** é um protocolo criado pela Anthropic que permite ao Claude se conectar a ferramentas e dados externos de forma padronizada. É como uma "tomada universal" — qualquer ferramenta que fale MCP pode ser plugada diretamente no Claude Desktop.

---

## Ferramentas configuradas

| Server | Função |
|--------|--------|
| `filesystem` | Acesso a arquivos locais via npx |
| `sqlite` | Banco de dados local via Python |

---

## Pré-requisitos

- [Claude Desktop](https://claude.ai/download)
- [Node.js v20+](https://nodejs.org)
- [Python 3.12+](https://python.org)

---

## Instalação

### 1. Instalar o MCP server de SQLite

```bash
pip install mcp-server-sqlite
```

### 2. Localizar o arquivo de configuração

Abrir no Claude Desktop:  
**Configurações → Desenvolvedor → Editar Config**

Caminho no Windows:
```
C:\Users\SeuUsuario\AppData\Local\Packages\Claude_xxx\LocalCache\Roaming\Claude\claude_desktop_config.json
```

### 3. Configurar os MCP servers

```json
{
  "mcpServers": {
    "filesystem": {
      "command": "npx",
      "args": [
        "-y",
        "@modelcontextprotocol/server-filesystem",
        "C:\\Users\\SeuUsuario\\Desktop"
      ]
    },
    "sqlite": {
      "command": "C:\\Users\\SeuUsuario\\AppData\\Local\\Programs\\Python\\Python312\\Scripts\\mcp-server-sqlite.exe",
      "args": [
        "--db-path",
        "C:\\Users\\SeuUsuario\\Desktop\\teste.db"
      ]
    }
  }
}
```

### 4. Reiniciar o Claude Desktop

- Fechar pelo ícone na **bandeja do sistema** (canto inferior direito)
- Abrir novamente
- Verificar em **Configurações → Desenvolvedor**
- Ambos devem aparecer com status: **running** 🟢

---

## Projeto 1 — Leitura de arquivos via filesystem

**Prompt usado:**
```
Liste os arquivos que estão no meu Desktop
```

**Resultado:** Claude listou todos os arquivos do Desktop via MCP filesystem em tempo real.

---

## Projeto 2 — Criação de banco de dados SQLite

**Prompt usado:**
```
Crie uma tabela chamada clientes com os campos: id, nome, email e cidade.
Depois insira 3 clientes fictícios.
```

**Resultado:** Claude criou a tabela e inseriu os dados diretamente no `teste.db` — sem nenhuma linha de SQL manual.

| id | nome | email | cidade |
|----|------|-------|--------|
| 1 | Ana Paula Souza | ana.souza@email.com | São Paulo |
| 2 | Carlos Mendes | carlos.mendes@email.com | Belo Horizonte |
| 3 | Fernanda Lima | fernanda.lima@email.com | Curitiba |

---

## Projeto 3 — Importação de CSV para SQLite

**Arquivo `leads.csv` criado:**
```csv
nome,email,cidade,valor
João Silva,joao@email.com,Brasília,1500
Maria Costa,maria@email.com,São Paulo,2300
Pedro Alves,pedro@email.com,Rio de Janeiro,1800
Lucia Ferreira,lucia@email.com,Salvador,3100
```

**Prompt usado:**
```
Leia o arquivo leads.csv que está no meu Desktop, crie uma tabela chamada
leads no banco de dados e importe todos os dados do CSV para essa tabela.
```

**Resultado:** Claude usou `filesystem` para ler o CSV e `sqlite` para importar os dados automaticamente — pipeline completo sem código.

---

## Projeto 4 — Análise de dados em linguagem natural

**Prompt usado:**
```
Qual cidade tem o maior valor? Me dá um resumo por cidade.
```

**Resultado:**

| # | Cidade | Total (R$) | Leads | Média (R$) |
|---|--------|-----------|-------|-----------|
| 1 | Salvador | 3.100 | 1 | 3.100 |
| 2 | São Paulo | 2.300 | 1 | 2.300 |
| 3 | Rio de Janeiro | 1.800 | 1 | 1.800 |
| 4 | Brasília | 1.500 | 1 | 1.500 |

Claude gerou queries SQL e análise completa via linguagem natural.

---

## O que é possível com filesystem + SQLite via MCP

- ✅ Ler e criar arquivos no computador via linguagem natural
- ✅ Criar e consultar bancos de dados sem escrever SQL
- ✅ Importar CSVs automaticamente para banco de dados
- ✅ Fazer análises de dados em tempo real
- ✅ Combinar as duas ferramentas em pipelines completos
- ✅ Simular mini CRM, BI ou sistema de leads local
