## Para acessar o MySQL

Abrir o MySQL Client

## Para ver todos os BD no servidor

```SQL
SHOW DATABASES;
```

## Para criar um banco de dados

```SQL
CREATE DATABASE SUPERMERCADO;
```

## Para ativar uma DB

```SQL
USE SUPERMERCADO;
```

## Criar uma tabela

```SQL
CREATE TABLE Estoque (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nome_produto VARCHAR(255) NOT NULL,
    categoria_produto VARCHAR(100),
    quantidade INT NOT NULL,
    preco_unitario DECIMAL(10, 2) NOT NULL,
    data_entrada DATE NOT NULL,
    data_validade DATE,
    fornecedor VARCHAR(255)
);
```

## Para inserir dados na tabela

```SQL
INSERT INTO Estoque (nome_produto, categoria_produto, quantidade, preco_unitario, data_entrada, data_validade, fornecedor)
VALUES
('Arroz', 'Grãos', 120, 5.50, '2024-09-28', NULL, 'Fornecedor ABC'),
('Feijão', 'Grãos', 80, 7.20, '2024-09-15', '2025-03-15', 'Fornecedor XYZ'),
('Óleo de Soja', 'Óleos', 60, 6.50, '2024-09-10', '2025-01-01', 'Fornecedor DEF'),
('Macarrão', 'Massas', 200, 3.80, '2024-09-20', '2025-06-20', 'Fornecedor LMN'),
('Açúcar', 'Adoçantes', 150, 4.10, '2024-09-18', NULL, 'Fornecedor OPQ');
```

## Para ver a tabela toda

```SQL
SELECT * FROM Estoque;
```

## Selecionar alguns elementos da tabela

```SQL
/*Seleciona o nome do produto na tabela*/
SELECT nome_produto FROM Estoque;
/*Seleciona o produto na tabela com uma condição mais refinada*/
SELECT quantidade FROM Estoque WHERE quantidade > 100 AND categoria_produto = 'Grãos';
/*Obtem o total de produtos por categoria*/
SELECT categoria_produto, SUM(quantidade) AS total_produtos 
FROM Estoque 
GROUP BY categoria_produto;
```

## Buscar um item específico

```SQL
/*Seleciona o nome do produto na tabela com uma condição*/
SELECT nome_produto FROM Estoque WHERE nome_produto = 'Arroz';
```

## Ordenar a tabela de forma ascendente e descentente da quantidade de itens do seu estoque.

```SQL
/*Do menor para o maior*/
SELECT * FROM Estoque
ORDER BY quantidade ASC;

/*Do maior para o menor*/
SELECT * FROM Estoque
ORDER BY quantidade DESC;
```

## Atualize a quantidade de 3 itens do seu estoque.

```SQL
UPDATE Estoque
SET quantidade = CASE
    WHEN nome_produto = 'Arroz' THEN 150
    WHEN nome_produto = 'Feijão' THEN 250
    WHEN nome_produto = 'Óleo de Soja' THEN 25
    ELSE quantidade
END
WHERE nome_produto IN('Arroz', 'Feijão', 'Óleo de Soja');
```

## Atualize vários registros do seu estoque.

```SQL
UPDATE Estoque
SET preco_unitario = CASE 
    WHEN nome_produto = 'Arroz' THEN 6.00
    WHEN nome_produto = 'Feijão' THEN 8.50
    WHEN nome_produto = 'Óleo de Soja' THEN 7.00
    WHEN nome_produto = 'Macarrão' THEN 4.50
    WHEN nome_produto = 'Açúcar' THEN 4.20
    ELSE preco_unitario 
END
WHERE nome_produto IN ('Arroz', 'Feijão', 'Óleo de Soja', 'Macarrão', 'Açúcar');
```

## Criar uma tabela com os endereços dos fornecedores.

```SQL
CREATE TABLE Fornecedores (
    id_fornecedor INT AUTO_INCREMENT PRIMARY KEY,
    nome_fornecedor VARCHAR(100) NOT NULL,
    endereco VARCHAR(255),
    cidade VARCHAR(100),
    estado VARCHAR(100),
    cep VARCHAR(10)
);
```


## Populando a tabela

```SQL
INSERT INTO Fornecedores (nome_fornecedor, endereco, cidade, estado, cep)
VALUES
    ('Fornecedor A', 'Rua Exemplo, 123', 'São Paulo', 'SP', '01000-000'),
    ('Fornecedor B', 'Avenida Teste, 456', 'Rio de Janeiro', 'RJ', '20000-000'),
    ('Fornecedor C', 'Travessa Modelo, 789', 'Belo Horizonte', 'MG', '30000-000'),
    ('Fornecedor D', 'Rua do Mercado, 321', 'Curitiba', 'PR', '80000-000'),
    ('Fornecedor E', 'Avenida Brasil, 654', 'Fortaleza', 'CE', '60000-000'),
    ('Fornecedor F', 'Rua das Flores, 987', 'Salvador', 'BA', '40000-000'),
    ('Fornecedor G', 'Praça Central, 159', 'Manaus', 'AM', '69000-000'),
    ('Fornecedor H', 'Rua da Paz, 753', 'Recife', 'PE', '50000-000'),
    ('Fornecedor I', 'Avenida do Sol, 258', 'Porto Alegre', 'RS', '90000-000'),
    ('Fornecedor J', 'Rua das Árvores, 369', 'Natal', 'RN', '59000-000');
```

## Adicione uma nova coluna de endereço de emails destes fornecedores.

```SQL
/*Altera a tabela adicionando a coluna de e-mail*/
ALTER TABLE Fornecedores
ADD COLUMN email VARCHAR(100);


/*Adicionando valores para essa coluna*/
UPDATE Fornecedores
SET email = CASE 
    WHEN nome_fornecedor = 'Fornecedor A' THEN 'fornecedorA@example.com'
    WHEN nome_fornecedor = 'Fornecedor B' THEN 'fornecedorB@example.com'
    WHEN nome_fornecedor = 'Fornecedor C' THEN 'fornecedorC@example.com'
    WHEN nome_fornecedor = 'Fornecedor D' THEN 'fornecedorD@example.com'
    WHEN nome_fornecedor = 'Fornecedor E' THEN 'fornecedorE@example.com'
    WHEN nome_fornecedor = 'Fornecedor F' THEN 'fornecedorF@example.com'
    WHEN nome_fornecedor = 'Fornecedor G' THEN 'fornecedorG@example.com'
    WHEN nome_fornecedor = 'Fornecedor H' THEN 'fornecedorH@example.com'
    WHEN nome_fornecedor = 'Fornecedor I' THEN 'fornecedorI@example.com'
    WHEN nome_fornecedor = 'Fornecedor J' THEN 'fornecedorJ@example.com'
END;
```