# Especificação Conceptual do Banco de Dados (MER)[cite: 2]

## 1. Entidades

* **CLIENTE:** Representa as pessoas físicas que utilizam os serviços de reserva e consumo no restaurante[cite: 1, 2].
* **RESERVA_MESA:** Registra a solicitação prévia de alocação de mesa efetuada por um cliente para um determinado dia e horário[cite: 1, 2].
* **MESA:** Representa os locais físicos disponíveis no restaurante para acomodação dos clientes[cite: 1, 2].
* **FUNCIONARIO:** Representa os colaboradores do restaurante encarregados do atendimento aos clientes[cite: 1, 2].
* **ATENDIMENTO:** Representa a comanda ativa referente à permanência e consumo dos clientes em uma mesa[cite: 1, 2].
* **PEDIDO_ITEM:** Registra os itens específicos solicitados e lançados durante um atendimento[cite: 1, 2].
* **ITEM_CARDAPIO:** Representa os produtos (comidas e bebidas) oferecidos pelo restaurante com seus respectivos preços[cite: 1, 2].
* **PAGAMENTO:** Registra as transações financeiras realizadas para a quitação do valor total de uma comanda[cite: 1, 2].

---

## 2. Relacionamentos e Cardinalidades

1. **[CLIENTE] (1,1) <Faz> (0,N) [RESERVA_MESA]**[cite: 1, 2]
   * **Explicação:** Um cliente pode realizar nenhuma ou várias reservas ao longo do tempo, mas cada reserva obrigatoriamente pertence a exatamente um cliente registrado[cite: 1, 2].

2. **[RESERVA_MESA] (0,1) <original> (0,1) [ATENDIMENTO]**[cite: 1, 2]
   * **Explicação:** Uma reserva pode dar origem a no máximo um atendimento presencial (ou nenhum, em caso de cancelamento/no-show). Um atendimento pode ter sido originado por uma reserva ou ser presencial sem reserva[cite: 1, 2].

3. **[MESA] (1,1) <Recebe> (0,N) [ATENDIMENTO]**[cite: 1, 2]
   * **Explicação:** Uma mesa pode receber vários atendimentos em horários e dias diferentes, mas cada atendimento ocorre em apenas uma mesa específica[cite: 1, 2].

4. **[FUNCIONARIO] (1,1) <atender> (0,N) [ATENDIMENTO]**[cite: 1, 2]
   * **Explicação:** Um funcionário (garçom) pode ser responsável por atender múltiplos atendimentos, mas cada atendimento possui um funcionário responsável[cite: 1, 2].

5. **[ATENDIMENTO] (1,1) <Gera> (0,N) [PEDIDO_ITEM]**[cite: 1, 2]
   * **Explicação:** Um atendimento gera nenhum ou múltiplos itens de pedido lançados na comanda. Cada pedido de item obrigatoriamente está associado a um único atendimento[cite: 1, 2].

6. **[ITEM_CARDAPIO] (1,1) <Refere> (0,N) [PEDIDO_ITEM]**[cite: 1, 2]
   * **Explicação:** Um item do cardápio pode estar referenciado em vários pedidos de itens em comandas distintas. Cada registro de pedido de item refere-se a exatamente um item do cardápio[cite: 1, 2].

7. **[ATENDIMENTO] (1,1) <Recebe> (1,N) [PAGAMENTO]**[cite: 1, 2]
   * **Explicação:** Um atendimento concluído pode ter um ou mais pagamentos registrados (ex: conta dividida entre clientes), sendo que cada pagamento é destinado a apenas um atendimento específico[cite: 1, 2].

---

## 3. Sugestão de Atributos

### CLIENTE
* `Cpf` (String) — **PK (Identificador Primário)**[cite: 1, 2]
* `Nome` (String)[cite: 1]
* `Telefones` (String array) — **Atributo Multivalorado**[cite: 1, 2]
* `Emails` (String array) — **Atributo Multivalorado**[cite: 1, 2]

### RESERVA_MESA
* `Cod Reserva` (int) — **PK (Identificador Primário)**[cite: 1, 2]
* `Data hora reserva` (datetime)[cite: 1]
* `Qtd pessoas` (int)[cite: 1]
* `Status` (String)[cite: 1]

### MESA
* `Num mesa` (int) — **PK (Identificador Primário)**[cite: 1, 2]
* `Capacidade` (int)[cite: 1]
* `Status` (String)[cite: 1]

### FUNCIONARIO
* `Cpf Fucionario` (String) — **PK (Identificador Primário)**[cite: 1, 2]
* `Nome` (String)[cite: 1]
* `Turno` (String)[cite: 1]
* `Cargo` (String)[cite: 1]

### ATENDIMENTO
* `Cod Comanda` (int) — **PK (Identificador Primário)**[cite: 1, 2]
* `Data hora abertura` (datetime)[cite: 1]
* `Data hora fechamento` (datetime)[cite: 1]
* `Valor total` (decimal) — **Atributo Derivado** (Soma dos valores subtotais dos itens do pedido)[cite: 1, 2]

### PEDIDO_ITEM
* `Cod pedido` (int) — **PK (Identificador Primário)**[cite: 1, 2]
* `Quantidade` (int)[cite: 1]
* `Observacao` (String)[cite: 1]
* `Hora pedido` (datetime)[cite: 1]
* `Valor subtotal` (decimal) — **Atributo Derivado** (`Quantidade` * `Preço unitario` do item)[cite: 1, 2]

### ITEM_CARDAPIO
* `Cod item` (int) — **PK (Identificador Primário)**[cite: 1, 2]
* `Nome item` (String)[cite: 1]
* `Categoria` (String)[cite: 1]
* `Preço unitario` (decimal)[cite: 1]

### PAGAMENTO
* `Cod pagamento` (int) — **PK (Identificador Primário)**[cite: 1, 2]
* `datahora` (datetime)[cite: 1]
* `Forma pagamento` (String)[cite: 1]
* `Valor` (decimal)[cite: 1]

---

## 4. Diagrama Entidade e Relacionamento (DER)

```mermaid
erDiagram
    CLIENTE {
        string Cpf PK
        string Nome
        string_array Telefones
        string_array Emails
    }

    RESERVA_MESA {
        int Cod_Reserva PK
        datetime Data_hora_reserva
        int Qtd_pessoas
        string Status
    }

    MESA {
        int Num_mesa PK
        int Capacidade
        string Status
    }

    FUNCIONARIO {
        string Cpf_Funcionario PK
        string Nome
        string Turno
        string Cargo
    }

    ATENDIMENTO {
        int Cod_Comanda PK
        datetime Data_hora_abertura
        datetime Data_hora_fechamento
        decimal Valor_total
    }

    PEDIDO_ITEM {
        int Cod_pedido PK
        int Quantidade
        string Observacao
        datetime Hora_pedido
        decimal Valor_subtotal
    }

    ITEM_CARDAPIO {
        int Cod_item PK
        string Nome_item
        string Categoria
        decimal Preco_unitario
    }

    PAGAMENTO {
        int Cod_pagamento PK
        datetime datahora
        string Forma_pagamento
        decimal Valor
    }

    CLIENTE ||--o{ RESERVA_MESA : "Faz"
    RESERVA_MESA o|--o| ATENDIMENTO : "original"
    MESA ||--o{ ATENDIMENTO : "Recebe"
    FUNCIONARIO ||--o{ ATENDIMENTO : "atender"
    ATENDIMENTO ||--o{ PEDIDO_ITEM : "Gera"
    ITEM_CARDAPIO ||--o{ PEDIDO_ITEM : "Refere"
    ATENDIMENTO ||--o{ PAGAMENTO : "Recebe"
