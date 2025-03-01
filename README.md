

Para listar todos os produtos que estão no estoque e suas quantidades:
SELECT * FROM product WHERE stockQuantity > 0;

Para filtrar os pedidos que estão marcados como 'Confirmado':
SELECT * FROM orders WHERE Order_status = 'Confirmado';

Para filtrar os fornecedores pelo nome social:
SELECT * FROM supplier ORDER BY SocialName;

Para recuperar os dados dos clientes relacionado aos pedidos:
SELECT c.idClient, c.Fname, c.Lname, o.idOrder, o.Order_status
FROM clients c
JOIN orders o ON c.idClient = o.idOrderClient;

Para mostrar a quantidade total de produtos vendidas por vendedor:
SELECT s.idSeller, s.SocialName, SUM(ps.prodQuantity) AS totalSold
FROM seller s
JOIN productSeller ps ON s.idSeller = ps.idPseller
GROUP BY s.idSeller, s.SocialName;

Lista os produtos armazenados em cada local, exibindo também as localizações:
SELECT p.Pname, sl.location
FROM storageLocation sl
JOIN product p ON sl.idLproduct = p.idProduct;

Mostra os detalhes dos pedidos, incluindo o status dos pagamentos e os métodos utilizados:
SELECT o.idOrder, o.Order_status, op.paymentMethod, op.paymentStatus
FROM orders o
JOIN OrderPayment op ON o.idOrder = op.idOrder;

Exibe os produtos fornecidos por cada fornecedor, incluindo a quantidade fornecida.:
SELECT s.SocialName, p.Pname, ps.quantity
FROM supplier s
JOIN producSupplier ps ON s.idSupplier = ps.idPsSuplier
JOIN product p ON ps.idPsProduct = p.idProduct;

Calcula o valor total dos pedidos confirmados agrupados por cliente:
SELECT c.idClient, c.Fname, c.Lname, SUM(o.totalValue) AS totalOrderValue
FROM clients c
JOIN orders o ON c.idClient = o.idOrderClient
WHERE o.Order_status = 'Confirmado'
GROUP BY c.idClient, c.Fname, c.Lname;

Exibe os produtos mais vendidos, ordenando pelos que possuem maiores quantidades vendidas:
SELECT p.Pname, SUM(po.poQuantity) AS totalSold
FROM product p
JOIN productOrder po ON p.idProduct = po.idPOproduct
GROUP BY p.Pname
ORDER BY totalSold;

Identifica clientes que não possuem nenhum pedido associado no banco de dados:
SELECT c.idClient, c.Fname, c.Lname
FROM clients c
LEFT JOIN orders o ON c.idClient = o.idOrderClient
WHERE o.idOrderClient IS NULL;

Calcula o valor total dos produtos vendidos por cada vendedor, multiplicando a quantidade pelo preço:
SELECT s.idSeller, s.SocialName, SUM(ps.prodQuantity * p.price) AS totalValueSold
FROM seller s
JOIN productSeller ps ON s.idSeller = ps.idPseller
JOIN product p ON ps.idProduct = p.idProduct
GROUP BY s.idSeller, s.SocialName;

Lista os produtos armazenados em cada local de armazenamento e a quantidade total correspondente:
SELECT ps.storageLocation, p.Pname, SUM(sl.quantity) AS totalQuantity
FROM productStorage ps
JOIN storageLocation sl ON ps.idProdStorage = sl.idLstorage
JOIN product p ON sl.idLproduct = p.idProduct
GROUP BY ps.storageLocation, p.Pname;


