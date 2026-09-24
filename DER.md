# Diagrama Entidade-Relacionamento

O modelo abaixo representa o banco do ATENDE PVH.

```mermaid
erDiagram
    PESSOAS ||--o| USUARIOS : possui
    USUARIOS ||--o| ATENDENTES : representa
    SERVICOS ||--o{ TIPOS_ATENDIMENTO : possui
    SERVICOS ||--o| FILAS : possui
    PESSOAS ||--o{ SENHAS : retira
    SERVICOS ||--o{ SENHAS : classifica
    TIPOS_ATENDIMENTO ||--o{ SENHAS : detalha
    FILAS ||--o{ SENHAS : organiza
    PESSOAS ||--o{ AGENDAMENTOS : realiza
    SERVICOS ||--o{ AGENDAMENTOS : seleciona
    TIPOS_ATENDIMENTO ||--o{ AGENDAMENTOS : define
    SENHAS ||--o| ATENDIMENTOS : gera
    ATENDENTES ||--o{ ATENDIMENTOS : realiza
    GUICHES ||--o{ ATENDIMENTOS : recebe
    SENHAS ||--o{ CHAMADAS : chamada
    ATENDENTES ||--o{ CHAMADAS : realiza
    GUICHES ||--o{ CHAMADAS : utiliza

    PESSOAS {
        int id_pessoa PK
        varchar nome_completo
        varchar cpf UK
        date data_nascimento
        varchar telefone
        varchar email UK
        timestamp data_cadastro
        boolean ativo
    }

    USUARIOS {
        int id_usuario PK
        int id_pessoa FK
        varchar login UK
        text senha_hash
        varchar tipo_usuario
        boolean ativo
        timestamp data_criacao
    }

    ATENDENTES {
        int id_atendente PK
        int id_usuario FK
        varchar matricula UK
        varchar cargo
        boolean ativo
    }

    SERVICOS {
        int id_servico PK
        varchar nome
        varchar sigla UK
        text descricao
        boolean ativo
    }

    TIPOS_ATENDIMENTO {
        int id_tipo_atendimento PK
        int id_servico FK
        varchar nome
        text descricao
        boolean ativo
    }

    FILAS {
        int id_fila PK
        int id_servico FK
        varchar nome
        text descricao
        boolean ativo
    }

    GUICHES {
        int id_guiche PK
        int numero UK
        varchar descricao
        boolean ativo
    }

    SENHAS {
        int id_senha PK
        int id_pessoa FK
        int id_servico FK
        int id_tipo_atendimento FK
        int id_fila FK
        int numero
        varchar codigo UK
        date data_senha
        timestamp hora_emissao
        varchar status
        boolean prioridade
    }

    AGENDAMENTOS {
        int id_agendamento PK
        int id_pessoa FK
        int id_servico FK
        int id_tipo_atendimento FK
        date data_agendamento
        time hora_agendamento
        varchar protocolo UK
        varchar status
        text observacoes
    }

    ATENDIMENTOS {
        int id_atendimento PK
        int id_senha FK
        int id_atendente FK
        int id_guiche FK
        timestamp data_chamada
        timestamp inicio_atendimento
        timestamp fim_atendimento
        varchar status
        text observacoes
    }

    CHAMADAS {
        int id_chamada PK
        int id_senha FK
        int id_atendente FK
        int id_guiche FK
        timestamp data_chamada
        int numero_chamada
    }
```

## Relacionamentos principais

### Pessoa → Usuário
Uma pessoa pode possuir uma conta de acesso. A relação é 1:0..1.

### Usuário → Atendente
Um usuário pode representar um atendente. A relação é 1:0..1.

### Serviço → Tipo de atendimento
Um serviço possui vários tipos de atendimento.

Exemplo:

```text
Nota Fiscal de Serviço
├── Emissão/consulta de NFS-e
├── Cancelamento de nota fiscal
├── Correção de nota fiscal
└── Dúvidas sobre NFS-e
```

### Pessoa → Senha
Um cidadão pode retirar várias senhas ao longo do tempo.

### Senha → Atendimento
Uma senha pode originar um atendimento.

### Atendente → Atendimento
Um atendente realiza vários atendimentos.

### Guichê → Atendimento
Um guichê recebe vários atendimentos ao longo do dia.

### Senha → Chamadas
Uma senha pode ser chamada mais de uma vez, permitindo registrar o histórico de chamadas.
