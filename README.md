# ⚙️ GeoSUS - Infraestrutura e Execução

Este repositório contém o `docker-compose.yml` que orquestra a execução dos microsserviços do sistema **GeoSUS**: `unidade-service`, `paciente-service` e `fila-service`, além do banco de dados PostgreSQL.

---

## 🚀 Como rodar o GeoSUS localmente

### ✅ Pré-requisitos

- Docker
- Docker Compose
- Git

---

### 🧭 Passo a passo

1. **Clone este repositório de infraestrutura:**

```bash
git clone https://github.com/moreiralud/infra-geosus.git
cd infra-geosus
```

2. **Execute o sistema com Docker Compose:**

```bash
docker-compose up --build
```

Isso irá:

- Subir o banco de dados PostgreSQL (porta `5434`).
- Subir os três microsserviços:
  - **unidade-service** na porta `8080`
  - **paciente-service** na porta `8081`
  - **fila-service** na porta `8082`

---

### 🧪 Como testar os endpoints

Você pode usar **Swagger** ou **Postman** para interagir com os serviços.

#### 🔹 1. Cadastrar um paciente

**POST** `http://localhost:8081/pacientes`

```json
{
  "nome": "João da Silva",
  "cpf": "11122233344",
  "latitude": -10.9472,
  "longitude": -37.0731
}
```

---

#### 🔹 2. Cadastrar uma unidade de saúde

**POST** `http://localhost:8080/unidades`

```json
{
  "nome": "UPA Nova Aracaju",
  "tipo": "UPA",
  "endereco": "Av. Central, 456, Aracaju-SE",
  "servicos": ["Emergência", "Raio-X"],
  "vagasDisponiveis": 3
}
```

---

#### 🔹 3. Direcionar paciente para unidade mais próxima

**POST** `http://localhost:8082/fila/direcionar`

```json
{
  "cpf": "11122233344",
  "latitude": -10.9472,
  "longitude": -37.0731,
  "raioKm": 5
}
```

**Resposta esperada:**

```json
{
  "id": 3,
  "nome": "UPA Nova Aracaju",
  "tipo": "UPA",
  "endereco": "Av. Central, 456, Aracaju-SE",
  "latitude": -10.9135,
  "longitude": -37.0751,
  "vagasDisponiveis": 3
}
```

---

## 🧹 Parar e limpar os containers

```bash
docker-compose down -v
```

Isso remove os containers e volumes, limpando o ambiente local.

---

## 📎 Repositórios relacionados

- [`unidade-service`](https://github.com/moreiralud/geosus)
- [`paciente-service`](https://github.com/moreiralud/paciente-service)
- [`fila-service`](https://github.com/moreiralud/fila-service)

---

## 👩‍💻 Autora

[Ludmila Moreira](https://github.com/moreiralud) • Tech Challenge Fase 4 – GeoSUS 🚑🌍
