Hotel Management System
Descrição
Este projeto consiste na criação de um sistema de gerenciamento de hotel utilizando o banco de dados MySQL. O sistema permite o gerenciamento de hóspedes, quartos e reservas, permitindo a inserção, atualização e remoção de registros, além da consulta de informações sobre hóspedes e reservas.

Funcionalidades:
Cadastro de hóspedes: Armazena dados como nome, documento e telefone.
Cadastro de quartos: Inclui informações como nome, tipo (simples, duplo ou luxo) e preço.
Gerenciamento de reservas: Registra reservas feitas por hóspedes para quartos específicos, incluindo datas de check-in e check-out.
Atualização de dados: Permite alterar informações de hóspedes e preços dos quartos.
Exclusão de reservas e hóspedes: Remove reservas específicas ou hóspedes, garantindo a exclusão em cascata de todas as reservas associadas ao hóspede.
Tabelas
O projeto contém as seguintes tabelas:

HÓSPEDE: Armazena os dados dos hóspedes.
QUARTOS: Contém informações sobre os quartos do hotel.
RESERVAS: Armazena as reservas feitas pelos hóspedes para os quartos.
Dependências
Para utilizar o projeto, você precisará:

MySQL 8.x ou superior
Estrutura do banco de dados:
Tabela hospede:

id_hospede: identificador único do hóspede.
nome: nome do hóspede.
documento: documento de identificação.
telefone: telefone de contato.
Tabela quartos:

id_quarto: identificador único do quarto.
nome: nome do quarto.
tipo: tipo do quarto (simples, duplo, luxo).
preco: preço do quarto.
Tabela reservas:

id_reserva: identificador único da reserva.
id_hospede: identificador do hóspede que fez a reserva.
id_quarto: identificador do quarto reservado.
data_checkin: data de entrada.
data_checkout: data de saída.
Como usar
1. Criação do banco de dados e tabelas
Execute o seguinte comando no MySQL para criar o banco de dados:
CREATE DATABASE HotelManagementSystem;
USE HotelManagementSystem;
Em seguida, crie as tabelas executando as queries fornecidas no arquivo script.sql.

2. Inserção de dados
Você pode inserir dados nas tabelas executando os comandos INSERT INTO fornecidos no arquivo script.sql.

3. Consultas
Para consultar os hóspedes e suas reservas, execute a query:
SELECT 
    h.nome AS Nome_Hospede,
    r.id_reserva AS ID_Reserva,
    r.data_checkin AS Data_Checkin,
    r.data_checkout AS Data_Checkout,
    q.nome AS Nome_Quarto,
    q.tipo AS Tipo_Quarto,
    q.preco AS Preco_Quarto
FROM
    reservas r
JOIN
    hospede h ON r.id_hospede = h.id_hospede
JOIN
    quartos q ON r.id_quarto = q.id_quarto;
4. Atualização de dados
Para atualizar as informações de um hóspede, como telefone ou documento, utilize:
UPDATE hospede
SET telefone = 'novo_telefone', documento = 'novo_documento'
WHERE id_hospede = <id_hospede>;

Para atualizar o preço de um quarto, utilize:
UPDATE quartos
SET preco = novo_preco
WHERE id_quarto = <id_quarto>;

5. Exclusão de dados
Para excluir uma reserva específica, utilize:
DELETE FROM reservas
WHERE id_reserva = <id_reserva>;

Para excluir um hóspede e todas as reservas associadas, utilize:
DELETE FROM hospede
WHERE id_hospede = <id_hospede>;

6. Configurar Chaves Estrangeiras com Cascata
Execute o comando abaixo para garantir que todas as reservas associadas a um hóspede sejam excluídas automaticamente quando o hóspede for removido:
ALTER TABLE reservas
ADD CONSTRAINT fk_hospede_reserva
FOREIGN KEY (id_hospede) REFERENCES hospede(id_hospede)
ON DELETE CASCADE;

