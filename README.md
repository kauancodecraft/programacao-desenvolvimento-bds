Aula Prática: Programação e Desenvolvimento de Banco de Dados

Este repositório contém os arquivos desenvolvidos durante a aula prática de Programação e Desenvolvimento de Banco de Dados, focada na criação e manipulação de um banco de dados MySQL para um sistema de gestão de contas a receber.

Conteúdo do Repositório

•
create_database.sql: Script SQL para a criação do banco de dados Loja e suas tabelas (Estado, Municipio, Cliente, ContaReceber).

•
inserir.sql: Script SQL para a inserção de dados de exemplo nas tabelas criadas.

•
consulta.sql: Script SQL que cria uma VIEW (ContasNaoPagas) para listar as contas a receber com situação pendente.

•
relatorio_aula_pratica.pdf: Relatório completo da aula prática, detalhando a introdução, métodos, resultados e conclusão.

Pré-requisitos

Para executar os scripts SQL, você precisará ter o MySQL Community Server instalado e configurado em seu ambiente.

Instalação do MySQL (Ubuntu/Debian)

Caso não tenha o MySQL instalado, você pode instalá-lo utilizando os seguintes comandos:

Bash


sudo apt update
sudo apt install mysql-server
sudo mysql_secure_installation # Siga as instruções para configurar a segurança do MySQL


Como Utilizar

Siga os passos abaixo para recriar o ambiente do banco de dados e executar as consultas:

1. Criar o Banco de Dados e Tabelas

Execute o script create_database.sql para criar o banco de dados Loja e todas as suas tabelas. Certifique-se de estar logado como um usuário MySQL com permissões para criar bancos de dados (ex: root).

Bash


mysql -u root -p < create_database.sql


Após executar, digite a senha do usuário root do MySQL quando solicitado.

2. Inserir Dados de Exemplo

Popule as tabelas com dados de exemplo executando o script inserir.sql:

Bash


mysql -u root -p < inserir.sql


3. Criar e Consultar a VIEW

Crie a VIEW ContasNaoPagas e consulte os dados de contas a receber pendentes com o script consulta.sql:

Bash


mysql -u root -p < consulta.sql
mysql -u root -p -e "USE Loja; SELECT * FROM ContasNaoPagas;"


Estrutura do Banco de Dados (DER)

O banco de dados foi projetado com base no seguinte modelo entidade-relacionamento:

Tabela Estado

Campo
Tipo
Descrição
ID
INT
Chave Primária
Nome
VARCHAR(80)
Nome do Estado
UF
CHAR(2)
Sigla do Estado


Tabela Municipio

Campo
Tipo
Descrição
ID
INT
Chave Primária
Nome
VARCHAR(80)
Nome do Município
Estado_ID
INT
Chave Estrangeira (referencia Estado.ID)


Tabela Cliente

Campo
Tipo
Descrição
ID
INT
Chave Primária
Nome
VARCHAR(80)
Nome do Cliente
CPF
CHAR(11)
CPF do Cliente (Único)
Celular
VARCHAR(10)
Número de Celular
Endereco
VARCHAR(100)
Endereço do Cliente
EndNumero
VARCHAR(10)
Número do Endereço
EndCEP
CHAR(8)
CEP do Endereço
Municipio_ID
INT
Chave Estrangeira (referencia Municipio.ID)


Tabela ContaReceber

Campo
Tipo
Descrição
ID
INT
Chave Primária
Cliente_ID
INT
Chave Estrangeira (referencia Cliente.ID)
DataVencimento
DATE
Data de Vencimento da Conta
Valor
DECIMAL(18,2)
Valor da Conta
Situacao
ENUM('1', '2', '3')
Situação da Conta: '1'=Paga, '2'=Cancelada, '3'=Pendente


