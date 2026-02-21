# Implementação da solução Vô-Lembrá (Java + Angular)

> Você está operando em **Agent Mode**, com permissão para:
>
> * Criar e editar arquivos
> * Implementar código
> * Ajustar configurações
>
> Atue como um **Senior FullStack Engineer** com foco em java e angular, responsável pela implementação completa da API.

---

## 📌 Contexto obrigatório (LEITURA INICIAL)

Antes de iniciar qualquer implementação, **leia atentamente** os seguintes arquivos:

```
.ai/standards.md
.ai/architecture.md
.ai/tech-stack.md
.ai/business-rules.md
```

Todas as decisões técnicas, arquiteturais e de negócio **DEVEM** seguir exatamente o que está definido nesses documentos.

⚠️ Se houver conflito entre este prompt e os arquivos `.ai/`, **os arquivos `.ai/` têm prioridade**.

---

## 🎯 Objetivo

Implementar uma solução para gerenciamento de horários de medicamentos, **API REST em Java 25 + Spring Boot + Angular 21** que **faça a gestão de responsáveis, medicamentos, pacientes e alertas**, conforme o arquivo ./.ai/business-rules.md

A aplicação deve possuir:

* Um monolito back-end java 25 para realizar as transações com o banco de dados
* Um monolito front-end angular 21 para utilização do usuário
* Banco de dados MYSQL
* Docker para subir uma imagem do banco de dados

---

## 🧩 Escopo funcional (FECHADO)

A API possui **exatamente dois endpoints públicos**:

* `POST /api/auth/register`
* `POST /api/auth/login`

Os demais endpints mencionados devem se autenticar com token JWT.

---

## 🛠️ Etapas obrigatórias de implementação

Execute o trabalho **nesta ordem**, sem pular etapas:

### 🔹 Etapa 1 (Backend) — Estrutura do projeto

* Criar projeto Spring Boot compatível com **Java 25**
* Usar Maven
* Configurar `application.yml`
* Organizar pacotes conforme `.ai/standards.md`

---

### 🔹 Etapa 2 (Backend) — Domínio e DTOs

* Criar modelos de domínio para notícias e fontes
* Criar DTOs usando `record`
* Garantir imutabilidade
* Garantir serialização compatível com o contrato GNews

---

### 🔹 Etapa 3 (Backend) — Implementação dos endpoints

* Implementar:
    * `POST api/auth/login`: Login para responsáveis e pacientes.
    * `POST api/auth/register`: Registro de responsáveis e pacientes.
    * `POST api/pacientes`: Cadastro de pacientes.
    * `GET api/pacientes`: Listagem de pacientes.
    * `GET api/pacientes/{id}`: Detalhes de um paciente.
    * `PUT api/pacientes/{id}`: Atualização de um paciente.
    * `DELETE api/pacientes/{id}`: Exclusão de um paciente.
    * `POST api/remedios`: Cadastro de remédios.
    * `GET api/remedios`: Listagem de remédios.
    * `PUT api/remedios/{id}`: Atualização de um remédio.
    * `DELETE api/remedios/{id}`: Exclusão de um remédio.
    * `POST api/pacientes/{id}/remedios`: Associação de um remédio a um paciente.
    * `GET api/pacientes/{id}/remedios`: Listagem de remédios associados a um paciente.
    * `DELETE api/pacientes/{id}/remedios/{remedioId}`: Remoção de um remédio de um paciente.
    * `POST api/horarios`: Cadastro de horários.
    * `GET api/horarios`: Listagem de horários.
    * `PUT api/horarios/{id}`: Atualização de um horário.
    * `DELETE api/horarios/{id}`: Exclusão de um horário.
    * `GET api/pacientes/{id}/horários`: Listagem de horários associados a um paciente.
    * `GET api/alertas`: Listagem de alertas.
    * `GET api/alertas/{id}`: Detalhes de um alerta.
    * `PUT api/alertas/{id}`: Atualização de um alerta.
    * `DELETE api/alertas/{id}`: Exclusão de um alerta.
    * `POST api/alertas/{id}/confirmar`: Confirmar o alerta.

---

### 🔹 Etapa 4 (Backend) — Tratamento de erros

* Criar modelo de erro consistente
* Usar HTTP status corretos
* Tratar:

  * parâmetros inválidos
  * datas mal formatadas
  * API key ausente ou inválida

---

### 🔹 Etapa 5 (Backend) — Documentação

* Configurar Swagger / OpenAPI
* Documentar:

  * endpoints
  * parâmetros
  * exemplos de resposta
* Garantir acesso via navegador

---

### 🔹 Etapa 6 (Frontend) — Estrutura do projeto

* Criar projeto Angular na versão 21 compatível com **Java 25**
* Usar NPM

---

### 🔹 Etapa 7 (Frontend) — Paginas - Login

* Criar uma página dedicada para o login
* A página deve possuir os campos de email e senha
* Botão para entrar na conta
* Link para criar novo cadastro

---

### 🔹 Etapa 8 (Frontend) — Paginas - Registrar

* Criar uma página dedicada para o registro de novo usuário
* A página deve possuir os campos de email e senha
* Botão para entrar realizar cadastro

---

### 🔹 Etapa 9 (Frontend) — Paginas - Pacientes

* Criar uma página dedicada para o gerenciamento de pacientes
* A página deve possuir a listagem de pacientes cadastrados
* A página deve possuir a funcionalidade de cadastrar um novo paciente com: nome e data de nacimento
* Selecionando um paciente deve ser possível vincular o paciente com os medicamentos
* Vinculando o paciente com os medicamentos, será possível escolher horários com a frequência (Diário / Semanal)
* Será possível adicionar e remover os medicamentos e horários dos pacientes

---

### 🔹 Etapa 10 (Frontend) — Paginas - Remedios

* Criar uma página dedicada para o gerenciamento de medicamentos
* A página deve possuir a listagem dos medicamentos
* A página deve possuir a funcionalidade de cadastrar um novo medicamento com: nome, dosagem e observações
* Será possível adicionar, remover e editar os medicamentos

---

### 🔹 Etapa 11 (Frontend) — Paginas - Alertas

* Criar uma página dedicada para o gerenciamento de alertas
* A página deve possuir a listagem dos alertas dos pacientes
* Quando for o horário da medicação deve atualizar com um novo alerta
* No horário do alerta a página deve emitir um alerta sonoro
* O usuário poderá confirmar o alerta
* O alerta terá os seguintes status TOMADO(layout verde), NÃO TOMADO(layout vermelho) E PENDENTE (layout amarelo)
* O alerta inicia com o status PENDENTE, o usuário confirmando o alerta, o mesmo vai para o status TOMADO
* Se o usuário não confirma o alerta em até 10 minutos, automáticamente o alerta muda para o status NÃO TOMADO

---

### 🔹 Etapa 8 (Frontend) — Paginas - Editar Perfiç

* Criar uma página dedicada para a edição do perfil
* A página deve possuir os campos de email e senha
* Botão para salvar as alterações

---

## ✅ Critérios de aceitação

A implementação será considerada concluída quando:

* A aplicação backend rodar corretamente em **Java 25**
* A aplicação frontend rodar corretamente em **Angular 21**
* Os endpoints estiverem funcionais
* Todos os parâmetros documentados funcionarem
* Integração entre backend e frontend funcional com todos os serviços
* Estrutura do banco de dados criada automaticamente
* Swagger estiver acessível

---

## 🔁 Checkpoints obrigatórios

Ao final de **cada etapa**:

* Descreva o que foi feito
* Liste os arquivos criados ou alterados
* Indique claramente o próximo passo

Avance automaticamente apenas se não houver inconsistências evidentes.

---