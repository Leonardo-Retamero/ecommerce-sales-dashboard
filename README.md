# E-commerce Sales Analytics Dashboard

### 📌 Visão Geral do Projeto
Este projeto tem como objetivo analisar o desempenho de um e-commerce a partir de uma base de dados contendo informações reais de vendas. A proposta é transformar dados brutos em insights relevantes que apoiem a tomada de decisão, utilizando técnicas de análise de dados, modelagem de dados, DAX e visualização no Power BI. Para isso, foi desenvolvido um dashboard interativo dividido em quatro páginas principais, cada uma focada em um aspecto estratégico do negócio. 

---

### 📊 Análise das Vendas
A página de Análise das Vendas apresenta indicadores de faturamento, volume de pedidos, tempo médio de envio, frete e avaliação média dos clientes que são acompanhados por indicadores complementares. Os gráficos apresentam insights sobre a receita ao longo do tempo (ano/mês), receita e frete médio por produto.

<img width="1409" height="793" alt="image" src="https://github.com/user-attachments/assets/e33b06c1-2bec-4ce9-90e0-2c0e58154214" />

- Receita ao longo do tempo (ano/mês): Permite identificar tendências de crescimento ou sazonalidade nas vendas, evidenciando períodos de alta e queda no faturamento.

- Receita por produto: Destaca os produtos mais relevantes para o faturamento e os produtos que menos vendem.

- Frete médio por produto: Possibilita avaliar o impacto logístico por produto, é possível identifacar que produtos mais caros tendem a ter o frete médio maior.

---

### 🌎 Análise por Estado
A página de Análise por Estado permite identificar diferenças regionais no comportamento de compra e na geração de receita. Os gráficos apresentam insights sobre o ticket e frete médio por estado, receita vs volume de pedidos e tempo médio de resposta ao cliente (dias).

<img width="1416" height="795" alt="image" src="https://github.com/user-attachments/assets/47723b18-4701-420a-a9af-276bf8009e0b" />

- Ticket médio por estado: Revela diferenças no valor médio das compras entre regiões, indicando mercados com maior poder de consumo.

- Frete médio por estado: Demonstra variações no custo logístico, podendo indicar regiões mais caras de atender.

- Receita vs volume de pedidos: Comparação entre os estados com maior receita e volume de pedidos.

---

### 🚚 Análise das Entregas
A Análise das Entregas avalia a eficiência logística, considerando prazos e qualidade do serviço. Os gráficos apresentam insights sobre o tempo médio de entrega por estado (dias), total de entregas fora do prazo por estado, volume de entregas no prazo vs atrasadas ao longo do tempo e taxa de entregas no prazo ao longo do tempo.

<img width="1441" height="806" alt="image" src="https://github.com/user-attachments/assets/49372eb4-9909-4797-994c-c1397621036a" />

- Tempo médio de entrega por estado: Mostra diferenças regionais na eficiência logística, identificando estados com maior tempo de entrega.

- Total de entregas fora do prazo por estado: Estados com maior volume de pedidos possuem mais entregas atrasados, indicando que a logística tem dificuldades em dar conta da demanda.

- Entregas no prazo vs atrasadas ao longo do tempo: Permite analisar a evolução da performance logística, identificando melhorias ou pioras ao longo do tempo.

- Taxa de entregas no prazo ao longo do tempo: Mede a qualidade do serviço logístico, indicando consistência e eficiência das entregas.

---

### 💳 Análise por Tipo de Pagamento
A Análise por Tipo de Pagamento explora as preferências dos clientes e o impacto dos meios de pagamento nas vendas. Os gráficos apresentam insights sobre o total de vendas por tipo de pagamento ao longo do tempo, ticket médio por tipo de pagamento e receita por tipo de pagamento e estado.

<img width="1480" height="825" alt="image" src="https://github.com/user-attachments/assets/6d3798ee-af5d-44c6-9d0f-b802784dd5bc" />

- Vendas por tipo de pagamento ao longo do tempo: Identifica tendências no uso dos meios de pagamento, mostrando mudanças no comportamento dos clientes.

- Ticket médio por tipo de pagamento: Revela quais métodos estão associados a compras de maior e menor valor.

- Receita por tipo de pagamento e estado: Permite analisar a receita pela distribuição geográfica dos meios de pagamento.

---

### 🛠️ Princípais Medidas DAX

### Ticket Médio
```dax
Ticket Médio: = 
DIVIDE(
    [Receita Total],
    DISTINCTCOUNT(pedidos[id_pedido])
)
```

### % Margem de Lucro

```dax
Margem Após Frete = SUM(itens_pedido[preço]) - [Frete]

% Margem = 
DIVIDE(
    [Margem Após Frete],
    SUM(itens_pedido[preço])
)
```
### Pedidos Cancelados

```dax
Pedidos Cancelados: = 
CALCULATE(
    DISTINCTCOUNT(pedidos[id_pedido]),
    pedidos[status_pedido] = "canceled"
)
```
### Taxa de Cancelamento

```dax
Taxa Cancelamento: = 
DIVIDE(
    [Pedidos Cancelados:],
    DISTINCTCOUNT(pedidos[id_pedido])
)
```

### Taxa de Entregas no Prazo

```dax
Taxa No Prazo: = 
DIVIDE(
    [Pedidos No Prazo],
    [Pedidos Entregues],
    0
)
```

### Entregas Fora do Prazo
```dax
Entregas Fora do Prazo: = 
CALCULATE(
    DISTINCTCOUNT(pedidos[id_pedido]),
    pedidos[status_entrega] = "Fora do Prazo"
)
```
