## AIR PUC ✈️

Sistema de compra de passagens aéreas com administração de voos, trechos, aeronaves e assentos, e interface de busca/seleção para usuários.

### 🔧 Tecnologias
- **Frontend**: HTML, CSS, JavaScript (arquivos estáticos)
- **Backend**: Node.js + Express com **TypeScript**
- **Banco de dados**: Oracle (usando `oracledb`)

### 📁 Estrutura do projeto
```
AIR-PUC/
  backend/                 # API Node/TypeScript + scripts SQL
    src/                   # Código-fonte (Express + oracledb)
    script_pi.sql          # Criação do schema, sequências e triggers
  frontend/
    ADMIN/                 # Telas de administração (CRUDs)
    USER/                  # Telas do usuário (busca, assentos, pagamento)
    style/                 # CSS
    assets/                # Imagens
```

---

## 🚀 Funcionalidades
- **Passageiro**: busca de voos, seleção de assentos, compra
- **Admin**: CRUD de aeronaves, aeroportos, cidades, trechos e voos

---

## ✅ Pré‑requisitos
- Node.js 18+
- Oracle Database acessível (local ou cloud)

---

## ⚙️ Configuração do Backend
1) Instale dependências:
```bash
cd backend
npm install
```

2) Crie um arquivo `.env` dentro de `backend/` com suas credenciais Oracle:
```ini
ORACLE_DB_USER=seu_usuario
ORACLE_DB_PASSWORD=sua_senha
ORACLE_CONN_STR=host:porta/servicename
```
Essas variáveis são consumidas por `src/OracleConnAtribs.ts`.

3) (Opcional) Ajuste `tsconfig.json` se desejar alterar `outDir`/`rootDir`.

---

## 🗄️ Banco de Dados (Oracle)
O schema completo está em `backend/script_pi.sql` e inclui tabelas, sequences e triggers (ex.: geração automática de assentos ao criar um voo).

Para criar o schema, execute o script no seu cliente Oracle favorito:
```sql
-- dentro do seu client SQL
@/caminho/para/AIR-PUC/backend/script_pi.sql
```

Entidades principais:
- `CIDADES`, `AEROPORTOS`, `AERONAVES`, `TRECHOS`, `VOOS`, `ASSENTOS`, `PASSAGENS`

---

## ▶️ Executando o Backend
```bash
cd backend
npm start
```
O comando compila TypeScript e inicia o servidor Express (porta `3000`).

---

## 🌐 Endpoints da API
Base URL: `http://localhost:3000`

Leitura (GET/POST):
- `GET /listarTrechos`
- `GET /listarCidades`
- `GET /listarAeronaves`
- `GET /listarAeroportos`
- `GET /listarDados` (voos com dados agregados)
- `POST /listarBuscaVoos` — body `{ data, origem, destino }`
- `POST /listarAssentos` — body `{ voo }`

Criação (PUT):
- `PUT /inserirAeronave`
- `PUT /inserirAeroporto`
- `PUT /inserirTrecho`
- `PUT /inserirVoo`
- `PUT /inserirCidade`
- `PUT /inserirPassagem`

Atualização (PUT):
- `PUT /alterarAeronave`
- `PUT /alterarAeroporto`
- `PUT /alterarTrecho`
- `PUT /alterarVoo`
- `PUT /alterarCidade`
- `PUT /alterarAssento` (marca assento como ocupado)

Exclusão (DELETE):
- `DELETE /excluirVoo`
- `DELETE /excluirAeronave`
- `DELETE /excluirAeroporto`
- `DELETE /excluirTrecho`
- `DELETE /excluirCidade`

Observações:
- Todas as rotas retornam um objeto no formato `{ status, message, payload }` conforme `src/CustomResponse.ts`.
- A conexão Oracle utiliza `oracledb.OUT_FORMAT_OBJECT` para retornar objetos JS.

---

## 🖥️ Frontend
As telas são estáticas (HTML/CSS/JS) e podem ser abertas via um servidor estático (ex.: VS Code Live Server) ou servidas por qualquer HTTP server.

- Admin: `frontend/ADMIN/screens` — CRUDs de Aeronave, Aeroporto, Cidade, Trecho e Voo
- Usuário: `frontend/USER/screens` — `PrimeiraTela.html`, `BuscaVoo.html`, `Assentos.html`, `pagamento.html`

Para desenvolvimento, a forma mais simples é abrir a pasta `frontend/` com um servidor estático apontando para essa raiz. As páginas JS consomem a API `http://localhost:3000`.

---

## 🧭 Dicas & Solução de Problemas
- "Erro ao conectar ao oracle": valide as variáveis `.env`, rede/VPN e o `ORACLE_CONN_STR`.
- Ao criar um novo voo, os assentos são gerados automaticamente (trigger `TGR_ASSENTOS`).
- Após operações de escrita, a API efetua `commit()` explicitamente.
- Se alterar portas/URLs, ajuste as chamadas no JS do frontend.

---

## 📄 Licença
Projeto acadêmico. Uso educacional.

