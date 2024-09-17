[![Review Assignment Due Date](https://classroom.github.com/assets/deadline-readme-button-22041afd0340ce965d47ae6ef1cefeee28c7c493a6346c4f15d667ab976d596c.svg)](https://classroom.github.com/a/r-tQZu0l)
# BBT3104-Lab1of6-DatabaseTransactions


| **Key**                                                               | Value                                                                                                                                                                              |
|---------------|---------------------------------------------------------|
| **Group Name**                                                               | ? |
| **Semester Duration**                                                 | 19<sup>th</sup> August - 25<sup>th</sup> November 2024                                                                                                                       |

## Flowchart

## Pseudocode
START TRANSACTION
SET @orderNumber = MAX(orderNumber) + 1 FROM orders

INSERT INTO orders (@orderNumber, currentDate, requiredDate, shippedDate, status, customerNumber)
SAVEPOINT before_product_1

INSERT INTO orderdetails (orderNumber, productCode, quantityOrdered, priceEach, orderLineNumber)
UPDATE products SET quantityInStock = quantityInStock - orderedQuantity

SAVEPOINT before_product_2
INSERT product_2
IF error THEN
   ROLLBACK TO SAVEPOINT before_product_2
ENDIF

INSERT remaining products
RECEIVE payment from customer

COMMIT TRANSACTION
## Support for the Sales Departments' Report
1) Add a payments table to store individual payment installments with amounts and dates for each order.
2) Modify the orders table to include fields like totalAmount and totalPaid.
3) Update payment processing logic to adjust the totalPaid after each payment and calculate the remaining balance.
4) Generate a report that shows orders where the totalPaid is less than the totalAmount to identify outstanding balances to be followed up.

Example schema;
CREATE TABLE payment_details (
    paymentId INT AUTO_INCREMENT PRIMARY KEY,
    orderNumber INT,
    paymentAmount DECIMAL(10,2),
    paymentDate DATE,
    balance DECIMAL(10, 2),
    FOREIGN KEY (orderNumber) REFERENCES orders(orderNumber)
);
