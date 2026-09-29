# Sistema de Gerenciamento de Atendimento e Reservas de Restaurante

## 1. Descrição do Minimundo
Este projeto consiste na modelagem de um banco de dados para a gestão operacional de um restaurante. O sistema visa resolver o controle e acompanhamento de reservas de mesas, ocupação presencial, atendimento por comanda, registro de pedidos de itens do cardápio e processamento de pagamentos[cite: 1, 2]. 

A aplicação otimiza o fluxo de trabalho dos funcionários, garante o histórico de consumo dos clientes e previne conflitos de horários na alocação das mesas[cite: 1, 2].

## 2. Regras de Negócio e Processos Principais

### Regras de Negócio
* Um cliente pode realizar cadastros de contato contendo múltiplos telefones e e-mails[cite: 1].
* Um cliente pode efetuar uma ou mais reservas de mesa em datas e horários distintos[cite: 1].
* As mesas possuem capacidades específicas de pessoas e status de ocupação (ex: Livre, Reservada, Ocupada)[cite: 1].
* Um atendimento é associado a uma comanda e vinculado a uma mesa e a um funcionário responsável[cite: 1].
* Um atendimento pode ser originado a partir de uma reserva prévia ou aberto diretamente no local[cite: 1].
* Durante o atendimento, podem ser registrados múltiplos itens de pedido vinculados ao cardápio[cite: 1].
* Cada item do pedido possui valor subtotal derivado da quantidade e do preço unitário do item[cite: 1].
* O valor total do atendimento é a soma dos subtotais dos itens solicitados[cite: 1].
* A comanda pode ser quitada através de um ou mais pagamentos (permitindo divisão de conta) em diferentes formas de pagamento[cite: 1].

### Processos Principais
1. **Gestão de Reservas:** Registro e atualização do status de reserva solicitada por um cliente[cite: 1].
2. **Abertura e Gestão de Atendimento:** Vinculação de uma comanda a uma mesa e a um funcionário no momento do atendimento[cite: 1].
3. **Lançamento de Pedidos:** Inclusão de itens do cardápio na comanda com quantidade e observações específicas[cite: 1].
4. **Fechamento e Pagamento:** Cálculo do valor total, registro do recebimento dos valores e finalização do atendimento[cite: 1].
