# 📘 Guia de Entrevistas Técnicas — **README GIGANTE** (Markdown)

<div style="background:#FFDD48; border-radius:14px; padding:14px 16px; font-weight:700;">
⚡ Objetivo: um README único, bonito e organizado, para te deixar <u>100% preparado</u> para entrevistas técnicas — de <b>live coding</b> a <b>system design</b>, passando por <b>SQL/NoSQL/Supabase</b>, <b>segurança</b>, <b>redes</b>, <b>Git/CI</b>, <b>testes</b> e <b>comportamental</b>.  
Inclui checklists, playbooks, <b>tabela multi-banco completa</b>, snippets e planos de estudo (7/14/30 dias).
</div>

---

## 🗺️ Sumário

* [Como usar](#-como-usar)
* [Mapa de competências por senioridade](#-mapa-de-competências-por-senioridade)
* [Checklist — Entrevistas de Programação](#-checklist--entrevistas-de-programação)
* [Padrões de resolução (DSA Patterns)](#-padrões-de-resolução-dsa-patterns)
* [Banco de Dados — Guia prático (detalhado)](#-banco-de-dados--guia-prático-detalhado)
* [Banco de Dados — Tabela Multi-Banco COMPLETA](#-banco-de-dados--tabela-multi-banco-completa)
* [SQL avançado (CTE, Window, anti-join, pivot)](#-sql-avançado-cte-window-anti-join-pivot)
* [Supabase — Policies, Auth, Storage, Realtime, Edge](#-supabase--policies-auth-storage-realtime-edge)
* [APIs Web — Design, versionamento e erros](#-apis-web--design-versionamento-e-erros)
* [Segurança — OWASP e checklist prático](#-segurança--owasp-e-checklist-prático)
* [Sistemas Operacionais & Redes](#-sistemas-operacionais--redes)
* [Concorrência & Assíncrono](#-concorrência--assíncrono)
* [Design de Sistemas — Passo a passo + estimativas](#-design-de-sistemas--passo-a-passo--estimativas)
* [Observabilidade & Performance](#-observabilidade--performance)
* [Git & Fluxos de trabalho](#-git--fluxos-de-trabalho)
* [Testes (Pirâmide, mocks, E2E)](#-testes-pirâmide-mocks-e2e)
* [Front-end (React/Next.js) e Electron Desktop](#-front-end-reactnextjs-e-electron-desktop)
* [Playbook de Live Coding](#-playbook-de-live-coding)
* [Comportamental (STAR/CARL) + respostas modelo](#-comportamental-starcarl--respostas-modelo)
* [Perguntas para o entrevistador](#-perguntas-para-o-entrevistador)
* [Planos de estudo (7/14/30 dias)](#-planos-de-estudo-71430-dias)
* [Cheat sheets úteis (JS/TS/Python/Java)](#-cheat-sheets-úteis-jstspythonjava)
* [Checklist final (5 min antes)](#-checklist-final-5-min-antes)
* [Notas rápidas + Setup Supabase](#-notas-rápidas--setup-supabase)
* 🔥 **[Supabase SDK — JS/TS & Python (Recipes completas)](#-supabase-sdk--jsts--python-recipes-completas)**  ← (ADICIONADO)

---

## 🚀 Como usar

* Estude por **módulos** (🔸 e ▶) e pratique com **mini-projetos/snippets**.
* Use os **blocos amarelos** para lembrar pontos críticos.

<div style="background:#FFDD48; padding:8px 10px; border-radius:10px; font-weight:600;">
💡 Regra de ouro: não decore — entenda <i>por quê</i>, pratique <i>como</i>, explique <i>quando usar</i>.
</div>

---

## 🧭 Mapa de competências por senioridade

| Nível           | Dominar                                                                                  | Conhecer bem                                           | Articular                                    |
| --------------- | ---------------------------------------------------------------------------------------- | ------------------------------------------------------ | -------------------------------------------- |
| **Júnior**      | Sintaxe; DSA básicos (arrays/strings/hash/pilha/fila); HTTP básico; SQL CRUD; Git        | Testes de unidade; REST; Docker básico; cloud básica   | Trade-offs simples; comunicação clara        |
| **Pleno**       | DSA (árvores/grafos/heap/DP leve); SQL avançado (JOIN/CTE/Window); caching; filas; CI/CD | Observabilidade; OWASP; design de APIs; NoSQL          | Estimar custos/latência; justificar escolhas |
| **Sênior/Lead** | System design (consistência/particionamento/falhas); p95/p99; arquitetura                | Estratégias de dados; multi-região; migrações; RLS/IAM | Negócio + impacto; riscos e mitigação        |

---

## ✅ Checklist — Entrevistas de Programação

### 🧱 Fundamentos

* Tipos, variáveis, operadores; **imutabilidade** quando fizer sentido.
  `JS:` `const config = Object.freeze({...})` • `TS:` `readonly`
* Controle de fluxo: `if/else`, `switch`, `for/while`, `break/continue`.
* Funções: parâmetros/retorno, recursão, **funções puras** (mesma entrada → mesmo resultado).
* Erros: sintaxe × execução × lógica; `try/catch`, `retry` exponencial, `circuit breaker`, `timeout`.
* Legibilidade: nomes claros, modularização, DRY, invariantes explícitos.

### 🧮 Algoritmos & ED

* Ordenação (quicksort/mergesort), **busca binária** (requer ordenação).
* **Patterns**: dois ponteiros, janela deslizante, prefix sums, pilha monotônica, busca binária “na resposta”.
* Estruturas: hash map/set, heap, deque, DSU/Union-Find, árvore binária, **grafos** (BFS/DFS/Dijkstra/Topo).
* Complexidade: Big-O de **tempo e memória**, evitar loops aninhados e cópias grandes.

### 🧠 Paradigmas & Boas práticas

* **POO**: encapsulamento, herança vs **composição**; SOLID (alto nível); **DI**.
* **Funcional**: `map/filter/reduce`, imutabilidade, composição de funções.
* **Legibilidade**: nomes claros, modularização, testes de unidade.

### 🧑‍💻 Prática ao vivo

* Explique a abordagem **antes de codar**, valide casos extremos.
* Refatore: simplifique condicionais, extraia funções, elimine *smells*.
* Depure: ler *stack traces*, `debugger`, casos mínimos reproduzíveis.
* Clássicos: `two-sum`, inverter lista ligada, travessias em árvore, `top-k`, *merge intervals*.

### 🌐 Web & APIs

* HTTP/REST/JSON; **idempotência**; status codes; paginação (offset vs **keyset**).
* AuthN/AuthZ: JWT, OAuth2, sessões + cookies, *refresh token*.
* Segurança: **OWASP Top 10** (XSS, CSRF, SQLi, SSRF), validação/escape, **rate limit**, CORS, **CSP**.

---

## 🧩 Padrões de resolução (DSA Patterns)

> Passos universais: **(1) perguntar** → **(2) exemplos** → **(3) brute force** → **(4) otimizar** → **(5) provar** → **(6) testar**.

* **Dois ponteiros**: pares/somas em ordenados; remover duplicatas in-place.
* **Janela deslizante**: substrings com restrição (freq/únicos), médias e contagens.
* **Prefix sums / diferença**: faixas e somas 2D (matriz prefixada).
* **Pilha monotônica**: próximo maior/menor, histograma, “temperaturas”.
* **Busca binária (na resposta)**: minimizar maior carga, dividir livros, Kth.
* **Grafos**: BFS (sem peso), Dijkstra (peso positivo), 0–1 BFS, topológica (DAG).
* **DP**: knapsack, LIS O(n log n), partições, bitmask leve.

---

## 🗄️ Banco de Dados — Guia prático (detalhado)

> **Tecnologias**: PostgreSQL, SQLite, MySQL, MongoDB, Redis, Supabase (Postgres + SDK).
> **Supabase = Postgres + serviços.** SQL é igual ao do Postgres.

### 📦 CRUD Básico (exemplos práticos)

<details>
<summary><b>▶ Criar tabela / coleção</b></summary>

**Relacionais (PostgreSQL / SQLite / MySQL)**

```sql
-- PostgreSQL
CREATE TABLE usuarios (id SERIAL PRIMARY KEY, nome VARCHAR(100), idade INT);

-- SQLite
CREATE TABLE usuarios (id INTEGER PRIMARY KEY, nome TEXT, idade INTEGER);

-- MySQL
CREATE TABLE usuarios (id INT AUTO_INCREMENT PRIMARY KEY, nome VARCHAR(100), idade INT);
```

**MongoDB**

```javascript
db.createCollection("usuarios");
```

**Redis**

```text
# Chave-valor; não há tabelas/coleções
```

**Supabase (SQL = PostgreSQL)**

```sql
-- Idem PostgreSQL
```

</details>

<details>
<summary><b>▶ Inserir (1) / Inserir (vários)</b></summary>

**Relacionais**

```sql
INSERT INTO usuarios (nome, idade) VALUES ('Ana', 25);
INSERT INTO usuarios (nome, idade) VALUES ('Ana',25), ('Bia',30);
```

**MongoDB**

```javascript
db.usuarios.insertOne({ nome: "Ana", idade: 25 });
db.usuarios.insertMany([{ nome: "Ana", idade: 25 }, { nome: "Bia", idade: 30 }]);
```

**Redis**

```text
HSET user:1 nome "Ana" idade 25
# múltiplos HSET / JSON.SET (se módulo JSON)
```

**Supabase (SDK)**

```ts
await supabase.from("usuarios").insert([{ nome: "Ana", idade: 25 }]);
```

</details>

<details>
<summary><b>▶ Selecionar, ordenar e paginação</b></summary>

**Relacionais**

```sql
SELECT nome, idade FROM usuarios WHERE idade > 18;
SELECT * FROM usuarios ORDER BY idade DESC LIMIT 10 OFFSET 20;
```

**MongoDB**

```javascript
db.usuarios.find({ idade: { $gt: 18 } }, { nome:1, idade:1 });
db.usuarios.find().sort({ idade: -1 }).skip(20).limit(10);
```

**Redis**

```text
GET user:1
HGETALL user:1
ZREVRANGE users_by_age 20 29
```

**Supabase (SDK)**

```ts
await supabase.from("usuarios").select("nome,idade").gt("idade", 18);
await supabase.from("usuarios").select("*").order("idade", { ascending: false }).range(20, 29);
```

</details>

<details>
<summary><b>▶ Atualizar / Excluir</b></summary>

**Relacionais**

```sql
UPDATE usuarios SET idade = 30 WHERE nome = 'Ana';
DELETE FROM usuarios WHERE nome = 'Ana';
```

**MongoDB**

```javascript
db.usuarios.updateOne({ nome: "Ana" }, { $set: { idade: 30 } });
db.usuarios.deleteOne({ nome: "Ana" });
```

**Redis**

```text
HSET user:1 idade 30
DEL user:1
```

**Supabase (SDK)**

```ts
await supabase.from("usuarios").update({ idade: 30 }).eq("nome", "Ana");
await supabase.from("usuarios").delete().eq("nome", "Ana");
```

</details>

### 🔗 JOINs & Agregações (exemplos)

<details>
<summary><b>▶ INNER / LEFT JOIN</b></summary>

**Relacionais**

```sql
SELECT u.nome, p.valor
FROM usuarios u
JOIN pedidos p ON p.usuario_id = u.id;

SELECT u.nome, p.valor
FROM usuarios u
LEFT JOIN pedidos p ON p.usuario_id = u.id;
```

**MongoDB (\$lookup)**

```javascript
db.usuarios.aggregate([
  { $lookup: { from:"pedidos", localField:"id", foreignField:"usuario_id", as:"pedidos" } }
]);

db.usuarios.aggregate([
  { $lookup: { from:"pedidos", localField:"id", foreignField:"usuario_id", as:"pedidos" } },
  { $unwind: { path:"$pedidos", preserveNullAndEmptyArrays:true } }
]);
```

**Redis** — *n/a* (modelagem com sets/sorted sets se necessário)

</details>

<details>
<summary><b>▶ GROUP BY / HAVING • Funções agregadas</b></summary>

**Relacionais**

```sql
SELECT u.id, COUNT(*) AS qnt
FROM pedidos p JOIN usuarios u ON u.id = p.usuario_id
GROUP BY u.id HAVING COUNT(*) > 3;

SELECT AVG(idade), MIN(idade), MAX(idade) FROM usuarios;
```

**MongoDB**

```javascript
db.pedidos.aggregate([
  { $group: { _id: "$usuario_id", qnt: { $sum: 1 } } },
  { $match: { qnt: { $gt: 3 } } }
]);

db.usuarios.aggregate([
  { $group: { _id: null, avg: { $avg: "$idade" }, min: { $min: "$idade" }, max: { $max: "$idade" } } }
]);
```

</details>

### 🧭 Índices, Full-Text & JSON (exemplos)

<details>
<summary><b>▶ Índices / Full-Text / JSON</b></summary>

**Relacionais**

```sql
CREATE INDEX idx_idade ON usuarios(idade);
CREATE UNIQUE INDEX u_nome ON usuarios(nome);
-- Full-text (Postgres): tsvector/tsquery + pg_trgm
SELECT data->>'cep' FROM clientes;
SELECT * FROM clientes WHERE data->>'cep' = '12345-000';
```

**SQLite**

```sql
SELECT json_extract(data, '$.cep') FROM clientes;
```

**MySQL**

```sql
SELECT JSON_EXTRACT(data, '$.cep') FROM clientes;
```

**MongoDB**

```javascript
db.usuarios.createIndex({ idade: 1 });
db.usuarios.createIndex({ nome: 1 }, { unique: true });
db.clientes.find({ cep: "12345-000" });
```

**Redis**

```text
ZADD users_by_age 30 "user:1"
SETNX chave valor  # “unicidade”
# Full-text via RediSearch (módulo)
```

</details>

### ♻️ UPSERT, CTE & Window (exemplos)

<details>
<summary><b>▶ UPSERT / CTE / Window</b></summary>

**Relacionais**

```sql
INSERT INTO u (id, nome) VALUES (1, 'Ana')
ON CONFLICT (id) DO UPDATE SET nome = EXCLUDED.nome;

WITH m AS (SELECT * FROM u WHERE idade > 18) SELECT * FROM m;

SELECT nome, RANK() OVER (ORDER BY idade DESC) FROM u;  -- MySQL 8+
```

**MongoDB**

```javascript
db.u.updateOne({ id: 1 }, { $set: { nome: "Ana" } }, { upsert: true });
db.u.aggregate([{ $setWindowFields: { /* ... */ } }]);
```

**Redis** — `SET` (sobrescreve)

</details>

### 🛠️ DDL, Transações, Geodados, Paginação & Backup (exemplos)

<details>
<summary><b>▶ ALTER/Views/Transações • Geodados • Paginação estável • Backup</b></summary>

**Relacionais**

```sql
ALTER TABLE u ADD COLUMN email VARCHAR(200);
ALTER TABLE u RENAME COLUMN nome TO nome_completo;
CREATE VIEW v AS SELECT ...;
BEGIN; ... COMMIT;
-- Geodados: PostGIS (Postgres)
SELECT * FROM u WHERE id > :cursor ORDER BY id LIMIT 50; -- keyset
```

**MongoDB**

```javascript
db.u.updateMany({}, { $rename: { "nome":"nome_completo" } });
session.startTransaction(); /* ... */ session.commitTransaction();
// GeoJSON + 2dsphere
db.u.find({ _id: { $gt: cursor } }).sort({ _id: 1 }).limit(50);
```

**Redis**

```text
# sem ACID; usar scripts Lua para atomicidade
ZSCAN key cursor
```

**Backup/Restore**

```text
PostgreSQL: pg_dump / pg_restore
SQLite: copiar .db
MySQL: mysqldump / mysql
MongoDB: mongodump / mongorestore
Redis: RDB/AOF snapshots
```

</details>

---

## 🗄️ Banco de Dados — **Tabela Multi-Banco COMPLETA**

> **Operação | PostgreSQL | SQLite | MySQL | MongoDB | Redis | Supabase (Postgres + Client)**

| **Operação**               | **PostgreSQL**                                                                 | **SQLite**                                                                  | **MySQL**                                                                                  | **MongoDB**                                                   | **Redis**                         | **Supabase**                                                                  |
| -------------------------- | ------------------------------------------------------------------------------ | --------------------------------------------------------------------------- | ------------------------------------------------------------------------------------------ | ------------------------------------------------------------- | --------------------------------- | ----------------------------------------------------------------------------- |
| **Criar tabela / coleção** | `CREATE TABLE usuarios (id SERIAL PRIMARY KEY, nome VARCHAR(100), idade INT);` | `CREATE TABLE usuarios (id INTEGER PRIMARY KEY, nome TEXT, idade INTEGER);` | `CREATE TABLE usuarios (id INT AUTO_INCREMENT PRIMARY KEY, nome VARCHAR(100), idade INT);` | `db.createCollection("usuarios")`                             | —                                 | **idem (SQL)**                                                                |
| **Inserir (1)**            | `INSERT INTO usuarios (nome, idade) VALUES ('Ana', 25);`                       | `idem`                                                                      | `idem`                                                                                     | `db.usuarios.insertOne({ nome:"Ana", idade:25 })`             | `HSET user:1 nome "Ana" idade 25` | **idem (SQL)** / `supabase.from("usuarios").insert([{nome:"Ana", idade:25}])` |
| **Inserir (vários)**       | `INSERT INTO usuarios (nome,idade) VALUES ('Ana',25), ('Bia',30);`             | `idem`                                                                      | `idem`                                                                                     | `db.usuarios.insertMany([...])`                               | múltiplos `HSET/JSON.SET`         | **idem (SQL)**                                                                |
| **Selecionar (filtro)**    | `SELECT nome,idade FROM usuarios WHERE idade > 18;`                            | `idem`                                                                      | `idem`                                                                                     | `db.usuarios.find({ idade:{ $gt:18 } }, { nome:1, idade:1 })` | `GET user:1` / `HGETALL user:1`   | **idem (SQL)** / `.select("nome,idade").gt("idade",18)`                       |
| **Ordenar + paginar**      | `SELECT * FROM usuarios ORDER BY idade DESC LIMIT 10 OFFSET 20;`               | `idem`                                                                      | `idem`                                                                                     | `find().sort({idade:-1}).skip(20).limit(10)`                  | `ZREVRANGE users_by_age 20 29`    | **idem (SQL)** / `.order("idade",{ascending:false}).range(20,29)`             |
| **Atualizar**              | `UPDATE usuarios SET idade=30 WHERE nome='Ana';`                               | `idem`                                                                      | `idem`                                                                                     | `updateOne({nome:"Ana"}, { $set:{idade:30} })`                | `HSET user:1 idade 30`            | **idem (SQL)** / `.update({idade:30}).eq("nome","Ana")`                       |
| **Excluir**                | `DELETE FROM usuarios WHERE nome='Ana';`                                       | `idem`                                                                      | `idem`                                                                                     | `deleteOne({ nome:"Ana" })`                                   | `DEL user:1`                      | **idem (SQL)** / `.delete().eq("nome","Ana")`                                 |
| **JOIN (INNER)**           | `... JOIN ... ON ...`                                                          | `idem`                                                                      | `idem`                                                                                     | `$lookup`                                                     | —                                 | **idem (SQL)**                                                                |
| **LEFT JOIN**              | `LEFT JOIN`                                                                    | `idem`                                                                      | `idem`                                                                                     | `$lookup` + `$unwind` (preservando nulos)                     | —                                 | **idem (SQL)**                                                                |
| **GROUP BY/HAVING**        | `GROUP BY ... HAVING ...`                                                      | `idem`                                                                      | `idem`                                                                                     | `$group` + `$match`                                           | —                                 | **idem (SQL)**                                                                |
| **Agregadas**              | `AVG/MIN/MAX`                                                                  | `idem`                                                                      | `idem`                                                                                     | `$group` (avg/min/max)                                        | —                                 | **idem (SQL)**                                                                |
| **Índice simples**         | `CREATE INDEX idx_idade ON usuarios(idade);`                                   | `idem`                                                                      | `idem`                                                                                     | `createIndex({ idade:1 })`                                    | `ZADD users_by_age 30 "user:1"`   | **idem (SQL)**                                                                |
| **Índice único**           | `CREATE UNIQUE INDEX u_nome ON usuarios(nome);`                                | `idem`                                                                      | `idem`                                                                                     | `createIndex({ nome:1 }, { unique:true })`                    | `SETNX` (lógica)                  | **idem (SQL)**                                                                |
| **Full-text**              | `tsvector/tsquery`, `pg_trgm`                                                  | `FTS3/4/5`                                                                  | `FULLTEXT`                                                                                 | `$text`                                                       | RediSearch                        | **idem (SQL)**                                                                |
| **JSON (consulta/filtro)** | `data->>'cep'` / `WHERE data->>'cep'='...'`                                    | `json_extract`                                                              | `JSON_EXTRACT`                                                                             | BSON nativo                                                   | —                                 | **idem (SQL)**                                                                |
| **UPSERT**                 | `ON CONFLICT ... DO UPDATE`                                                    | `ON CONFLICT ...`                                                           | `ON DUPLICATE KEY UPDATE`                                                                  | `updateOne(..., { upsert:true })`                             | `SET` (sobrescreve)               | **idem (SQL)** / `.upsert([...])`                                             |
| **CTE (WITH)**             | `WITH ... AS (...) SELECT ...`                                                 | suporte básico                                                              | (MySQL 8+)                                                                                 | pipeline                                                      | —                                 | **idem (SQL)**                                                                |
| **Window**                 | `RANK() OVER(...)`                                                             | (3.25+)                                                                     | (8+)                                                                                       | `$setWindowFields`                                            | —                                 | **idem (SQL)**                                                                |
| **ALTER (ADD/RENAME)**     | `ALTER TABLE ... ADD/RENAME`                                                   | `idem`                                                                      | `idem`                                                                                     | `$rename`                                                     | —                                 | **idem (SQL)**                                                                |
| **Views / Materialized**   | `CREATE VIEW` / `CREATE MATERIALIZED VIEW`                                     | Views simples                                                               | Views simples                                                                              | coleções derivadas / `$merge`                                 | —                                 | **idem (SQL)**                                                                |
| **Transações**             | `BEGIN; ... COMMIT;` (MVCC)                                                    | `BEGIN/COMMIT`                                                              | `START TRANSACTION;`                                                                       | `session.startTransaction()`                                  | scripts Lua                       | **idem (SQL)**                                                                |
| **Geoespacial**            | PostGIS                                                                        | limitado                                                                    | GEOMETRY                                                                                   | GeoJSON + `2dsphere`                                          | módulos                           | **idem (SQL)**                                                                |
| **Paginação (keyset)**     | `WHERE id > $cursor ORDER BY id LIMIT ...`                                     | `idem`                                                                      | `idem`                                                                                     | `find({_id:{$gt:cursor}})...`                                 | `ZSCAN`                           | **idem (SQL)**                                                                |
| **Backup/restore**         | `pg_dump/pg_restore`                                                           | copiar .db                                                                  | `mysqldump/mysql`                                                                          | `mongodump/mongorestore`                                      | RDB/AOF                           | **idem (SQL)**                                                                |

> 💡 **PostgreSQL**: prefira `JSONB` + índice **GIN**; **keyset pagination** escala melhor que OFFSET; entenda **níveis de isolamento** e anomalias.

---

## 🧠 SQL avançado (CTE, Window, anti-join, pivot)

**Anti-join (encontrar ausentes)**

```sql
SELECT u.id
FROM usuarios u
LEFT JOIN pedidos p ON p.usuario_id = u.id
WHERE p.usuario_id IS NULL;
```

**CTE recursiva (hierarquia)**

```sql
WITH RECURSIVE chain AS (
  SELECT id, parent_id, 0 AS depth FROM categorias WHERE id = :root
  UNION ALL
  SELECT c.id, c.parent_id, depth+1
  FROM categorias c JOIN chain ch ON c.parent_id = ch.id
)
SELECT * FROM chain;
```

**Janela (acumulado por cliente)**

```sql
SELECT cliente_id,
       SUM(valor) OVER (PARTITION BY cliente_id ORDER BY data) AS acumulado
FROM vendas;
```

**Pivot simples (Postgres via FILTER)**

```sql
SELECT
  cliente_id,
  COUNT(*) FILTER (WHERE status='pago')     AS pagos,
  COUNT(*) FILTER (WHERE status='pendente') AS pendentes
FROM pedidos
GROUP BY cliente_id;
```

---

## 🟨 Supabase — Policies, Auth, Storage, Realtime, Edge

**RLS (Row Level Security) / Policies**

```sql
ALTER TABLE public.usuarios ENABLE ROW LEVEL SECURITY;

CREATE POLICY "read_self" ON public.usuarios
FOR SELECT USING (auth.uid() = id);

CREATE POLICY "insert_self" ON public.usuarios
FOR INSERT WITH CHECK (auth.uid() = id);

CREATE POLICY "update_self" ON public.usuarios
FOR UPDATE USING (auth.uid() = id) WITH CHECK (auth.uid() = id);
```

**Auth / OAuth**

```ts
await supabase.auth.signInWithPassword({ email, password });
await supabase.auth.signInWithOAuth({ provider: "github" });
```

**Storage / URL assinada**

```ts
await supabase.storage.from("bucket").upload("path/file.png", file);
const { data } = await supabase
  .storage.from("bucket")
  .createSignedUrl("path/file.png", 60);
```

**Realtime**

```ts
supabase
  .channel("room")
  .on("postgres_changes", { event: "*", schema: "public", table: "usuarios" }, console.log)
  .subscribe();
```

**Edge Function (Deno)**

```ts
// supabase/functions/say-hello/index.ts
import "jsr:@supabase/functions-js/edge-runtime.d.ts";

Deno.serve(async (req) => {
  const { name = "world" } = await req.json().catch(() => ({}));
  return new Response(JSON.stringify({ ok: true, msg: `Hello, ${name}!` }), {
    headers: { "Content-Type": "application/json" },
  });
});
```

---

## 🧾 APIs Web — Design, versionamento e erros

* **Versione** na URL: `/v1/...`; nada “quebra” sem nova versão.
* **Idempotência** para POST sensíveis (cobrança): `Idempotency-Key`.
* **Paginação**: prefira **cursor/keyset** (`next_cursor`) a `offset`.
* **Filtros**: whitelist de campos; ordenação segura.
* **Contratos**: OpenAPI/Swagger; exemplos de request/response.
* **Erros consistentes** + `correlation_id`.

**Modelo de erro**

```json
{
  "error": {
    "code": "RESOURCE_NOT_FOUND",
    "message": "Pedido não encontrado",
    "correlation_id": "b2b7c9..."
  }
}
```

**OpenAPI (trecho)**

```yaml
paths:
  /v1/pedidos:
    get:
      parameters:
        - name: cursor
          in: query
          schema: { type: string }
      responses:
        "200":
          content:
            application/json:
              schema: { $ref: "#/components/schemas/PedidosPage" }
```

---

## 🔐 Segurança — OWASP e checklist prático

<div style="background:#FFDD48; padding:8px 10px; border-radius:10px; font-weight:600;">
Checklist rápido
</div>

* **Input**: valide/normalize; **escape** (HTML/SQL); prepared statements.
* **AuthN/Z**: expiração do JWT, rotação de refresh, escopos; *least privilege*.
* **CSRF**: SameSite + token; **CORS** com origens confiáveis.
* **Headers**: `Content-Security-Policy`, `X-Frame-Options`, `X-Content-Type-Options`.
* **Segredos**: fora do repo (cofre/variáveis); rotação periódica.
* **Logs**: sem dados sensíveis; **correlation-id**.
* **Rate limit** e bot detection nas rotas críticas.

---

## 🖥️ Sistemas Operacionais & Redes

* Processos vs threads; bloqueante vs não-bloqueante; **CPU-bound vs IO-bound**.
* TCP vs UDP; TLS handshake; DNS; HTTP/1.1 vs 2 vs 3 (QUIC).
* Latência vs **throughput**; Nagle; keep-alive; backpressure.
* `JS`: `async/await` e event loop • `Go`: goroutines + channels.

---

## 🔀 Concorrência & Assíncrono

* Locks (mutex), RW-lock, **optimistic locking** (versões), CAS.
* Filas *producer–consumer*; **debounce** vs **throttle**.
* **Idempotência** (APIs/BD); **isolamento** (RC/RR/Serializable), *phantom reads*; **sagas** e compensações.

---

## 🏗️ Design de Sistemas — Passo a passo + estimativas

**Roteiro (8 passos)**

1. Escopo/MVP • 2) Cargas (RPS/picos/storage) • 3) APIs & idempotência • 4) Dados (chaves/índices/padrões de acesso) • 5) Componentes (LB/app/cache/BD/fila/blobs/search) • 6) Consistência (forte vs eventual) • 7) Falhas (timeouts/retries/circuit breaker/DR) • 8) Observabilidade (logs/RED/USE/tracing).

**Back-of-the-envelope**

* 1 RPS ≈ **86.4k req/dia**.
* Pico 200 RPS (95% leitura) → **cache** na frente do BD + réplicas de leitura.
* P95 < 200 ms: DNS+TLS (\~50) + app (60) + BD (40) + cache (10) + rede (40).

**Arquitetura exemplo**

* API **stateless** (3 réplicas) atrás de **LB L7**; **Redis** para leitura quente; **Postgres** com réplicas; **S3-like** para blobs; **fila** (RabbitMQ/Kafka) para jobs; **keyset** nos painéis; **RLS** multi-tenant.

---

## 📊 Observabilidade & Performance

* **Logs estruturados** (JSON) + `correlation_id`.
* **RED** (Rate, Errors, Duration) | **USE** (Utilization, Saturation, Errors).
* Métricas **p50/p95/p99**; budgets de latência; sprint de performance.
* **Profiling**: CPU/heap; **N+1 queries**; GC; IO.

---

## 🌳 Git & Fluxos de trabalho

* **Conventional Commits**; branching: `main` protegido, `feature/*`, `hotfix/*`.
* **Rebase interativo** antes do PR; `bisect` para regressões.
* PRs curtos; linters/tests no CI.

**CI (GitHub Actions — Node)**

```yaml
name: ci
on: [push, pull_request]
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      - uses: actions/checkout@v4
      - uses: actions/setup-node@v4
        with: { node-version: "20" }
      - run: npm ci
      - run: npm run lint && npm test
      - run: npm run build
```

**Dockerfile (Node)**

```dockerfile
FROM node:20-alpine
WORKDIR /app
COPY package*.json ./
RUN npm ci --omit=dev
COPY . .
CMD ["node","dist/server.js"]
```

---

## 🧪 Testes (Pirâmide, mocks, E2E)

* **Pirâmide**: unidade >> integração > E2E.
* Unidade: funções puras/domínio. Integração: BD/filas/HTTP. E2E: fluxos críticos.
* Evite **over-mocking**; cubra bordas (timeouts/falhas externas); dados realistas (não sensíveis).

---

## 🧑‍💻 Playbook de Live Coding

1. Confirme requisitos/limites.
2. Mostre brute force e por que otimizar.
3. Escolha o **pattern** (janela/pilha/grafo/DP).
4. Esboce testes: base, borda, grandes.
5. Codifique claro (nomes/early returns).
6. Analise **complexidade** e riscos.
7. Refatore e comente decisões.

---

## 🗣️ Comportamental (STAR/CARL) + respostas modelo

**Modelos**

* **STAR**: Situação • Tarefa • Ação • Resultado.
* **CARL**: Contexto • Ação • Resultado • Lições.

**Perguntas comuns + esqueletos**

* **Fale sobre você**: trajetória curta → 2 conquistas mensuráveis → o que busca.
* **Maior desafio**: risco alto → ações concretas → impacto numérico.
* **Conflito**: empatia + objetivo comum + acordo verificável.
* **Falha**: como detectou; como mitigou; lição aplicada depois.

<div style="background:#FFF8B0; border-left:8px solid #FFDD48; padding:10px 12px; border-radius:8px;">
💬 Dica: tenha 3 histórias “de bolso”: <i>bug crítico</i>, <i>otimização com impacto</i>, <i>liderança sem cargo</i>.
</div>

---

## ❓ Perguntas para o entrevistador

* Quais as **métricas de sucesso** do time/produto?
* Como é o fluxo de **deploy** e **on-call**?
* Quais os **gargalos técnicos** mais críticos?
* Como medem **performance** (p95/p99) e evitam regressões?
* Qual o **roadmap** (6–12 meses) e principais riscos?

---

## 📆 Planos de estudo (7/14/30 dias)

**7 dias (sprint)**

* DSA: 2 patterns/dia + 5 exercícios.
* SQL: JOIN/CTE/Window.
* Web: HTTP/status/paginação/erros.
* 1 simulado de código + 1 comportamental.

**14 dias (equilíbrio)**

* DSA: grafos (BFS/Dijkstra/Topo), pilha monotônica, DP leve.
* DB: índices, keyset, JSONB, transações.
* Design: cache/fila/replicação; 2 estudos de caso.
* 2 simulados (1 código, 1 design).

**30 dias (robusto)**

* DSA avançado + revisões.
* Design completo (feed, chat, encurtador, analytics).
* Segurança & observabilidade (RED/USE, tracing).
* 4 simulados (2 código, 2 design) + gravação para feedback.

---

## 🧾 Cheat sheets úteis (JS/TS/Python/Java)

**Coleções e tipos**

| Conceito   | JS/TS                       | Python               | Java                           |
| ---------- | --------------------------- | -------------------- | ------------------------------ |
| Dicionário | `Record<string,T>` / `Map`  | `dict`               | `Map<K,V>`                     |
| Conjunto   | `Set<T>`                    | `set`                | `Set<T>`                       |
| Fila       | `Array` + `shift` / `Deque` | `collections.deque`  | `ArrayDeque` / `Queue`         |
| Heap       | (lib externa)               | `heapq`              | `PriorityQueue`                |
| Imutáveis  | `readonly`, `as const`      | `tuple`, `frozenset` | `List.of(...)` (view imutável) |

**Try/catch**

* **JS/TS**

  ```ts
  try { await doWork(); }
  catch (e) { logger.error(e); throw new Error("OP_FAILED"); }
  ```
* **Python**

  ```py
  try:
      do_work()
  except Exception as e:
      logger.exception(e)
      raise
  ```
* **Java**

  ```java
  try { doWork(); }
  catch (Exception e) { log.error("fail", e); throw e; }
  ```

**HTTP status (essencial)**
200 OK • 201 Created • 204 No Content • 400 Bad Request • 401 Unauthorized • 403 Forbidden • 404 Not Found • 409 Conflict • 422 Unprocessable • 429 Too Many Requests • 500/502/503

---

## ⏱️ Checklist final (5 min antes)

* Explique **trade-offs** de 2 abordagens.
* Tenha **exemplos** de falha/risco e mitigação.
* Relembre **padrões** (janela, dois ponteiros, pilha, binária, grafo).
* Prepare 2–3 **perguntas** ao final.
* Teste câmera/áudio/IDE (se remoto).

---

## 📝 Notas rápidas + Setup Supabase

* **UPSERT**: Postgres/SQLite → `ON CONFLICT`; MySQL → `ON DUPLICATE KEY UPDATE`; Mongo → `upsert:true`; Redis → `SET`.
* **Full-text**: Postgres (`tsvector/tsquery` + `pg_trgm`), MySQL (`FULLTEXT`), SQLite (FTS), Mongo (`$text`), Redis (RediSearch).
* **Supabase**: Para SQL, copie PostgreSQL; para SDK, use `.select/.insert/.update/.upsert/.rpc`.

**Setup rápido (JS/TS)**

```ts
// npm i @supabase/supabase-js
import { createClient } from "@supabase/supabase-js";

const supabase = createClient(
  process.env.NEXT_PUBLIC_SUPABASE_URL!,
  process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY!
);
```

---

<div style="text-align:center; background:#FFDD48; border-radius:16px; padding:12px 14px; font-weight:800;">
Pronto! Todo o conteúdo foi reunido no <b>README gigante</b>, sem tirar nada — com a tabela multi-banco completa e todas as seções expandidas. Boa preparação! 💛
</div>

---

# 🔥 Supabase SDK — **JS/TS & Python (Recipes completas)** *(ADICIONADO)*

<div style="background:#FFDD48; border-radius:12px; padding:10px 12px; font-weight:700;">
Tudo abaixo foi <u>adicionado</u> sem remover nada do seu README. Foco em uso prático do Supabase em <b>JS/TS</b> e <b>Python</b> (Auth, Storage, CRUD, filtros, paginação, RLS, RPC, Realtime, tipos, testes).
</div>

## 📦 Instalação & Ambiente

**JavaScript/TypeScript**

```bash
npm i @supabase/supabase-js
# ou
pnpm add @supabase/supabase-js
```

```ts
import { createClient } from "@supabase/supabase-js";

export const supabase = createClient(
  process.env.NEXT_PUBLIC_SUPABASE_URL!,     // NUNCA vaze a service_role no client
  process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY! // Chave ANON no front
);
```

**Python**

```bash
pip install supabase
```

```py
import os
from supabase import create_client, Client

supabase_url: str = os.environ["SUPABASE_URL"]
supabase_key: str = os.environ["SUPABASE_KEY"]  # use a ANON no client; service_role só no backend
supabase: Client = create_client(supabase_url, supabase_key)
```

<div style="background:#FFF8B0; border-left:8px solid #FFDD48; padding:8px 10px; border-radius:8px;">
🔐 <b>Segurança:</b> Chave <code>service_role</code> <u>nunca</u> vai para o navegador/app móvel. Use-a apenas no backend para tarefas administrativas.
</div>

---

## 🧑‍💻 CRUD, Filtros, Ordenação e Paginação

**JS/TS — CRUD + filtros**

```ts
// Create
const { data: inserted, error: e1 } = await supabase
  .from("usuarios")
  .insert([{ nome: "Ana", idade: 25 }]);

// Read (filtros)
const { data: rows, error: e2 } = await supabase
  .from("usuarios")
  .select("id, nome, idade")
  .gt("idade", 18)            // > 18
  .ilike("nome", "%an%");     // case-insensitive

// Update
const { error: e3 } = await supabase
  .from("usuarios")
  .update({ idade: 30 })
  .eq("nome", "Ana");

// Delete
const { error: e4 } = await supabase
  .from("usuarios")
  .delete()
  .eq("nome", "Ana");
```

**JS/TS — Ordenação + paginação (`range`)**

```ts
const page = 3, size = 10;
const from = (page - 1) * size;
const to = from + size - 1;

const { data, error } = await supabase
  .from("usuarios")
  .select("*")
  .order("idade", { ascending: false, nullsFirst: false })
  .range(from, to);
```

**Python — CRUD + filtros**

```py
# Create
res = supabase.table("usuarios").insert({"nome": "Ana", "idade": 25}).execute()

# Read (filtros)
res = (
  supabase.table("usuarios")
  .select("id, nome, idade")
  .gt("idade", 18)
  .ilike("nome", "%an%")
  .execute()
)
rows = res.data

# Update
supabase.table("usuarios").update({"idade": 30}).eq("nome", "Ana").execute()

# Delete
supabase.table("usuarios").delete().eq("nome", "Ana").execute()
```

**Python — Ordenação + paginação**

```py
page, size = 3, 10
start, end = (page - 1) * size, (page * size) - 1

res = (
  supabase.table("usuarios")
  .select("*")
  .order("idade", desc=True)
  .range(start, end)
  .execute()
)
```

---

## ♻️ UPSERT (conflitos), Joins aninhados e Views

**JS/TS — UPSERT com `onConflict`**

```ts
await supabase
  .from("usuarios")
  .upsert([{ id: 1, nome: "Ana", idade: 25 }], { onConflict: "id" });
```

**JS/TS — “join” via relação (PostgREST)**

```ts
// suponha: pedidos(usuario_id) -> usuarios(id)
const { data } = await supabase
  .from("pedidos")
  .select(`
    id, valor, created_at,
    usuarios:usuario_id ( id, nome )
  `)
  .eq("usuarios.nome", "Ana");
```

**Python — UPSERT e relação**

```py
supabase.table("usuarios").upsert({"id": 1, "nome": "Ana", "idade": 25}).execute()

res = (
  supabase.table("pedidos")
  .select("id, valor, created_at, usuarios:usuario_id ( id, nome )")
  .eq("usuarios.nome", "Ana")
  .execute()
)
```

> 💡 Para <b>views materializadas</b> e CTEs, use SQL puro no Supabase (mesmo dialeto do PostgreSQL).

---

## 🔐 Auth (email/senha, OAuth, sessão) e RLS

**JS/TS — Email/senha & sessão atual**

```ts
const { data: signInData, error } = await supabase.auth.signInWithPassword({
  email: "ana@example.com",
  password: "secret"
});

const {
  data: { user, session }
} = await supabase.auth.getSession();

await supabase.auth.signOut();
```

**JS/TS — OAuth (ex.: GitHub)**

```ts
await supabase.auth.signInWithOAuth({ provider: "github" });
```

**Python — Email/senha & logout**

```py
auth = supabase.auth.sign_in_with_password({"email": "ana@example.com", "password": "secret"})
current = supabase.auth.get_session()
supabase.auth.sign_out()
```

**RLS — Policies úteis (SQL)**

```sql
ALTER TABLE public.usuarios ENABLE ROW LEVEL SECURITY;

CREATE POLICY "read_self" ON public.usuarios
FOR SELECT USING (auth.uid() = id);

CREATE POLICY "insert_self" ON public.usuarios
FOR INSERT WITH CHECK (auth.uid() = id);

CREATE POLICY "update_self" ON public.usuarios
FOR UPDATE USING (auth.uid() = id) WITH CHECK (auth.uid() = id);
```

> ⚠️ Teste suas queries com e sem sessão (ANON vs service\_role) para garantir que as policies funcionem como esperado.

---

## 🗂️ Storage (upload, public URL, signed URL)

**JS/TS**

```ts
// Upload (Blob/File no browser)
await supabase.storage.from("bucket").upload("avatars/ana.png", file);

// Public URL (se o bucket for público)
const { data: pub } = supabase.storage.from("bucket").getPublicUrl("avatars/ana.png");

// Signed URL (expira em 60s)
const { data: signed } = await supabase
  .storage
  .from("bucket")
  .createSignedUrl("avatars/ana.png", 60);
```

**Python**

```py
# Upload (bytes ou caminho)
with open("ana.png", "rb") as f:
    supabase.storage.from_("bucket").upload("avatars/ana.png", f)

# Public URL
pub = supabase.storage.from_("bucket").get_public_url("avatars/ana.png")

# Signed URL
signed = supabase.storage.from_("bucket").create_signed_url("avatars/ana.png", 60)
```

---

## 📡 Realtime (escuta de mudanças)

**JS/TS — Postgres Changes**

```ts
const channel = supabase
  .channel("room")
  .on("postgres_changes",
    { event: "*", schema: "public", table: "usuarios" },
    payload => console.log("change:", payload)
  )
  .subscribe();

// ... depois
supabase.removeChannel(channel);
```

---

## 🧮 RPC (funções SQL)

**PostgreSQL (SQL)**

```sql
CREATE OR REPLACE FUNCTION total_pedidos(uid uuid)
RETURNS integer
LANGUAGE sql
AS $$
  SELECT COUNT(*) FROM pedidos WHERE usuario_id = uid;
$$;
```

**JS/TS — chamar RPC**

```ts
const { data, error } = await supabase.rpc("total_pedidos", { uid: "..." });
```

**Python — chamar RPC**

```py
res = supabase.rpc("total_pedidos", {"uid": "..."}).execute()
```

---

## ✅ Padrões de erro & Retentativas

**JS/TS**

```ts
const { data, error } = await supabase.from("u").select("*");
if (error) {
  console.error(error);
  // backoff simples
  await new Promise(r => setTimeout(r, 300));
  // tente novamente se fizer sentido...
}
```

**Python**

```py
res = supabase.table("u").select("*").execute()
if res.error:
    print(res.error)
    # estratégia de retry se for transitório
```

---

## 🧰 TypeScript: tipos fortes (Database)

Gere tipos do esquema e use no client para autocompletar/checar colunas:

```ts
// types/database.ts (exemplo de tipo gerado, simplificado)
export type Database = {
  public: {
    Tables: {
      usuarios: {
        Row: { id: string; nome: string; idade: number | null };
        Insert: { id?: string; nome: string; idade?: number | null };
        Update: { nome?: string; idade?: number | null };
      };
    };
  };
};
```

```ts
import { createClient } from "@supabase/supabase-js";
import type { Database } from "./types/database";

const supabase = createClient<Database>(
  process.env.NEXT_PUBLIC_SUPABASE_URL!,
  process.env.NEXT_PUBLIC_SUPABASE_ANON_KEY!
);

// agora supabase.from("usuarios") fica tipado
```

> 💛 Vantagem: menos erro de coluna/campo e melhor DX durante a entrevista.

---

## 🧪 Testes (JS/TS & Python) com Supabase

**JS/TS (Vitest/Jest) — integração leve**

```ts
import { supabase } from "../src/db";

test("insere e lê usuario", async () => {
  const { error: e1 } = await supabase.from("usuarios").insert([{ nome: "Ana", idade: 25 }]);
  expect(e1).toBeNull();

  const { data, error: e2 } = await supabase.from("usuarios").select("*").eq("nome", "Ana").single();
  expect(e2).toBeNull();
  expect(data?.idade).toBe(25);
});
```

**Python (pytest)**

```py
from supabase import create_client

def test_insert_read(monkeypatch):
    supabase = create_client("http://...", "anon-key")
    supabase.table("usuarios").insert({"nome":"Ana","idade":25}).execute()
    res = supabase.table("usuarios").select("*").eq("nome","Ana").single().execute()
    assert res.data["idade"] == 25
```

---

## 🧭 Boas práticas rápidas (JS/TS & Python)

* **Paginação estável**: combine `.order("id")` com `.range(...)` e “cursor” quando fizer sentido.
* **Idempotência**: use `.upsert` com `onConflict` para evitar duplicatas.
* **Políticas RLS**: sempre escreva `SELECT/INSERT/UPDATE/DELETE` separadas e teste com contas diferentes.
* **Erros**: padronize respostas (mapeie `PostgREST` errors para seus DTOs).
* **Tipos (TS)**: gere `Database` e injete no `createClient<Database>()`.
* **Service tasks**: no backend, use `service_role` para tarefas administrativas (ex.: seeds/migrações), nunca no cliente.
