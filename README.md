# Vorseum

**Vorseum** é uma holding tecnológica orientada à criação de produtos e serviços proprietários, com foco em segurança digital, inteligência aplicada, infraestrutura tecnológica e soluções personalizadas para diferentes segmentos de mercado.

Seu objetivo não é apenas desenvolver softwares isolados — é construir um **ecossistema interconectado de soluções**, capaz de atender desde usuários individuais até grandes organizações e estruturas governamentais.

---

## Por que a Vorseum existe

A Vorseum nasce da necessidade de resolver um problema estrutural contemporâneo:

> A crescente dependência da tecnologia sem a devida proteção, controle e inteligência sobre os próprios sistemas.

A empresa se posiciona como uma **arquitetura de proteção e evolução digital**, sustentada por três pilares:

| Pilar | Descrição |
|---|---|
| **Segurança** | Proteger dados, sistemas e identidades |
| **Controle** | Dar visibilidade e governança sobre ambientes digitais |
| **Escala** | Permitir crescimento sustentável e estruturado |

---

## Estrutura Estratégica

A Vorseum não é um único produto, mas um **ecossistema modular**, composto por diferentes frentes de atuação:

- **Núcleo de Produtos** — softwares próprios com foco em segurança digital, monitoramento, inteligência automatizada e proteção contra ameaças
- **Soluções Corporativas** — customização e implementação para empresas privadas, profissionais especializados e organizações com necessidades específicas
- **Infraestrutura e Plataforma** — base tecnológica que garante escalabilidade, integração entre produtos e padronização de serviços
- **Expansão Institucional** — atuação potencial no setor governamental, projetos regulados e parcerias estratégicas de grande escala

---

## Modelo de Negócio

Modelo híbrido, combinando:

- **SaaS** — produtos com planos recorrentes
- **Licenciamento e contratos** — para empresas e instituições
- **Serviços especializados** — customização, implementação e suporte
- **Expansão vertical** — novos produtos dentro do próprio ecossistema

---

## Diferencial Competitivo

O diferencial da Vorseum não está apenas no que ela constrói, mas em **como ela estrutura o que constrói**:

- **Arquitetura orientada a ecossistema** — produtos pensados para integração desde o início
- **Segurança como núcleo, não como feature** — não é um módulo adicional, é a base
- **Visão de longo prazo** — construção estruturada, não soluções pontuais
- **Evolução modular** — cada produto fortalece o todo

A Vorseum se posiciona entre empresas de cibersegurança, plataformas de infraestrutura digital e holdings de tecnologia multi-produto — mas opera como uma **camada estratégica acima dessas categorias**, integrando funcionalidades que normalmente estão fragmentadas no mercado.

---

## Visão de Longo Prazo

```
Validação de MVPs
       ↓
Consolidação de base de usuários
       ↓
Expansão para empresas (B2B)
       ↓
Entrada em mercados regulados
       ↓
Internacionalização
```

No longo prazo, a Vorseum busca operar com diferentes unidades especializadas sob uma mesma estrutura estratégica, com atuação em:

- Produtos SaaS escaláveis
- Soluções corporativas (B2B)
- Infraestrutura crítica
- Ambientes regulados (governo)
- Expansão internacional

---

## Impacto Social

Além do objetivo econômico, a Vorseum possui potencial para gerar impacto estrutural:

- Apoio a iniciativas educacionais em tecnologia
- Desenvolvimento de soluções acessíveis
- Proteção digital de populações vulneráveis

Essa dimensão faz parte da visão de longo prazo da empresa.

---

---

# Vorseum Cyber

**Vorseum Cyber** é o primeiro produto da Vorseum — uma plataforma de cibersegurança personalizada, criada para proteger profissionais e pequenas empresas contra vazamento de dados, falhas humanas e exposição digital. Rápida, inteligente e acessível, é a primeira camada de defesa para quem lida com dados sensíveis no dia a dia.

---

## Propósito do MVP

Oferecer segurança real e tangível para públicos com alta exposição e pouca proteção digital. O MVP já entrega valor desde o primeiro uso, com monitoramento de dados, alertas automáticos e consulta de status de vazamentos.

---

## Público-alvo

- Profissionais da saúde (psicólogos, dentistas, terapeutas)
- Pequenas empresas e consultórios com base de clientes
- Criadores de conteúdo com presença online

---

## Funcionalidades

### 1. Autenticação e Usuários

- Cadastro e login com Devise + JWT
- Perfis com roles (`admin`, `user`)
- Endpoint protegido de perfil

### 2. Monitoramento de Vazamento de Dados

- Cadastro de e-mails, CPFs e domínios para monitoramento
- Verificação automática via job em background ao cadastrar
- Agendamento recorrente diário para re-checagem (`BreachCheckJob`)
- Integração com [Have I Been Pwned](https://haveibeenpwned.com/) para e-mails e domínios
- Integração configurável com API externa para verificação de CPF

### 3. Consulta de Status de Vazamentos

- Endpoint `GET /api/v1/monitor/:id` com resultado detalhado por tipo (email, CPF, domínio)
- Campo `breached` consolidado para facilitar exibição no frontend
- Histórico de quando a última verificação foi realizada

### 4. Alertas de Exposição

- Envio automático de e-mail ao detectar vazamento (`BreachAlertMailer`)
- Mensagem personalizada com os dados afetados

### 5. Threat Intelligence — Monitoramento de IPs

- Consulta de reputação de IPs via [AbuseIPDB](https://www.abuseipdb.com/)
- Classificação automática de risco: `low`, `medium`, `high`, `critical`
- Armazenamento de metadata completo (ISP, país, total de denúncias, última denúncia)
- Histórico de IPs monitorados por usuário, com isolamento multi-tenant

---

## Stack Técnica

| Camada | Tecnologia |
|---|---|
| Backend | Ruby on Rails 8 (API-only) |
| Banco de dados | PostgreSQL com campo JSONB |
| Autenticação | Devise + JWT |
| Background jobs | Solid Queue |
| Testes | RSpec + FactoryBot |
| Integrações HTTP | Faraday |
| Frontend | React *(planejado)* |

---

## API — Referência dos Endpoints

### Autenticação

| Método | Rota | Descrição |
|---|---|---|
| `POST` | `/api/v1/signup` | Cadastro de usuário |
| `POST` | `/api/v1/login` | Login, retorna token JWT |
| `GET` | `/api/v1/profile` | Dados do usuário autenticado |

### Monitoramento

| Método | Rota | Descrição |
|---|---|---|
| `GET` | `/api/v1/monitor` | Lista todos os dados monitorados do usuário |
| `POST` | `/api/v1/monitor` | Cadastra novo dado e dispara verificação |
| `GET` | `/api/v1/monitor/:id` | Retorna status detalhado de vazamentos |
| `DELETE` | `/api/v1/monitor/:id` | Remove dado monitorado |

### Threat Intelligence

| Método | Rota | Descrição |
|---|---|---|
| `GET` | `/api/v1/threat_intel` | Lista IPs monitorados do usuário |
| `POST` | `/api/v1/threat_intel` | Submete IP → consulta AbuseIPDB → salva resultado |
| `GET` | `/api/v1/threat_intel/:id` | Detalhe de um registro de ameaça |
| `DELETE` | `/api/v1/threat_intel/:id` | Remove registro |

### Exemplos de Resposta

**`POST /api/v1/threat_intel`**

```json
{
  "id": 1,
  "ip": "1.2.3.4",
  "source": "abuseipdb",
  "risk_level": "high",
  "metadata": {
    "abuse_confidence_score": 82,
    "country_code": "RU",
    "isp": "Some Hosting ISP",
    "domain": "evil.com",
    "total_reports": 37,
    "last_reported_at": "2024-01-15T10:00:00+00:00"
  },
  "created_at": "2025-07-25T12:00:00.000Z"
}
```

**`GET /api/v1/monitor/:id`**

```json
{
  "id": 1,
  "email": "usuario@exemplo.com",
  "cpf": "123.456.789-09",
  "domain": "empresa.com.br",
  "last_checked_at": "2025-07-25T12:00:00.000Z",
  "breached": true,
  "checks": {
    "email": {
      "breached": true,
      "breaches": [{ "Name": "Adobe", "BreachDate": "2013-10-04" }]
    },
    "cpf": {
      "breached": false,
      "breaches": []
    },
    "domain": {
      "breached": false,
      "breaches": []
    }
  }
}
```

---

## Variáveis de Ambiente

| Variável | Obrigatória | Descrição |
|---|---|---|
| `HIBP_API_KEY` | Sim | Chave de API do Have I Been Pwned |
| `CPF_BREACH_API_URL` | Não | URL da API de verificação de CPF |
| `CPF_BREACH_API_KEY` | Não | Token de autenticação da API de CPF |
| `ABUSEIPDB_API_KEY` | Não* | Chave de API do AbuseIPDB (obrigatória para Threat Intel) |
| `DATABASE_URL` | Sim | URL de conexão com o PostgreSQL |
| `DEVISE_JWT_SECRET_KEY` | Sim | Secret para assinatura dos tokens JWT |

---

## Configuração Local

```bash
# Instalar dependências
bundle install

# Configurar banco de dados
bin/rails db:create db:migrate

# Rodar testes
bundle exec rspec

# Subir servidor
bin/rails server
```

---

## Status de Desenvolvimento

- [x] Autenticação segura com Devise + JWT
- [x] Estrutura de usuários com role
- [x] Monitoramento de e-mails, CPFs e domínios
- [x] Verificação automática via job em background
- [x] Agendamento recorrente diário de re-checagem
- [x] Alertas automáticos por e-mail ao detectar vazamento
- [x] Endpoint de status detalhado de vazamentos por item
- [x] Testes automatizados (RSpec + FactoryBot)
- [x] Threat Intelligence — monitoramento de IPs via AbuseIPDB com classificação de risco
- [ ] Frontend (React)
- [ ] Relatório mensal (PDF ou Web)
- [ ] Threat Intel avançado — integração com VirusTotal e Shodan

---

## Licença

Este projeto está sob licença proprietária enquanto em desenvolvimento interno. Direitos autorais reservados à Vorseum.

---

## Desenvolvido por

**Hannah Freitas**
Backend Developer & CEO da Vorseum
*Construindo segurança digital com propósito.*
