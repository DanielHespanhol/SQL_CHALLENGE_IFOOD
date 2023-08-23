# SQL_CHALLENGE_IFOOD

# Banco de Dados E-commerce

Este repositório contém um banco de dados projetado para atender às necessidades de um sistema de comércio eletrônico. As tabelas foram criadas seguindo as melhores práticas de modelagem de banco de dados relacional, incluindo chaves primárias, chaves estrangeiras, índices e relacionamentos apropriados. O banco também já está populado com dados de teste para permitir o uso imediato.

## Tabelas Principais

### Tabela `product`
Esta tabela contém informações sobre os produtos disponíveis no catálogo, incluindo nome, descrição, preço, categoria, e outros detalhes relevantes.

```sql
CREATE TABLE product (
    product_id INT PRIMARY KEY,
    product_name VARCHAR(255) NOT NULL,
    product_description TEXT,
    product_price DECIMAL(10, 2) NOT NULL,
    product_category VARCHAR(50),
    -- Outros campos relevantes
);
```

### Tabela `stock`
A tabela `stock` armazena informações sobre a localização dos estoques. Isso é importante para o controle de inventário.

```sql
CREATE TABLE stock (
    stock_id INT PRIMARY KEY,
    stock_location VARCHAR(255) NOT NULL,
    -- Outros campos relevantes
);
```

### Tabela `product_stock`
Esta tabela faz o relacionamento entre produtos e locais de estoque, indicando a quantidade existente em cada local para cada produto.

```sql
CREATE TABLE product_stock (
    product_id INT,
    stock_id INT,
    quantity INT,
    PRIMARY KEY (product_id, stock_id),
    FOREIGN KEY (product_id) REFERENCES product(product_id),
    FOREIGN KEY (stock_id) REFERENCES stock(stock_id)
);
```

### Tabela `supplier`
A tabela `supplier` contém informações sobre os fornecedores que abastecem o estoque de produtos.

```sql
CREATE TABLE supplier (
    supplier_id INT PRIMARY KEY,
    supplier_name VARCHAR(255) NOT NULL,
    -- Outros campos relevantes
);
```

### Tabela `product_supplier`
Esta tabela relaciona produtos aos seus respectivos fornecedores.

```sql
CREATE TABLE product_supplier (
    product_id INT,
    supplier_id INT,
    PRIMARY KEY (product_id, supplier_id),
    FOREIGN KEY (product_id) REFERENCES product(product_id),
    FOREIGN KEY (supplier_id) REFERENCES supplier(supplier_id)
);
```

### Tabela `seller`
A tabela `seller` contém informações sobre os vendedores cadastrados na plataforma.

```sql
CREATE TABLE seller (
    seller_id INT PRIMARY KEY,
    seller_name VARCHAR(255) NOT NULL,
    -- Outros campos relevantes
);
```

### Tabela `product_seller`
Esta tabela relaciona produtos aos vendedores que os comercializam.

```sql
CREATE TABLE product_seller (
    product_id INT,
    seller_id INT,
    PRIMARY KEY (product_id, seller_id),
    FOREIGN KEY (product_id) REFERENCES product(product_id),
    FOREIGN KEY (seller_id) REFERENCES seller(seller_id)
);
```

### Tabela `customer`
A tabela `customer` armazena informações sobre os clientes que realizam compras na plataforma.

```sql
CREATE TABLE customer (
    customer_id INT PRIMARY KEY,
    customer_name VARCHAR(255) NOT NULL,
    -- Outros campos relevantes
);
```

### Tabela `orders`
Esta tabela registra os pedidos realizados pelos clientes.

```sql
CREATE TABLE orders (
    orders_id INT PRIMARY KEY,
    customer_id INT,
    order_date DATE NOT NULL,
    -- Outros campos relevantes
    FOREIGN KEY (customer_id) REFERENCES customer(customer_id)
);
```

### Tabela `payment`
A tabela `payment` armazena as formas de pagamento disponíveis para os pedidos.

```sql
CREATE TABLE payment (
    payment_id INT PRIMARY KEY,
    payment_method VARCHAR(50) NOT NULL,
    -- Outros campos relevantes
);
```

### Tabela `product_orders`
Esta tabela relaciona produtos aos pedidos, indicando a quantidade adquirida em cada pedido.

```sql
CREATE TABLE product_orders (
    product_id INT,
    orders_id INT,
    product_orders_quantity INT,
    PRIMARY KEY (product_id, orders_id),
    FOREIGN KEY (product_id) REFERENCES product(product_id),
    FOREIGN KEY (orders_id) REFERENCES orders(orders_id)
);
```

## Configuração Inicial

Para começar a usar este banco de dados, siga os passos abaixo:

1. **Execute o Script SQL**: Execute o script SQL fornecido neste repositório para criar toda a estrutura do banco de dados e popular as tabelas com dados de teste.

2. **Consulta e Inserção de Dados**: Uma vez criado, o banco já estará populado e pronto para consultas e inserções. Você pode começar a realizar consultas e inserir dados imediatamente.

## Exemplos de Consultas SQL

Aqui estão alguns exemplos de consultas SQL que você pode executar neste banco de dados:

- Buscar todos os produtos:

```sql
SELECT * FROM product;
```

- Buscar produtos por categoria:

```sql
SELECT * FROM product WHERE product_category = 'Relógios';
```

- Buscar quantidade em estoque por produto/local:

```sql
SELECT product_id, stock_id, quantity FROM product_stock;
```

- Buscar produtos associados a um pedido:

```sql
SELECT p.product_name, po.product_orders_quantity 
FROM product as p
JOIN product_orders as po ON p.product_id = po.product_id
WHERE po.orders_id = 134;
```

## Considerações Finais

Este banco de dados foi projetado com base em um planejamento e modelagem conceitual cuidadosa. Foram aplicadas boas práticas de modelagem relacional, e o banco está pronto para ser usado em um sistema de comércio eletrônico.

Lembre-se de que este é um modelo inicial e que você pode personalizá-lo e adicionar recursos adicionais conforme necessário, como transações e segurança.

O SGBD MySQL foi escolhido devido ao seu suporte à modelagem relacional, desempenho e facilidade de uso. Sinta-se à vontade para utilizar outros sistemas de gerenciamento de banco de dados se preferir.

Divirta-se explorando e utilizando este banco de dados para construir seu sistema de comércio eletrônico!
