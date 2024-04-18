# turzin

# Problema 2996

Você trabalha em uma transportadora e precisa mostrar com urgência o ano e o nome de todos os clientes que enviaram e
receberam pacotes azuis ou do ano de 2015 e também que o endereço do seu remetente ou destinatário não seja de Taiwan.
Além disso, você deve ordenar o resultado pelo ano de maneira decrescente.


CREATE TABLE IF NOT EXISTS sender as
SELECT *

FROM packages

LEFT JOIN users ON packages.id_user_sender=users.id

SELECT * FROM sender

DROP TABLE sender

CREATE TABLE IF NOT EXISTS receiver as
SELECT year,
sender.name as sender,
users.name as receiver,
color,
sender.address as sender_address,
users.address as receiver_address,
users.name
FROM sender
LEFT JOIN users ON sender.id_user_receiver = users.id
WHERE (sender.address != 'Taiwan' AND users.address != 'Taiwan') AND (sender.color='blue' OR sender.year=2015)

DROP TABLE receiver

SELECT year,sender,receiver FROM receiver
