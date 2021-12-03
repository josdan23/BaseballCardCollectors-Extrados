REQUISITOS:
- Usuario: para cada usuario se debe guardar el id, nombre de usuario, contraseña, email, y rol.
- Roles: los roles serán coleccionista y administrador de sistema.
- Cartas: cada carta debe tener un id de carta, nombre del jugador en la carta, apellido del jugador, equipo, rol del jugador en el equipo, foto del jugador y rareza de la carta (bronze,plata,oro,platino).
- Series:Una serie representa un lote de cartas encargado a la fábrica y muestra como estaban las cosas en el momento del diseño de esas cartas. cada carta debe pertenecer a una y solo una serie(por ejemplo serie 1, serie 2, serie 3, etc). Se deberá guardar la fecha en la que salió cada serie y que tarjetas pertenecen a cada serie. Tener en cuenta que un jugador puede aparecer en 2 o más series con información distinta (ej: jugador X pertenece al equipo A en la serie 1 y al equipo B en la serie 2)
- Colecciones: cada serie tendrá colecciones de cartas. Una colección de cartas es un grupo dado de cartas de una serie (ejemplo: "jugadores de X equipo de serie 1" o "MVP de serie 1"). No todas las cartas necesariamente tienen que pertenecer a una colección. Una carta puede pertenecer a 2 o más colecciones.
  

VENTAJAS DEL MODELO
- Si en un futuro la carta desea agregar más info sobre el jugador/equipo, puede hacerlo agregando atributos o relaciones a la tabla player_career. Por ejemplo: statistics, averages, suspensions, salaries, etc.
- Se permite la separación con sus respectivos controles, en tres instancias de db diferentes donde cada una contengan una capa logica:  user_information, card_information, player_information.


CONSIDERACIONES A TENER EN CUENTA
 - Es posible que existan admins que desempeñen el rol de colecionistas.
 - Pueden existir cartas de una serie que pertenezcan a una colección de otra serie. Al realizar un input se debe verificar que la serie de la carta deba coincidir con la serie de la colección, caso contrario no puede pertener a la coleccion.
 - Las queries pueden llegar a ser largas.


QUERIES DE EJEMPLO

- CARTAS QUE POSEE UN USUARIO ID 11

select * from users, users_cards, cards, player_career, players
where users.idUser = users_cards.fk_idUser
and users.idUser = 11
and users_cards.fk_idCard = cards.idCard
and cards.fk_playerCareer = player_career.idPlayerCareer
and player_career.fk_idPlayer = players.idPlayer



- INFO DE CARTA ID 3

select * from cards, player_career, players, teams
where cards.idCard = 3
and cards.fk_playerCareer = player_career.idPlayerCareer
and player_career.fk_idPlayer = players.idPlayer
and player_career.fk_idTeam = teams.idTeam

- CARTAS DE LA SERIE 1

select * from series, cards
where series.idSerie = 2
and series.idSerie = cards.fk_idSerie


- CARTAS DE JUGADOR 4

select * from players, player_career, cards
where players.idPlayer = 4
and players.idPlayer = player_career.fk_idPlayer
and cards.fk_playerCareer = player_career.idPlayerCareer

- Cantidad de cartas de rareza 4
select count(rarities.idRarity) from RARITIES, cards
where rarities.idRarity = 4
and rarities.idRarity = cards.fk_idRarity

- CARTAS DEL EQUIPO 20
select * from teams, player_career, cards
where teams.idTeam = 21
and teams.idteam = player_career.fk_idTeam
and cards.fk_playerCareer = player_career.idPlayerCareer


