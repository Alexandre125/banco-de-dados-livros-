# banco-de-dados-livros-

# Criar banco de dados:
CREATE DATABASE db_MeusLivros;

# Ver bancos de dados existentes:
SHOW DATABASES;

# Selecionar banco para trabalho
USE db_MeusLivros;

# Como saber qual banco está selecionado
SELECT DATABASE();

# Criar tabela de autores
CREATE TABLE tbl_Autores (
	IdAutor  SMALLINT PRIMARY KEY  AUTO_INCREMENT,
	NomeAutor VARCHAR(20) NOT NULL,
	SobrenomeAutor VARCHAR(60) NOT NULL
); 
DESCRIBE tbl_Autores;

# Criar tabela de editoras
CREATE TABLE tbl_Editoras (
	IdEditora SMALLINT PRIMARY KEY AUTO_INCREMENT,
	NomeEditora VARCHAR(50) NOT NULL
);
DESCRIBE tbl_Editoras;

# Criar tabela de Assuntos
CREATE TABLE  tbl_Assuntos (
	IdAssunto TINYINT PRIMARY KEY AUTO_INCREMENT,
	Assunto VARCHAR(25) NOT NULL
); 

DESCRIBE tbl_Assuntos;

drop table tbl_livros;

# Criar tabela de Livros
CREATE TABLE IF NOT EXISTS tbl_Livros (
	IDLivro SMALLINT PRIMARY KEY NOT NULL AUTO_INCREMENT,
	NomeLivro VARCHAR(70) NOT NULL,
	ISBN13 VARCHAR(13) NOT NULL,
	DataPub DATE,
	PrecoLivro DECIMAL(10,2) NOT NULL,
	NumeroPaginas SMALLINT NOT NULL,
	IdEditora SMALLINT NOT NULL,
	IdAssunto TINYINT NOT NULL,
	CONSTRAINT fk_id_editora FOREIGN KEY (IdEditora) REFERENCES tbl_Editoras (IdEditora) ON DELETE CASCADE,
	CONSTRAINT fk_id_assunto FOREIGN KEY (IdAssunto) REFERENCES tbl_Assuntos (IdAssunto) ON DELETE CASCADE
);

DESCRIBE tbl_Livros;

#  Criar tabela associativa de Livros e Autores
CREATE TABLE tbl_LivrosAutores (
	IdLivro SMALLINT NOT NULL,
	IdAutor SMALLINT NOT NULL,
	CONSTRAINT fk_id_livros FOREIGN KEY (IdLivro) 
	REFERENCES tbl_Livros (IdLivro),
	CONSTRAINT fk_id_autores FOREIGN KEY (IdAutor) 
	REFERENCES tbl_Autores (IdAutor)
);
DESCRIBE tbl_LivrosAutores;

USE db_MeusLivros;

ALTER TABLE tbl_Livros AUTO_INCREMENT=100;
DESCRIBE tbl_Livros;

# Inserir registros na tabela de editoras:
INSERT INTO tbl_editoras (NomeEditora)
VALUES
('Prentice Hall'), ('O Reilly'), 
('Microsoft Press'), ('Wiley'), 
('Mc Graw Hill'), ('Bookman'),
('Novatec'), ('Apress'),
('Sybex'), ('Mike Murach and Associates');
# Verificar se está correto:
SELECT * FROM tbl_editoras;

# Se eu quiser adicionar mais uma editora:
INSERT INTO tbl_editoras (NomeEditora)
VALUES ('MakerMedia');

# Inserir registros na tabela de Assuntos:
INSERT INTO tbl_Assuntos (Assunto)
VALUES
('Ficção'), ('Botânica'),
('Eletrônica'), ('Matemática'),
('Aventura'), ('literatura'),
('Informática'), ('Suspense');

SELECT * FROM tbl_assuntos;

# Inserir regitros na tabela de autores:
INSERT INTO tbl_autores (NomeAutor, SobrenomeAutor)
VALUES
('Daniel', 'Barret'), ('Gerald', 'Carter'), ('Mark', 'Sobell'),
('William', 'Stanek'), ('Richard', 'Blum'), ('Christine', 'Bresnahan'),
('Richard', 'Silverman'), ('Robert', 'Byrnes'), ('Jay', 'Ts'),
('Robert', 'Eckstein'), ('Paul', 'Horowitz'), ('Winfield', 'Hill'),
('Joel', 'Murach'), ('Paul', 'Scherz'), ('Simon', 'Monk');

SELECT * FROM tbl_autores; 

# Inserir registros na tabela de Livros:
INSERT INTO tbl_Livros (NomeLivro, ISBN13, DataPub, PrecoLivro, NumeroPaginas, IdAssunto, IdEditora)
VALUES
('Linux Command Line and Shell Scripting', '9781118983843', '20150109', 165.55, 816, 7, 4),
('SSH, the Secure Shell', '9780596008956', '20050517', 295.41, 672, 7, 2),
('Using Samba', '9780596002565', '20031221', 158.76, 449, 7, 2),
('A Arte da Eletrônica', '9788582604342', '20170308', 176.71, 1160, 7, 6),
('Windows Server 2012 Inside Out', '9780735666313', '20130125', 179.51, 1584, 7, 3),
('Murach´s MySQL', '9781943872367', '20190501', 227.64, 650, 7, 10),
('Practical Electronics for Inventors', '9781259587542', '20160711', 119.58, 1056, 3, 5);

SELECT * FROM tbl_livros;

# Preencher tabela LivrosAutores (associativa)--> relaciona livros com seus autores:
INSERT INTO tbl_LivrosAutores (IdLivro, IdAutor)
VALUES
(100,5), (100,6),
(101,1), (101,7), (101,8),
(102,2), (102,9), (102,10),
(103,11), (103,12),
(104,4),
(105,13),
(106,14), (106,15);
SELECT * FROM tbl_livrosautores;

INSERT INTO tbl_autores (NomeAutor, SobrenomeAutor)
VALUES 
('Rosana','Rios'), ('Claudio','Blanc'), ('Isabela','Freitas');
SELECT*FROM tbl_autores;

INSERT INTO tbl_editoras (NomeEditora)
VALUES 
('Lê'), ('Autêntica'), ('intrinseca');
SELECT*FROM tbl_editoras;

INSERT INTO tbl_assuntos (Assunto)
VALUES 
('Romance'), ('Ficção'), ('Terror');
SELECT*FROM tbl_assuntos;

SELECT * FROM tbl_editoras, tbl_assuntos;

UPDATE tbl_assuntos
SET assunto = 'Psicologia' WHERE IdAssunto = 9;

SELECT * FROM tbl_assuntos;

INSERT INTO tbl_livros (NomeLivro, ISBN13, DataPub, PrecoLivro, NumeroPaginas, IdEditora, IdAssunto)
VALUES
('A Filha do Alquimista', '9788532908407', '20190429', 44.00, 284, 12, 10),
('Avantesma-13 HISTORIAS CLASSICAS DE FANTASMAS', '9788582174098', '20140000', 49.80, 208, 13, 11),
('Não se iluda, Não', '9788580577686', '20150629', 19.90, 272, 14, 9);

#execultamos consutas simples comandos:
USE db_meuslivros;

SELECT NomeAutor FROM tbl_Autores;

SELECT * FROM tbl_Autores;

SELECT NomeLivro FROM tbl_Livros;

SELECT Assunto FROM tbl_Assuntos;

SELECT NomeEditora FROM tbl_Editoras;

#ESPECÍFICANDO COLUNAS

SELECT NomeLivro, PrecoLivro FROM tbl_Livros;

SELECT NomeAutor, SobrenomeAutor FROM tbl_Autores;

SELECT NomeLivro, ISBN13, DataPub FROM tbl_Livros;

SELECT Idlivro, NomeLivro, NumeroPaginas FROM tbl_Livros;

#Consutas com ordenação; comando: ORDEM BY nome da coluna ASC : ASC= ordem crescente, DESC= ordem decrescente.alter
#executando
SELECT NomeLivro, IdEditora FROM tbl_Livros ORDER BY IdEditora;

SELECT NomeLivro, Precolivro FROM tbl_Livros ORDER BY PrecoLivro DESC;

SELECT NomeLivro, DataPub, IdAssunto FROM tbl_Livros ORDER BY idAssunto, NomeLivro;

SELECT NomeLivro, PrecoLivro, DataPub FROM tbl_Livros ORDER BY DataPub DESC;

SELECT NomeAutor, SobrenomeAutor FROM tbl_autores ORDER BY SobrenomeAutor;

USE db_meuslivros;

# Nomes de livros, IDs de assuntos e editora, sem ordem definida.
SELECT NomeLivro, IdAssunto, idEditora 
FROM tbl_Livros;

# Lista de assuntos em ordem alfabética.
SELECT Assunto FROM tbl_assuntos
ORDER BY Assunto ASC;

#  O nome da editora da tabela de editoras cujo ID é igual a 2;
SELECT NomeEditora, IdEditora
FROM tbl_editoras
WHERE IdEditora = 2;

# Nomes de livros, preços e datas de publicação, em ordem cronológica de data de publicação, dos livros da editora de ID igual a 3
SELECT  NomeLivro, PrecoLivro, DataPub, IdEditora
FROM tbl_Livros
WHERE IdEditora = 3
ORDER BY DataPub, IdEditora;

# Nome e sobrenome do autor cujo ID é igual a 4
SELECT  NomeAutor, SobrenomeAutor, IdAutor
FROM tbl_autores
WHERE IdAutor = 4;

# Livro associado ao ID do assunto “Técnico”.
SELECT  IdAssunto
FROM tbl_Assuntos
WHERE Assunto = 'Técnico';

# Nomes de livros, ID de assunto e editora, do assunto “Técnico”. 
SELECT  NomeLivro, IdEditora, IdAssunto
FROM tbl_livros
WHERE IdAssunto  = 23;

# A Data de publicação do livro “Using Samba” 
SELECT  DataPub, NomeLivro
FROM tbl_livros
WHERE NomeLivro = 'Using Samba';

select * from tbl_livros;
UPDATE tbl_livros SET NomeLivro='SSH, O Shell Seguro' WHERE IdLivro=101;

#  O Preço do livro “SSH, o Shell Seguro”
SELECT NomeLivro, PrecoLivro
FROM tbl_livros
WHERE NomeLivro = 'SSH, O Shell Seguro';

SELECT * FROM tbl_assuntos;
UPDATE tbl_assuntos SET assunto= 'Ficção Cientifica' WHERE IdAssunto=1;

# Atividade 4- Apelidos e Lógicas:

INSERT INTO tbl_editoras (NomeEditora)
VALUES
('Record'), ('Companhia de Bolso');
# Verificar se está correto:
SELECT * FROM tbl_editoras;

INSERT INTO tbl_Assuntos (Assunto)
VALUES
('Ciências Sociais'), ('Ciências'),
('História da Arte');
SELECT * FROM tbl_assuntos;

INSERT INTO tbl_autores (NomeAutor, SobrenomeAutor)
VALUES
('Umberto', 'Eco'), ('Carl', 'Sagan');
SELECT * FROM tbl_autores;

INSERT INTO tbl_Livros (NomeLivro, ISBN13, DataPub, PrecoLivro, NumeroPaginas, IdAssunto, IdEditora)
VALUES
('O Fascismo Eterno', '9788501116154', '20181010', 19.66, 140, 12, 15),
('Bilhões e Bilhões', '9788535911947', '20080325', 22.74, 300, 13, 16),
('História da Beleza', '9788501090881', '20100930', 139.99, 420, 14, 15); 
SELECT * FROM tbl_livros;
SELECT * FROM tbl_assuntos;  
SELECT * FROM tbl_editoras;

INSERT INTO tbl_LivrosAutores (IdLivro, IdAutor)
VALUES
(119,18),
(120,19),
(121,20);
SELECT * FROM tbl_livros;
SELECT (IdLivro) FROM tbl_livros;
SELECT (IdAutor) FROM tbl_autores;

SELECT NomeLivro AS Livro, IdAssunto, PrecoLivro 'Preço' FROM tbl_Livros WHERE PrecoLivro > 55.00;

SELECT NomeLivro, IdAssunto FROM tbl_Livros WHERE IdAssunto = 5 and 11 and 8 ORDER BY NomeLivro ASC;

use db_meuslivros;

SELECT * from tbl_assuntos;

SELECT NomeLivro Livro, PrecoLivro 'Preço' FROM tbl_Livros WHERE IdEditora > 2 ORDER BY 'Preço' ASC LIMIT 4; 

SELECT NomeLivro Livro, ISBN13, PrecoLivro 'Preço', DataPub 'Data'
 FROM tbl_Livros 
 WHERE DataPub < '20100101' AND DataPub> '20050101' ORDER BY DataPub ASC; 
 

 SELECT PrecoLivro'Preço', IdEditora  FROM tbl_livros WHERE IdEditora=3;
 
 SELECT sum(PrecoLivro)/count(IdEditora) 'Preço médio' FROM tbl_livros  WHERE IdEditora = 2 AND 3 ;
 
SELECT NomeLivro, MAX(PrecoLivro) 'Preço' FROM tbl_livros;

# Diminua o preço dos livros publicados entre 01/01/2001 e 15/11/2009 em 15% e depois mostre os livros 
#e seus novos preços.
DELIMITER //
CREATE PROCEDURE diminuirPreco ( x SMALLINT)
begin
	UPDATE tbl_livros
    SET PrecoLivro = PrecoLivro * (1 - x /100);
    SELECT 'Procedimento executado com sucesso! ' FROM tbl_livros WHERE DataPub > '20010101' AND DataPub < '20091115';
END//
DELIMITER ;
SELECT NomeLivro, PrecoLivro FROM tbl_livros;

CALL diminuirPreco (15);

SELECT NomeLivro AS Livro, PrecoLivro 'Preço' FROM tbl_livros WHERE DataPub > '20010101' AND DataPub < '20091115';

#Retorne os nomes dos livros, sobrenomes dos autores e assuntos dos livros que custam mais de R$ 190,00
SELECT NomeLivro AS Livro, Assunto FROM tbl_livros 
INNER JOIN tbl_assuntos ON tbl_livros.IdAssunto = tbl_assuntos.IdAssunto
WHERE PrecoLivro >= 190.00;

#○ Mostre o número total de páginas dos livros que foram publicados a partir de 01 de janeiro de 2012.
SELECT NumeroPaginas, DataPub FROM tbl_livros WHERE DataPub >= '20120101';

#Retorne os nomes dos livros, sobrenomes dos autores e assuntos dos livros que custam mais de R$ 190,00
use db_MeusLivros;
SELECT tbl_Livros.NomeLivro, tbl_Autores.SobrenomeAutor, tbl_LivrosAutores.IdLivro, PrecoLivro
FROM tbl_LivrosAutores
INNER JOIN tbl_Livros 
	ON tbl_Livros.IdLivro = tbl_LivrosAutores.IdLivro
INNER JOIN tbl_Autores
	ON tbl_Autores.IdAutor = tbl_LivrosAutores.IdAutor
WHERE PrecoLivro >= 190.00;

#  Obtenha os ISBNs dos livros publicados por autores cujo sobrenome começa com a letra S, em ordem cronológica.
SELECT tbl_Autores.SobrenomeAutor, tbl_LivrosAutores.IdLivro, tbl_Livros.ISBN13
FROM tbl_LivrosAutores
INNER JOIN tbl_Livros 
	ON tbl_Livros.IdLivro = tbl_LivrosAutores.IdLivro
INNER JOIN tbl_Autores 
	ON tbl_Autores.IdAutor = tbl_LivrosAutores.IdAutor
WHERE SobrenomeAutor LIKE 's%'
ORDER BY SobrenomeAutor;

#Sintaxe
#CREATE PROCEDURE nome_procedimento (parâmetros)
#declarções a executar
CREATE PROCEDURE verPreco (varLivro SMALLINT)
SELECT CONCAT('o preço do livro ', NomeLivro, ' é ', PrecoLivro) as Preço
FROM tbl_livros WHERE IdLivro = varLivro;

CALL verPreço (101);

CREATE PROCEDURE consultaLivros (varEditora VARCHAR(50))
SELECT CONCAT ('O livro ' , NomeLivro, ' custa ', PrecoLivro) AS Preço
FROM tbl_Livros
INNER JOIN tbl_editoras
	ON tbl_livros.Ideditora = tbl_editoras.IdEditora
WHERE tbl_editoras.NomeEditora = varEditora;
    
    SELECT NomeEditora FROM tbl_editoras;
CALL consultaLivros ('Lê');

#Exemplo: aumentar od preços dos livros em x%
DELIMITER //
CREATE PROCEDURE aumentaPreco ( x SMALLINT)
begin
	UPDATE tbl_livros
    SET PrecoLivro = PrecoLivro * (1 + x/100);
    SELECT 'Procedimento executado com sucesso! ';
END//
DELIMITER ;
SELECT * FROM tbl_livros where Idlivro;
SELECT PrecoLivro FROM tbl_livros WHERE Idlivro = 100 ;

CALL aumentaPreco (15);

SELECT PrecoLivro FROM tbl_livros WHERE Idlivro = 100;

USE db_meuslivros;

DELIMITER //
CREATE PROCEDURE diminuirPreco (x SMALLINT)
BEGIN
	UPDATE tbl_livros
    SET PrecoLivro = PrecoLivro * (1 + x/100);
    select 'Procedimento execultado com sucesso! ';
END//

DELIMITER ;

SELECT PrecoLivro FROM tbl_livros;

CALL diminuirPreco (17);

SELECT PrecoLivro FROM tbl_livros;

#2. Acrescentar um valor informado aos preços dos livros, em Reais (R$), não em porcentagem
DELIMITER //
CREATE PROCEDURE acrescentarPreco (x SMALLINT)
BEGIN
	UPDATE tbl_livros
    SET PrecoLivro = PrecoLivro + x ;
    SELECT 'Procedimento execultado ';
END//
    
DELIMITER;
    
SELECT PrecoLivro FROM tbl_livros;
    
CALL acrescentarPreco (10)
    
SELECT PrecoLivro FROM tbl_livros;
    
#3. Efetuar uma consulta que retorne os nomes dos livros, assunto, editora e nome e sobrenome do autor 
#(esses dois concatenados), de um livro consultado pelo seu ID.
SELECT tbl_Livros.NomeLivro, tbl_assuntos.Assunto, tbl_editoras,CONCAT (tbl_Autores.NomeAutor, SobrenomeAutor), tbl_LivrosAutores.IdLivro
FROM tbl_Livros
INNER JOIN tbl_Livros
	ON tbl_livros.IdAssunto = tbl_assuntos.IdAssunto
INNER JOIN tbl_editoras
	ON tbl_editoras.IdEditora = tbl_livros.IdEditora
INNER JOIN tbl_autores
	ON tbl_autores.IdAutor = tbl_LivrosAutores.IdAutor
WHERE IdLivros;

#4. Cadastrar um assunto novo, informado como parâmetro.
SELECT tbl_Autores.SobrenomeAutor, tbl_LivrosAutores.IdLivro, tbl_Livros.ISBN13
FROM tbl_LivrosAutores
INNER JOIN tbl_Livros 
	ON tbl_Livros.IdLivro = tbl_LivrosAutores.IdLivro
INNER JOIN tbl_Autores 
	ON tbl_Autores.IdAutor = tbl_LivrosAutores.IdAutor
WHERE SobrenomeAutor LIKE 's%'
ORDER BY SobrenomeAutor;
    
 #criando TRIGGERS   
CREATE TRIGGER tr_insere_assunto AFTER INSERT ON tbl_assuntos
FOR EACH ROW  SET @msg = 'Assunto inserido com sucesso!';

#Inserir registro para testar o TRIGGER
INSERT INTO tbl_assuntos (Assunto)
VALUES ('Calculo');

#Verificar resultado
SELECT @msg;

DELIMITER //
CREATE TRIGGER tr_insere_livro BEFORE INSERT
ON tbl_livros
FOR EACH ROW
begin
	IF NEW.DataPub IS NULL THEN
		SET NEW.DataPub = CURDATE();
	END IF;
END//
DELIMITER ;

SHOW TRIGGERS;

INSERT INTO tbl_livros (NomeLivro, ISBN13, DataPub, PrecoLivro, NumeroPaginas, IdAssunto, IdEditora)
VALUES ('Livro Teste', '9780952012899', NULL, 180.21, 999, 5, 4);

INSERT INTO tbl_livros (NomeLivro, ISBN13, PrecoLivro, NumeroPaginas, IdAssunto, IdEditora)
VALUES ('Livro Teste 2', '9780952012899', 180.21, 999, 5, 4);

SELECT * FROM tbl_livros;

CREATE TABLE Produto (
IdProduto INT NOT NULL AUTO_INCREMENT,
Nome_Produto VARCHAR (45) NULL,
Preco_Normal DECIMAL(10,2) null,
Preco_Desconto DECIMAL(10,2) null,
primary key (IdProduto) );

DELIMITER $$
create TRIGGER tr_desconto BEFORE INSERT ON Produto
FOR each row
BEGIN
IF NEW.Preco_Normal > 50.00 THEN
	SET NEW.Preco_Desconto = (NEW.Preco_Normal * 0.90);
else
	SET NEW.Preco_Desconto = NEW.Preco_Normal;
END IF;
SET @resultado = 'Produto cadastrado.' ;
END$$
DELIMITER ;

INSERT INTO Produto (Nome_Produto, Preco_Normal)
VALUES ('DVD', 1.00), ('Bateria', 74.00), ('Carregador', 52.00), ('Pendrive', 18.00);

select @resultado AS Resultado, Nome_Produto Produto, Preco_normal, Preco_Desconto FROM Produto;

