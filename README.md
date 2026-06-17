# table
 BANCO DE DADOS  HT-SIS-01-M-26-10495
CREATE DATABASE SIS04T25;
USE SIS04T25;

CREATE TABLE Customers (
    CustomerID INT AUTO_INCREMENT PRIMARY KEY,
    CustomerName VARCHAR(100) NOT NULL,
    ContactName VARCHAR(100),
    Address VARCHAR(200),
    City VARCHAR(100),
    PostalCode VARCHAR(20),
    Country VARCHAR(100)
);

CREATE TABLE Categories (
    CategoryID INT AUTO_INCREMENT PRIMARY KEY,
    CategoryName VARCHAR(100) NOT NULL,
    Description VARCHAR(255)
);

CREATE TABLE Employees (
    EmployeeID INT AUTO_INCREMENT PRIMARY KEY,
    LastName VARCHAR(100),
    FirstName VARCHAR(100),
    BirthDate DATE,
    Photo VARCHAR(255),
    Notes TEXT
);

CREATE TABLE Suppliers (
    SupplierID INT AUTO_INCREMENT PRIMARY KEY,
    SupplierName VARCHAR(100),
    ContactName VARCHAR(100),
    Address VARCHAR(200),
    City VARCHAR(100),
    PostalCode VARCHAR(20),
    Country VARCHAR(100),
    Phone VARCHAR(20)
);

CREATE TABLE Products (
    ProductID INT AUTO_INCREMENT PRIMARY KEY,
    ProductName VARCHAR(100),
    SupplierID INT,
    CategoryID INT,
    Unit VARCHAR(50),
    Price DECIMAL(10,2)
);

CREATE TABLE Shippers (
    ShipperID INT AUTO_INCREMENT PRIMARY KEY,
    ShipperName VARCHAR(100),
    Phone VARCHAR(20)
);

CREATE TABLE Orders (
    OrderID INT AUTO_INCREMENT PRIMARY KEY,
    CustomerID INT,
    EmployeeID INT,
    OrderDate DATE,
    ShipperID INT
);

CREATE TABLE OrderDetails (
    OrderDetailID INT AUTO_INCREMENT PRIMARY KEY,
    OrderID INT,
    ProductID INT,
    Quantity INT
);

ALTER TABLE Products
ADD CONSTRAINT fk_products_suppliers
FOREIGN KEY (SupplierID)
REFERENCES Suppliers(SupplierID);

ALTER TABLE Products
ADD CONSTRAINT fk_products_categories
FOREIGN KEY (CategoryID)
REFERENCES Categories(CategoryID);

ALTER TABLE Orders
ADD CONSTRAINT fk_orders_customers
FOREIGN KEY (CustomerID)
REFERENCES Customers(CustomerID);

ALTER TABLE Orders
ADD CONSTRAINT fk_orders_employees
FOREIGN KEY (EmployeeID)
REFERENCES Employees(EmployeeID);

ALTER TABLE Orders
ADD CONSTRAINT fk_orders_shippers
FOREIGN KEY (ShipperID)
REFERENCES Shippers(ShipperID);

ALTER TABLE OrderDetails
ADD CONSTRAINT fk_orderdetails_orders
FOREIGN KEY (OrderID)
REFERENCES Orders(OrderID);

ALTER TABLE OrderDetails
ADD CONSTRAINT fk_orderdetails_products
FOREIGN KEY (ProductID)
REFERENCES Products(ProductID);

INSERT INTO Customers
(CustomerName, ContactName, Address, City, PostalCode, Country)
VALUES
('João da Silva', 'Carlos Silva', 'Rua das Flores, 125', 'São Paulo', '01000-000', 'Brasil'),
('Maria Santos', 'Ana Lima', 'Av. Brasil, 450', 'Rio de Janeiro', '20000-000', 'Brasil');

INSERT INTO Categories
(CategoryName, Description)
VALUES
('CDs', 'Discos compactos de áudio'),
('DVDs', 'Filmes e vídeos'),
('Blu-Ray', 'Filmes em alta definição');

INSERT INTO Employees
(LastName, FirstName, BirthDate, Photo, Notes)
VALUES
('Souza', 'Pedro', '1985-03-10', NULL, 'Atendente'),
('Oliveira', 'Mariana', '1990-07-21', NULL, 'Vendas');

INSERT INTO Suppliers
(SupplierName, ContactName, Address, City, PostalCode, Country, Phone)
VALUES
('Music World', 'Lucas Pereira', 'Rua do Comércio, 100', 'São Paulo', '01000-000', 'Brasil', '(11)3333-4444'),
('Global Discos', 'Fernando Costa', 'Av. das Nações, 200', 'Rio de Janeiro', '20000-000', 'Brasil', '(21)2222-3333');

INSERT INTO Products
(ProductName, SupplierID, CategoryID, Unit, Price)
VALUES
('CD Rock Clássico', 1, 1, 'Unidade', 29.90),
('DVD Show Ao Vivo', 2, 2, 'Unidade', 39.90),
('Blu-Ray Ação Total', 2, 3, 'Unidade', 49.90);

INSERT INTO Shippers
(ShipperName, Phone)
VALUES
('Entrega Rápida', '(31)9999-1111'),
('Transportadora Brasil', '(31)8888-2222');

INSERT INTO Orders
(CustomerID, EmployeeID, OrderDate, ShipperID)
VALUES
(1, 1, '2025-05-01', 1),
(2, 2, '2025-05-02', 2);

INSERT INTO OrderDetails
(OrderID, ProductID, Quantity)
VALUES
(1, 1, 2),
(1, 2, 1),
(2, 3, 1);
