# Modelo de dados e regras de negócio

## Estados da senha

```text
AGUARDANDO
    ↓
CHAMANDO
    ↓
EM_ATENDIMENTO
    ↓
CONCLUIDA
```

Caminho alternativo:

```text
AGUARDANDO → CANCELADA
```

## Regras

1. Toda senha pertence a um cidadão.
2. Toda senha pertence a um serviço.
3. Toda senha possui um tipo de atendimento.
4. Todo serviço possui uma fila.
5. Uma senha não pode repetir o mesmo número dentro da mesma fila e data.
6. Uma senha pode gerar no máximo um registro principal de atendimento.
7. Um atendimento pode ter um atendente e um guichê.
8. Chamadas são registradas separadamente para manter histórico.
9. Agendamento possui protocolo único.
10. Usuários possuem tipos: cidadão, atendente ou administrador.
11. CPF e e-mail são únicos quando cadastrados.
12. Senhas são armazenadas como hash no campo `senha_hash`, nunca em texto puro.

## Consultas úteis

### Fila atual

```sql
SELECT * FROM vw_fila_atual;
```

### Atendimentos

```sql
SELECT * FROM vw_atendimentos;
```

### Painel de chamadas

```sql
SELECT * FROM vw_painel_chamadas;
```

### Histórico

```sql
SELECT * FROM vw_historico_cidadao;
```
