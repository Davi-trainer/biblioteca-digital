# 📚 Biblioteca Virtual

![Java](https://img.shields.io/badge/Java-21-orange?logo=openjdk&logoColor=white)
![Status](https://img.shields.io/badge/Status-Em%20desenvolvimento-yellow)
![License](https://img.shields.io/badge/License-MIT-green)
![Academic](https://img.shields.io/badge/Projeto-A3%20Acadêmico-blue)

Sistema de **Biblioteca Virtual** desenvolvido como projeto acadêmico **A3** da disciplina de **Programação e Algoritmos com Java**, aplicando conceitos de programação orientada a objetos, estruturas de dados, persistência de informações e regras de negócio no gerenciamento de uma biblioteca.

---

## 📑 Sumário

- [Sobre o projeto](#-sobre-o-projeto)
- [Objetivos](#-objetivos)
- [Funcionalidades](#️-funcionalidades)
- [Sistema de planos](#-sistema-de-planos)
- [Catálogo de livros](#-catálogo-de-livros)
- [Sistema de empréstimos](#-sistema-de-empréstimos)
- [Controle de multas](#-controle-de-multas)
- [Biblioteca 100% digital](#-biblioteca-100-digital)
- [Painel administrativo](#️-painel-administrativo)
- [Banco de dados](#️-banco-de-dados)
- [Arquitetura](#-arquitetura)
- [Segurança](#-segurança)
- [Validações](#-validações)
- [Fluxo geral do sistema](#-fluxo-geral-do-sistema)
- [Tecnologias](#-tecnologias)
- [Requisitos](#-requisitos)
- [Estrutura do projeto](#-estrutura-prevista-do-projeto)
- [Como executar](#️-como-executar)
- [Fluxo de desenvolvimento (Git)](#-git-e-fluxo-de-desenvolvimento)
- [Colaboradores](#-colaboradores)
- [Status do projeto](#-status-do-projeto)
- [Licença](#-licença)

---

## 📖 Sobre o projeto

A Biblioteca Virtual é um sistema para gerenciamento de livros, usuários, planos de acesso e empréstimos. Usuários podem se cadastrar, contratar um plano de acesso e consultar o acervo disponível; administradores gerenciam o catálogo e a base de usuários.

O projeto contempla dois perfis de utilização:

| Perfil | Descrição |
|---|---|
| 👤 **Usuário** | Consulta o catálogo, contrata planos e realiza empréstimos |
| 🛠️ **Administrador** | Gerencia livros, usuários, planos e empréstimos |

> A aplicação poderá operar com **empréstimos físicos**, um modelo **100% digital**, ou um modelo híbrido — a definição final depende dos requisitos da equipe.

---

## 🎯 Objetivos

**Objetivo geral:** desenvolver um sistema de biblioteca em **Java**, aplicando os conhecimentos da disciplina de Programação e Algoritmos.

**Objetivos específicos:**

- Aplicar programação orientada a objetos na modelagem do sistema;
- Implementar cadastro de usuários e catálogo de livros;
- Controlar planos de acesso, sua validade e contratação;
- Implementar área administrativa e regras de empréstimo;
- Controlar prazos de devolução e calcular multas por atraso;
- Aplicar validações cadastrais e boas práticas de desenvolvimento;
- Utilizar Git e GitHub em fluxo de trabalho colaborativo.

---

## ⚙️ Funcionalidades

### 👤 Área do usuário

- Criar conta e realizar login;
- Consultar e pesquisar o catálogo de livros;
- Visualizar detalhes e disponibilidade de um livro;
- Escolher, contratar e acompanhar o status/validade de um plano;
- Consultar empréstimos, prazos de devolução e multas;
- Acessar conteúdo digital, quando esse modelo for adotado.

---

## 💳 Sistema de planos

Cada usuário pode possuir um plano de acesso associado à conta. O sistema verifica automaticamente se o plano está:

- ✅ **Ativo**
- ⚠️ **Próximo do vencimento**
- ❌ **Expirado**

```text
Usuário → Plano → Data de início → Data de vencimento → Plano válido?
                                                              ├── Sim → Acesso permitido
                                                              └── Não → Acesso bloqueado
```

O acesso a funcionalidades restritas depende do estado atual do plano.

### 💰 Contratação do plano

Durante a contratação, o sistema poderá solicitar dados de validação cadastral e pagamento (CPF, CEP, dados de pagamento).

> ⚠️ **Segurança:** o sistema não armazena dados completos de cartão de crédito no banco de dados. Em uma implementação real, o pagamento seria processado por um gateway especializado (com tokenização); para fins acadêmicos, poderão ser usados dados fictícios/simulados.

---

## 📚 Catálogo de livros

| Campo | Descrição |
|---|---|
| ID | Identificador único |
| Título | Nome do livro |
| Autor | Autor da obra |
| ISBN | Identificação do livro |
| Categoria | Categoria/gênero |
| Ano | Ano de publicação |
| Editora | Editora responsável |
| Disponibilidade | Disponível ou indisponível |
| Tipo | Físico ou digital |

O catálogo permite pesquisa e consulta das obras disponíveis.

---

## 📦 Sistema de empréstimos

Para livros físicos, o sistema controla retirada, data do empréstimo, prazo e data de devolução, situação, atrasos e multas.

```text
Usuário → Seleciona livro → Disponível?
                               ├── Não → Solicitação recusada
                               └── Sim → Empréstimo criado → Prazo definido
                                          → Devolução → Verifica atraso → Multa, se aplicável
```

---

## 💸 Controle de multas

Quando há empréstimo físico, o sistema verifica automaticamente se a devolução ocorreu após o prazo:

```text
diasDeAtraso = dataDevolucao - dataLimite

se diasDeAtraso > 0:
    multa = diasDeAtraso × valorDiario
```

As regras definitivas de cálculo poderão ser ajustadas conforme os requisitos definidos pela equipe.

---

## 💻 Biblioteca 100% digital

Como alternativa ao empréstimo físico, o projeto pode adotar um modelo totalmente digital, em que:

- não há devolução física nem logística de entrega;
- o acesso ao conteúdo depende exclusivamente da validade do plano;
- não se aplica multa por atraso.

```text
Usuário → Plano ativo?
             ├── Não → Acesso negado
             └── Sim → Livro digital → Acesso permitido
```

A decisão entre biblioteca física, digital ou híbrida será definida durante a implementação.

---

## 🛠️ Painel administrativo

O administrador gerencia:

- **Livros:** cadastrar, alterar, remover e consultar;
- **Usuários:** cadastrar, alterar e consultar;
- **Planos:** gerenciar, consultar ativos e expirados;
- **Empréstimos:** gerenciar, consultar devoluções e multas;
- **Acervo:** gerenciar disponibilidade dos livros.

```text
Administrador → Autenticação → Painel Administrativo
                                    ├── Usuários
                                    ├── Livros
                                    ├── Planos
                                    ├── Empréstimos
                                    ├── Devoluções
                                    └── Multas
```

---

## 🗄️ Banco de dados

Estrutura conceitual prevista:

```text
USUARIO ──── PLANO
        └─── EMPRESTIMO ──── LIVRO

ADMINISTRADOR ──── GERENCIAMENTO
```

**Entidades previstas:** `Usuario`, `Administrador`, `Livro`, `Plano`, `Pagamento`, `Emprestimo`, `Multa`.

A estrutura definitiva será refinada durante o desenvolvimento.

---

## 🧱 Arquitetura

O projeto é desenvolvido em **Java**, com conceitos de **Programação Orientada a Objetos**: classes, encapsulamento, herança, polimorfismo, abstração, interfaces, collections, tratamento de exceções, validação de dados e separação de responsabilidades em camadas.

```text
src/
├── model/
│   ├── Usuario.java
│   ├── Administrador.java
│   ├── Livro.java
│   ├── Plano.java
│   ├── Emprestimo.java
│   └── Multa.java
├── service/
│   ├── UsuarioService.java
│   ├── LivroService.java
│   ├── PlanoService.java
│   └── EmprestimoService.java
├── repository/
│   ├── UsuarioRepository.java
│   ├── LivroRepository.java
│   └── PlanoRepository.java
└── Main.java
```

---

## 🔐 Segurança

Mesmo sendo um projeto acadêmico, algumas práticas de segurança serão observadas:

- **Dados pessoais:** informações como CPF são tratadas como dados sensíveis e usadas apenas quando necessárias às regras do sistema;
- **Senhas:** nunca armazenadas em texto puro — o correto é utilizar uma função de hash apropriada;
- **Pagamentos:** dados completos de cartão não são armazenados pela aplicação.

```text
Correto:   Aplicação → Gateway de pagamento → Processador de pagamento
Incorreto: Aplicação → Banco de dados → Número completo do cartão
```

---

## 🧪 Validações

- CPF e CEP em formato válido;
- Campos obrigatórios preenchidos e e-mail válido;
- Senha com requisitos mínimos de segurança;
- Existência de usuário, livro, plano e empréstimo consultados;
- Plano válido ou expirado;
- Disponibilidade do livro;
- Devolução dentro ou fora do prazo.

---

## 🔄 Fluxo geral do sistema

```text
                         ┌───────┐
                         │ LOGIN │
                         └───┬───┘
                 ┌───────────┴───────────┐
                 ▼                       ▼
           ┌──────────┐           ┌───────────────┐
           │ USUÁRIO  │           │ ADMINISTRADOR │
           └────┬─────┘           └───────┬───────┘
                ▼                         ▼
         ┌─────────────┐           ┌──────────────┐
         │ Plano ativo?│           │ Gerenciar    │
         └──────┬──────┘           │ sistema      │
        ┌───────┴───────┐          └──────────────┘
        ▼               ▼
      SIM              NÃO
        │               │
        ▼               ▼
  ┌────────────┐   ┌───────────┐
  │Acesso a    │   │Contratar  │
  │livros      │   │plano      │
  └─────┬──────┘   └─────┬─────┘
        ▼                ▼
  ┌────────────┐   ┌───────────┐
  │Empréstimo  │   │Pagamento  │
  └─────┬──────┘   └───────────┘
        ▼
  ┌────────────┐   ┌────────────┐
  │Devolução   │──▶│Verificar   │
  └────────────┘   │atraso      │
                    └──────┬─────┘
                    ┌──────┴──────┐
                    ▼             ▼
                  NÃO            SIM
                    │             │
                    ▼             ▼
                 Concluído   Calcular multa
```

---

## 🚀 Tecnologias

- **Java**
- **Git** e **GitHub**
- **Banco de dados / SQL**, caso utilizado na implementação
- **IDE compatível com Java**

Tecnologias adicionais poderão ser incluídas conforme a arquitetura definitiva do sistema.

---

## 📋 Requisitos

### Funcionais

| ID | Requisito | Descrição |
|---|---|---|
| RF01 | Cadastro de usuário | O sistema deve permitir o cadastro de novos usuários |
| RF02 | Autenticação | Usuários autenticados acessam suas funcionalidades |
| RF03 | Cadastro de livros | O administrador pode cadastrar novos livros |
| RF04 | Gerenciamento de livros | O administrador pode consultar, alterar e remover livros |
| RF05 | Consulta de livros | O usuário pode consultar o catálogo |
| RF06 | Gerenciamento de planos | O sistema permite contratação e controle de planos |
| RF07 | Validação do plano | O sistema verifica a validade antes de operações restritas |
| RF08 | Empréstimo | O usuário pode solicitar empréstimo de livros físicos (se implementado) |
| RF09 | Controle de prazo | O sistema registra o prazo de devolução |
| RF10 | Multa | O sistema identifica atrasos e calcula a multa |
| RF11 | Área administrativa | Funcionalidades exclusivas para administradores |
| RF12 | Pagamento | Fluxo de contratação com dados fictícios ou gateway apropriado |

### Não funcionais

| ID | Requisito | Descrição |
|---|---|---|
| RNF01 | Linguagem | Desenvolvido em **Java** |
| RNF02 | Segurança | Informações sensíveis não armazenadas de forma insegura |
| RNF03 | Persistência | Dados importantes mantidos após o encerramento da aplicação |
| RNF04 | Usabilidade | Fluxos simples e compreensíveis |
| RNF05 | Manutenibilidade | Código organizado para facilitar futuras alterações |
| RNF06 | Versionamento | Desenvolvimento com **Git** e **GitHub** |

---

## 📂 Estrutura prevista do projeto

```text
BibliotecaVirtual/
├── src/
│   ├── model/
│   ├── service/
│   ├── repository/
│   ├── controller/
│   └── Main.java
├── database/
│   └── schema.sql
├── docs/
│   ├── requisitos.md
│   └── diagramas/
├── tests/
├── .gitignore
├── LICENSE
├── README.md
└── pom.xml
```

> A estrutura poderá ser adaptada conforme as ferramentas e decisões técnicas da equipe.

---

## ▶️ Como executar

**Pré-requisitos:** Java JDK, Git, banco de dados configurado (se utilizado) e uma IDE compatível com Java.

```bash
# Verificar instalação do Java
java --version

# Clonar o repositório
git clone URL_DO_REPOSITORIO

# Entrar no diretório do projeto
cd BibliotecaVirtual
```

A forma de execução final dependerá da estrutura do projeto e da ferramenta de build utilizada.

---

## 🌿 Git e fluxo de desenvolvimento

Desenvolvimento colaborativo via GitHub, com branches de funcionalidade integradas à branch principal:

```text
main
 ├── feature/cadastro-usuarios
 ├── feature/catalogo-livros
 ├── feature/planos
 ├── feature/emprestimos
 └── feature/painel-admin
```

---

## 👥 Colaboradores

| Colaborador | GitHub |
|---|---|
| Davi Peres | [@Davi-trainer](https://github.com/Davi-trainer) |
| Melissa | [@melissasn](https://github.com/melissasn) |
| Hillo Silva | [@HilloSilvaDev](https://github.com/HilloSilvaDev) |
| Euriandes Jales | [@EuriandesJales](https://github.com/EuriandesJales) |

---

## 🎓 Projeto acadêmico

Desenvolvido como parte da avaliação **A3** da disciplina **Programação e Algoritmos com Java**, aplicando em um projeto prático conceitos de programação, modelagem, lógica, orientação a objetos, persistência de dados e desenvolvimento colaborativo.

---

## 📈 Status do projeto

🚧 **Em desenvolvimento**

- [ ] Estrutura inicial do projeto
- [ ] Modelagem das entidades
- [ ] Banco de dados
- [ ] Cadastro de usuários e autenticação
- [ ] Cadastro de livros e catálogo
- [ ] Sistema de planos e validação
- [ ] Sistema de pagamento
- [ ] Painel administrativo
- [ ] Empréstimos, devoluções e cálculo de multas
- [ ] Testes
- [ ] Documentação
- [ ] Apresentação final

---

## 📜 Licença

Este projeto está licenciado sob a **MIT License**. Consulte o arquivo [`LICENSE`](LICENSE) para o texto completo.

> Software desenvolvido exclusivamente para fins **acadêmicos e educacionais**, como parte do projeto A3 da disciplina de Programação e Algoritmos com Java.

---

<p align="center">
  Desenvolvido por <strong>Davi Peres · Melissa · Hillo Silva · Euriandes Jales</strong>
</p>

<p align="center">
  📚 Biblioteca Virtual — Projeto A3
</p>
