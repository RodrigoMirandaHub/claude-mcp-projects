# 02 — MCP SQLite Server

## O que é
O MCP SQLite Server permite ao Claude criar tabelas, inserir dados, fazer
consultas e análises em um banco de dados local — tudo via linguagem natural,
sem escrever SQL manualmente.

---

## Configuração

### Pré-requisitos
- Claude Desktop instalado
- Python 3.12+

### Instalação

```bash
pip install mcp-server-sqlite
```

### Localizar o executável

```bash
where mcp-server-sqlite
```

Resultado esperado:
```
C:\Users\SeuUsuario\AppData\Local\Programs\Python\Python312\Scripts\mcp-server-sqlite.exe
```

### JSON de configuração

```json
"sqlite": {
  "command": "C:\\Users\\SeuUsuario\\AppData\\Local\\Programs\\Python\\Python312\\Scripts\\mcp-server-sqlite.exe",
  "args": [
    "--db-path",
    "C:\\Users\\SeuUsuario\\Desktop\\teste.db"
  ]
}
```

Substitua `SeuUsuario` pelo seu nome de usuário do Windows.

---

## Como verificar se está funcionando

1. Abrir Claude Desktop
2. Ir em **Configurações → Desenvolvedor**
3. O server `sqlite` deve aparecer com status **running** 🟢

---

## Exemplos de uso

### Criar tabela e inserir dados
```
Crie uma tabela chamada clientes com os campos: id, nome, email e cidade.
Depois insira 3 clientes fictícios.
```

### Consultar dados
```
Liste todos os clientes cadastrados
```

### Análise de dados
```
Qual cidade tem o maior valor? Me dá um resumo por cidade.
```

### Importar CSV para o banco
```
Leia o arquivo leads.csv que está no meu Desktop, crie uma tabela chamada
leads no banco de dados e importe todos os dados do CSV para essa tabela.
```

---

## Resultado do projeto CSV → SQLite

| # | Cidade | Total (R$) | Leads | Média (R$) |
|---|--------|-----------|-------|-----------|
| 1 | Salvador | 3.100 | 1 | 3.100 |
| 2 | São Paulo | 2.300 | 1 | 2.300 |
| 3 | Rio de Janeiro | 1.800 | 1 | 1.800 |
| 4 | Brasília | 1.500 | 1 | 1.500 |

Claude gerou queries SQL e análise completa via linguagem natural.

---

## O que é possível
- ✅ Criar tabelas e banco de dados do zero
- ✅ Inserir e atualizar dados via linguagem natural
- ✅ Fazer consultas SQL sem escrever SQL
- ✅ Importar CSVs automaticamente
- ✅ Análise e relatórios em tempo real
- ✅ Simular CRM, BI ou sistema de leads local

---

**Autor:** Rodrigo Miranda  
**GitHub:** github.com/RodrigoMirandaHub
