# 03 — MCP Google Sheets Server

Pipeline completo: Claude lê dados do SQLite e exporta automaticamente
para o Google Sheets via MCP — sem escrever uma linha de código.

---

## O que é
O MCP Google Sheets Server permite ao Claude ler, criar e editar planilhas
do Google Sheets diretamente via linguagem natural, usando autenticação OAuth.

---

## Pré-requisitos
- Claude Desktop instalado
- Python 3.12+
- Conta Google com acesso ao Google Cloud Console

---

## Passo 1 — Ativar a API do Google Sheets

1. Acesse https://console.cloud.google.com
2. Selecione ou crie um projeto
3. Vá em **APIs e serviços → Biblioteca**
4. Pesquise **Google Sheets API** e clique em **Ativar**

---

## Passo 2 — Criar credenciais OAuth

1. Vá em **APIs e serviços → Credenciais**
2. Clique em **+ Criar credenciais → ID do cliente OAuth**
3. Tipo de aplicativo: **App para computador**
4. Nome: `claude-mcp-sheets`
5. Clique em **Criar** e depois **Fazer download do JSON**
6. Crie uma pasta para as credenciais:

```
mkdir C:\Users\SeuUsuario\Documents\mcp-credentials
```

7. Mova o arquivo JSON baixado para essa pasta e renomeie para `credentials.json`

---

## Passo 3 — Instalar o MCP server

```bash
pip install mcp-google-sheets
```

Verificar onde foi instalado:

```bash
where mcp-google-sheets
```

Resultado esperado:
```
C:\Users\SeuUsuario\AppData\Local\Programs\Python\Python312\Scripts\mcp-google-sheets.exe
```

---

## Passo 4 — Autenticar com o Google (primeira vez)

Navegue até a pasta de credenciais e rode o servidor:

```bash
cd C:\Users\SeuUsuario\Documents\mcp-credentials
mcp-google-sheets --credentials credentials.json
```

Uma janela do navegador vai abrir pedindo autorização. Após autorizar, o terminal vai mostrar:

```
Successfully authenticated using OAuth flow
```

Isso cria um arquivo `token.json` na pasta — guarde-o, ele evita precisar autenticar de novo.

---

## Passo 5 — Corrigir bug de prints no pacote

O pacote `mcp-google-sheets` tem um bug: ele imprime texto no stdout durante
a autenticação, o que quebra o protocolo JSON do MCP.

Solução: substituir o arquivo `server.py` do pacote pela versão corrigida
(sem os prints que interferem na comunicação).

Caminho do arquivo original:
```
C:\Users\SeuUsuario\AppData\Local\Programs\Python\Python312\Lib\site-packages\mcp_google_sheets\server.py
```

---

## Passo 6 — Configurar o Claude Desktop

Abrir o arquivo de configuração em:
**Claude Desktop → Configurações → Desenvolvedor → Editar Config**

Adicionar o bloco do google-sheets:

```json
"google-sheets": {
  "command": "C:\\Users\\SeuUsuario\\AppData\\Local\\Programs\\Python\\Python312\\Scripts\\mcp-google-sheets.exe",
  "args": [
    "--credentials",
    "credentials.json"
  ],
  "env": {
    "TOKEN_PATH": "C:\\Users\\SeuUsuario\\Documents\\mcp-credentials\\token.json",
    "CREDENTIALS_PATH": "C:\\Users\\SeuUsuario\\Documents\\mcp-credentials\\credentials.json"
  },
  "cwd": "C:\\Users\\SeuUsuario\\Documents\\mcp-credentials"
}
```

Substituir `SeuUsuario` pelo nome de usuário do Windows.

---

## Passo 7 — Verificar se está funcionando

1. Fechar o Claude Desktop pela bandeja do sistema
2. Abrir novamente
3. Ir em **Configurações → Desenvolvedor**
4. O server `google-sheets` deve aparecer com status **running** 🟢

---

## Projeto — Pipeline SQLite → Google Sheets

### O que foi feito
Claude leu os dados da tabela `leads` no banco SQLite local e exportou
automaticamente para uma planilha do Google Sheets — usando 3 ferramentas
MCP ao mesmo tempo.

### Prompt usado
```
Na planilha [ID], insira os dados dos leads que estão no banco de dados
SQLite na tabela leads
```

### Resultado na planilha

| id | nome | email | cidade | valor |
|----|------|-------|--------|-------|
| 1 | João Silva | joao@email.com | Brasília | 1500 |
| 2 | Maria Costa | maria@email.com | São Paulo | 2300 |
| 3 | Pedro Alves | pedro@email.com | Rio de Janeiro | 1800 |
| 4 | Lucia Ferreira | lucia@email.com | Salvador | 3100 |

### As 3 ferramentas trabalhando juntas
```
SQLite (leitura) → Claude (processamento) → Google Sheets (escrita)
```

---

## Outros exemplos de uso

### Listar planilhas
```
Liste todas as planilhas no meu Google Drive
```

### Ler dados de uma planilha
```
Leia os dados da planilha [ID] e me mostre um resumo
```

### Criar nova planilha
```
Crie uma nova planilha chamada "Relatório de Vendas"
```

### Analisar e exportar
```
Analise os dados de vendas do SQLite e crie um relatório
na planilha [ID] com totais por cidade
```

---

## O que é possível com Google Sheets via MCP
- ✅ Ler e escrever dados em planilhas
- ✅ Criar novas planilhas e abas
- ✅ Importar dados do SQLite para Sheets automaticamente
- ✅ Gerar relatórios e análises em linguagem natural
- ✅ Pipeline completo: banco de dados → planilha → análise
- ✅ Integrar com filesystem para exportar CSVs também

---

**Autor:** Rodrigo Miranda
**GitHub:** github.com/RodrigoMirandaHub
**LinkedIn:** linkedin.com/in/rodrigo-h-miranda
