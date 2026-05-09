# 01 — MCP Filesystem Server

## O que é
O MCP Filesystem Server permite ao Claude acessar, ler e criar arquivos
diretamente no seu computador via linguagem natural.

---

## Configuração

### Pré-requisitos
- Claude Desktop instalado
- Node.js v20+

### JSON de configuração

```json
"filesystem": {
  "command": "npx",
  "args": [
    "-y",
    "@modelcontextprotocol/server-filesystem",
    "C:\\Users\\SeuUsuario\\Desktop"
  ]
}
```

Substitua `SeuUsuario` pelo seu nome de usuário do Windows.

---

## Como verificar se está funcionando

1. Abrir Claude Desktop
2. Ir em **Configurações → Desenvolvedor**
3. O server `filesystem` deve aparecer com status **running** 🟢

---

## Exemplos de uso

### Listar arquivos
```
Liste os arquivos que estão no meu Desktop
```

### Ler um arquivo
```
Leia o conteúdo do arquivo leads.csv no meu Desktop
```

### Criar um arquivo
```
Crie um arquivo chamado notas.txt no meu Desktop com o texto: "Primeiro arquivo via MCP"
```

---

## O que é possível
- ✅ Listar arquivos e pastas
- ✅ Ler conteúdo de arquivos (CSV, TXT, JSON, MD)
- ✅ Criar novos arquivos
- ✅ Editar arquivos existentes
- ✅ Base para pipelines com outros MCP servers

---

**Autor:** Rodrigo Miranda  
**GitHub:** github.com/RodrigoMirandaHub
