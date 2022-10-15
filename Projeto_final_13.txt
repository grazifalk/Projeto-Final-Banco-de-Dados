--Trabalho realizado por:
--Amanda Casadem, Aniello Longobardi, Eduardo de Andrade, Graziela Falk e Roberto de Andrade

--Criação do banco de dados

create database projeto_final;

--Criação das tabelas

--criação da tabela "Funcionário"
create table funcionario (
	id_funcionario bigserial not null, 
	nome_funcionario varchar(100)not null,
	cpf_funcionario varchar(15) unique not null, 
	salario numeric not null,
	primary key(id_funcionario)
);

--Criação da tabela "Categoria"
create table categoria(
	id_categoria serial not null, 
	nome_categoria varchar(100) not null,
	primary key(id_categoria)
);

--Criação da tabela "Produto"
create table produto(
	id_produto serial not null,
	id_funcionario integer not null, 
	id_categoria integer not null,
	nome_produto varchar(100) not null,
	qtd_estoque integer not null,
	data_fabricacao date not null,
	valor_produto numeric not null,
	data_cadastro date not null,
	primary key(id_produto),
	constraint fk_id_funcionario
	foreign key(id_funcionario) references funcionario(id_funcionario)
		match full
		on update cascade
		on delete cascade,
	constraint fk_id_categoria
	foreign key(id_categoria) references categoria(id_categoria)
		match full
		on update cascade
		on delete cascade
);

--Criação da tabela "Endereço"
create table endereco (
	id_endereco serial not null,
	rua varchar(100) not null,
	cep varchar(9) not null,
	bairro varchar(50) not null,
	numero varchar(5) not null,
	cidade varchar(50) not null,
	estado char(2) not null,
	primary key(id_endereco)
);

--Criação da tabela cliente
create table cliente (
	id_cliente serial not null,
	id_endereco integer not null,
	nome_cliente varchar(100) not null,
	login varchar(100) not null,
	senha varchar(100) not null,
	email varchar(100) not null,
	cpf_cliente varchar(15) unique not null,
	data_nascimento date not null,
	telefone varchar(20) not null,
	primary key(id_cliente),
	constraint fk_id_endereco
	foreign key(id_endereco) references endereco (id_endereco)
		match full
		on update cascade
		on delete cascade
);

--Criação da tabela pedido
create table pedido (
	id_pedido serial not null,
	id_cliente integer not null,
	id_produto integer not null,
	qtd_produto integer not null,
	data_pedido timestamp not null,
	primary key(id_pedido),
	constraint fk_id_cliente
	foreign key(id_cliente) references cliente(id_cliente)
		match full
		on update cascade
		on delete cascade,
	constraint fk_id_produto
	foreign key(id_produto) references produto(id_produto)
		match full
		on update cascade
		on delete cascade
);

--insert nas tabelas

--Inserção de dados nas colunas da tabela "Funcionário"
insert into funcionario (nome_funcionario, cpf_funcionario, salario)
values
	('Laura Patrícia Cavalcanti', '898.369.309-65', 1200.0),
	('Milena Cristiane Lopes', '674.825.222-98', 1600.0),
	('Giovanni Murilo Sales', '289.823.452-48', 1800.0),
	('Luís Joaquim Fernandes', '405.210.907-41', 1950.0),
	('Julio Luiz Santos', '024.308.478-17', 2200.0);

--Inserção de dados nas colunas da tabela "Categoria"
insert into categoria (nome_categoria)
values
	('Bebidas'),
	('Sobremesa'),
	('Massas'),
	('Sanduíches'),
	('Porções');

--Inserção de dados nas colunas da tabela "Endereço"
insert into endereco(rua, cep, bairro, numero, cidade, estado)
values
	('Estrada do Aviário', '25720-180', 'Aviário', '516', 'Petrópolis', 'RJ'),
	('Avenida Carlos Gomes', '25720-120', 'Princesa Isabel', '242', 'Petrópolis', 'RJ'),
	('Rua Rio Negro', '25720-000', 'Alvorada', '822', 'Petrópolis', 'RJ'),
	('Rua Carvalho Júnior', '25720-100', 'Corrêas', '194', 'Petrópolis', 'RJ'),
	('Servidão Geraldo de Alcântara', '25720-200', 'Saldanha Marinho', '516', 'Petrópolis', 'RJ'),
	('Rua Junior', '25720-147', 'pantanal', '195', 'Petrópolis', 'RJ'),
	('av.Alcântara', '25780-200', 'tartaruga', '598', 'Petrópolis', 'RJ');

--Inserção de dados nas colunas da tabela cliente
insert into cliente(nome_cliente, login, senha, email, cpf_cliente, data_nascimento, telefone, id_endereco)
values
	('Sabrina Caroline Gomes', 'carolgomes', '6514863686', 'sabrina_gomes@citadini.imb.br', '862.655.887-29', '1988-08-22', '(24) 3924-3598', 1),
	('Cauã Alexandre Duarte', 'cauaduarte', '12345678', 'caua.duarte@engenharia.ufjf.br', '566.231.447-06', '1945-03-09', '(24) 3775-3903', 2),
	('Clara Lívia Caldeira', 'claracaldeira', '13284389781', 'catarina_caldeira@tkk.com.br', '678.367.597-02', '1955-07-10', '(24) 3932-4421', 3),
	('Kaique Elias da Mata', 'kaiquemata', '54565882399', 'kaiqueeliasdamata@tjam.jus.br', '266.231.447-06', '1995-02-19', '(24) 3975-4829', 4),
	('Alessandra da Conceição', 'aleconceicao', '64975734918524', 'esther_daconceicao@gsw.com.br', '512.132.766-44', '1956-01-22', '(24) 3530-9334', 5),
	('Paulo duarte da silva','pauloduarte','123','pauloduarte@gmail.com','210.546.788-69','1974-08-02','(24)3654-6987',6 ),
	('Maria Eduarda da Mata', 'mariaeduarda', '54689754259', 'mariaeduardaamatatjam.jus.br', '452.689.447-06', '1996-08-19', '(24) 8954-4829', 7);

--Inserção de dados nas colunas da tabela "Produto"
insert into produto(id_funcionario, id_categoria, nome_produto, qtd_estoque, data_fabricacao, valor_produto, data_cadastro)
values
	(1, 1, 'Pepsi', 55, '2022-07-20', '10.0', '2022-01-10'),
	(2, 2, 'Pudim', 40, '2022-08-25', '6.0', '2022-03-03'),
	(3, 3, 'Pizza', 50, '2022-08-26', '70.0', '2022-01-09'),
	(4, 4, 'X-tudão', 35, '2022-08-25', '15.0', '2022-03-17'),
	(5, 5, 'Batata frita', 15, '2022-08-20', '25.0', '2022-04-2');

--Inserção de dados nas colunas da tabela pedido
insert into pedido(id_cliente, id_produto, qtd_produto, data_pedido)
values
	(1, 5, 2, '2022-08-27 17:08'),
	(1, 1, 1, '2022-08-27 17:08'),
	(2, 3, 1, '2022-08-25 19:31'),
	(2, 1, 1, '2022-08-25 19:31'),
	(2, 5, 1, '2022-08-25 19:31'),
	(3, 2, 2, '2022-08-26 18:39'),
	(4, 4, 4, '2022-08-25 17:52'),
	(4, 2, 2, '2022-08-25 17:52'),
	(4, 2, 4, '2022-08-25 17:52'),
	(5, 3, 1, current_timestamp),
	(5, 1, 1, current_timestamp);
	
--4)a. SQL de consulta: produtos cadastrados, nome categoria e nome funcionário que cadastrou

--Sem inner join 
select produto.nome_produto as "Produto", categoria.nome_categoria as "Categoria", funcionario.nome_funcionario as "Funcionario"
from produto , categoria , funcionario
where produto.id_categoria = categoria.id_categoria and
produto.id_funcionario = funcionario.id_funcionario;

--Com inner join
select produto.nome_produto as "Produto", categoria.nome_categoria as "Categoria", funcionario.nome_funcionario as "Funcionario"
from produto 
inner join categoria
on produto.id_categoria = categoria.id_categoria
inner join funcionario
on produto.id_funcionario = funcionario.id_funcionario;


--4)b. Uma consulta mostrando todos os pedidos feitos (sem os itens do pedido), com o nome e telefone do cliente;

--Sem inner join 
select pedido.id_pedido as "Pedidos", cliente.nome_cliente as "Nome do cliente", cliente.telefone as "Telefone do cliente"
from pedido, cliente
where pedido.id_cliente  = cliente.id_cliente;

--Com inner join
select pedido.id_pedido as "Pedidos", cliente.nome_cliente as "Nome do cliente" , cliente.telefone as "Telefone do cliente"
from pedido
inner join cliente
on pedido.id_cliente  = cliente.id_cliente;


--4)c. Uma consulta mostrando todos os pedidos feitos, com seus itens, mostrando: número do pedido,
--     nome do cliente, data do pedido, nome do produto comprado e a quantidade comprada de cada produto;

--Sem inner join 
select pedido.id_pedido, cliente.nome_cliente as "Nome do cliente", pedido.data_pedido as "Data do pedido", produto.nome_produto as "Produto", pedido.qtd_produto as "Quantidade"
from pedido, cliente , produto
where pedido.id_cliente = cliente.id_cliente and  pedido.id_produto = produto.id_produto;

--Com inner join
select pedido.id_pedido , cliente.nome_cliente as "Nome do cliente", pedido.data_pedido as "Data do pedido", produto.nome_produto as "Produto", pedido.qtd_produto as "Quantidade"
from pedido
inner join cliente
on pedido.id_cliente = cliente.id_cliente  
inner join produto
on pedido.id_produto = produto.id_produto;


--4)d. Uma consulta mostrando a quantidade de pedidos por cliente, com resultado ordenado por nome do cliente, de modo crescente

--Sem inner join
select cliente.nome_cliente as "Nome do cliente", count(pedido.id_cliente) as "Quantidade de pedidos"
from pedido, cliente 
where pedido.id_cliente = cliente.id_cliente 
group by cliente.nome_cliente 
order by cliente.nome_cliente asc

--Com inner join
select cliente.nome_cliente  as "Nome do cliente", count(pedido.id_cliente) as "Quantidade de pedidos"
from  pedido
inner join cliente on pedido.id_cliente = cliente.id_cliente
group by cliente.nome_cliente 
order by cliente.nome_cliente asc


--5)a. Aumentar em 500 o salário de todos os funcionários

select * from funcionario

update funcionario set salario = salario + 500


--5)b. Alterar o email e telefone de um cliente cadastrado

select * from public.cliente

update cliente 
set email = 'sabrina_gomes@gmail.com', 
telefone = '(24) 2581-9673'
where id_cliente = 1;


--6) Excluir os clientes que não tem @ no email ou que a senha seja menor que 8 caracteres

select * from cliente

delete from cliente 
where char_length(senha)<8 or email not like '%@%';

