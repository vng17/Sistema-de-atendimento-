# ATENDE PVH

## Central de Atendimento ao Cidadão — Protótipo Acadêmico

Sistema acadêmico de gerenciamento de filas e atendimentos para uma central pública. O projeto permite que o cidadão escolha um serviço, retire ou agende uma senha, acompanhe sua posição e receba a chamada. Atendentes gerenciam a fila e administradores acompanham os indicadores.

> **Aviso:** este é um projeto acadêmico. Os serviços e nomes apresentados são exemplos para fins de demonstração e não representam necessariamente os serviços oficiais de qualquer órgão público.

## Objetivo

Demonstrar, em um único projeto, os conceitos de:

- Modelagem relacional;
- Chaves primárias e estrangeiras;
- Relacionamentos 1:N;
- Integridade referencial;
- Filas de atendimento;
- Cadastro de cidadãos e atendentes;
- Agendamento;
- Histórico de chamadas;
- Views para relatórios;
- Funções/procedures em PostgreSQL;
- Protótipo de interface responsivo;
- Gamificação/experiência de acompanhamento por posição e status.

## Funcionalidades

### Cidadão
- Cadastro e login;
- Escolha do serviço;
- Escolha do tipo de atendimento;
- Retirada de senha presencial/online;
- Agendamento;
- Acompanhamento da fila;
- Aviso de "Você é o próximo";
- Aviso de chamada e guichê;
- Histórico de atendimentos.

### Atendente
- Dashboard;
- Visualização da fila;
- Chamar próximo;
- Iniciar atendimento;
- Finalizar atendimento;
- Registro de observações;
- Associação com guichê.

### Administração
- Cadastro de pessoas;
- Cadastro de atendentes;
- Serviços e tipos de atendimento;
- Guichês;
- Atendimentos;
- Indicadores básicos.

### Painel de chamadas
- Senha chamada;
- Serviço;
- Guichê;
- Próximas senhas;
- Layout para televisão/tela grande.

## Tecnologias

- PostgreSQL
- pgAdmin 4
- HTML5
- CSS3
- JavaScript
- Git/GitHub
- Mermaid para o DER

## Estrutura do projeto

```text
ATENDE-PVH/
├── README.md
├── .gitignore
├── database/
│   ├── 01_schema.sql
│   ├── 02_functions.sql
│   ├── 03_views.sql
│   └── 04_seed.sql
├── docs/
│   ├── DER.md
│   └── MODELO.md
└── prototype/
    ├── index.html
    ├── style.css
    └── app.js
```

## Como criar o banco no pgAdmin

1. Abra o PostgreSQL no pgAdmin.
2. Crie um banco, por exemplo `atende_pvh`.
3. Abra o **Query Tool**.
4. Execute os arquivos nesta ordem:

```text
01_schema.sql
02_functions.sql
03_views.sql
04_seed.sql
```

A ordem é importante porque as funções e views dependem das tabelas.

## Contas de demonstração

| Perfil | Login | Senha |
|---|---|---|
| Cidadão | `cidadao@exemplo.com` | `123456` |
| Atendente | `1001` | `1234` |
| Administrador | `9000` | `admin` |

As credenciais acima são **somente para demonstração acadêmica**.

## Executar o protótipo

A pasta `prototype` não precisa de servidor para a demonstração básica.

Abra:

```text
prototype/index.html
```

ou publique a pasta no GitHub Pages.

O protótipo utiliza `localStorage` para simular os dados e demonstrar os fluxos antes da integração com o PostgreSQL.

## Modelo de dados

O banco foi dividido em entidades principais:

- `pessoas`
- `usuarios`
- `atendentes`
- `servicos`
- `tipos_atendimento`
- `filas`
- `guiches`
- `senhas`
- `agendamentos`
- `atendimentos`
- `chamadas`

Veja o [DER completo](docs/DER.md).

## Fluxo principal

```text
CIDADÃO
   ↓
LOGIN / CADASTRO
   ↓
ESCOLHA DO SERVIÇO
   ↓
TIPO DE ATENDIMENTO
   ↓
RETIRAR SENHA OU AGENDAR
   ↓
ACOMPANHAR FILA
   ↓
CHAMADA
   ↓
GUICHÊ
   ↓
ATENDIMENTO
   ↓
FINALIZAÇÃO
   ↓
HISTÓRICO
```

## Fluxo do atendente

```text
LOGIN
  ↓
DASHBOARD
  ↓
CHAMAR PRÓXIMO
  ↓
SENHA = CHAMANDO
  ↓
INICIAR ATENDIMENTO
  ↓
SENHA = EM_ATENDIMENTO
  ↓
FINALIZAR
  ↓
SENHA = CONCLUIDA
```

## Proposta de inovação

A inovação escolhida é a **inteligência de dados aplicada ao gerenciamento da fila**, usando informações de posição, tempo estimado, histórico de atendimentos e indicadores para melhorar a experiência do cidadão e permitir acompanhamento operacional.

A interface também possui elementos de engajamento, como posição na fila e estados de proximidade da chamada.

## Próxima etapa de integração

O protótipo atual funciona localmente. Para uma aplicação completa, a arquitetura recomendada é:

```text
Frontend (Lovable/React)
        ↓
API / Backend
        ↓
PostgreSQL
        ↓
Views + Functions + Tables
```

Não é recomendado conectar diretamente um frontend público ao PostgreSQL. A senha deve ser armazenada com hash e as operações devem passar por uma API/backend.

## Apresentação acadêmica

Na apresentação, o projeto pode ser demonstrado em quatro etapas:

1. Cidadão entra no sistema e escolhe um serviço.
2. Cidadão retira uma senha e acompanha sua posição.
3. Atendente chama a próxima senha e o painel mostra o guichê.
4. O atendimento é finalizado e passa para o histórico.

## Autores

Projeto acadêmico desenvolvido para a disciplina de Banco de Dados.

**Grupo:**
- Gustavo Nogueira
- Maria Clara Nogueira
- Vinícius Augusto
- Vitor Aluizio
