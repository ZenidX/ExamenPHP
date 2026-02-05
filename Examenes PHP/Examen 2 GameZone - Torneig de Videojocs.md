---
layout: default
title: "Examen 2: GameZone - Torneig de Videojocs"
---

# EXAMEN 2: GameZone — Torneig de Videojocs

## EXAMEN UF1 — Avaluació RA3 (5 punts)

**Durada: 1 hora**

1. Desenvolupa la següent aplicació: (5p)

Crea el directori **nomCognomExamenM9** amb els fitxers `index.html` i `query.php` (com a mínim, pots crear més fitxers si ho necessites).

**No s'ha de tindre en compte el control d'errors, suposarem que l'usuari escriu tot correctament.**

**Es poden consultar els apunts i pràctiques realitzades. La detecció d'ús de qualsevol altre pàgina o ús d'alguna IA (durant o després de l'examen), comporta un 0 a tota la prova d'avaluació.**

**S'ha d'utilitzar la llibreria i funcions explicades a classe.**

Importa el fitxer `gamezone.sql` a la teva base de dades i segueix les instruccions:

## 📄 enunciat_gamezone.txt

```
EXAMEN RA3 — GameZone (Torneig de Videojocs)

1. Importa el fitxer gamezone.sql a la teva base de dades.

2. index.html
   - Crea un formulari amb un camp de text on l'usuari pugui escriure
     el NOM D'UN EQUIP (ex: "Phoenix Esports", "Barcelona Wolves"...).
   - El formulari enviarà les dades a query.php mitjançant POST.

3. query.php
   - Connecta't a la base de dades.
   - Realitza una consulta que mostri totes les partides on ha participat
     l'equip introduït (tant com equip local com visitant), juntament amb
     el nom de l'equip rival i el resultat.
   - Mostra els resultats en una TAULA HTML amb les columnes:
     Data | Joc | Equip Rival | Punts Propis | Punts Rival | Resultat
   - La columna "Resultat" ha de mostrar:
     · "Victòria" si l'equip consultat ha guanyat
     · "Derrota" si ha perdut
     · "Empat" si han empatat
   - A sota de la taula, mostra:
     · El nombre total de partides jugades.
     · El nombre de victòries, derrotes i empats.
   - Si no es troben resultats, mostra el missatge:
     "No s'han trobat partides per a l'equip indicat."
```

### CRITERIS

- Connexió a la BBDD (1,25p)
- Consulta (1,5p)
- Tractament de dades (2,25p)

### ENTREGA

S'ha de penjar tot al Moodle abans de finalitzar l'hora d'examen.
Es pot entregar mitjançan:

- un archiu comprimit .zip
- url a un repositori de github public o on zenidx sigui colaborador. Per a aquest examen si que es tindrà en compte l'última versió/commit que hi hagi al repositori amb data dintre de l'hora d'examen.

## 💾 gamezone.sql

```sql
-- =============================================
-- GameZone — Torneig de Videojocs
-- =============================================

DROP DATABASE IF EXISTS gamezone;
CREATE DATABASE gamezone CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
USE gamezone;

CREATE TABLE equips (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nom VARCHAR(100) NOT NULL,
    ciutat VARCHAR(50) NOT NULL,
    any_fundacio INT NOT NULL
);

CREATE TABLE jugadors (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nickname VARCHAR(50) NOT NULL,
    nom_real VARCHAR(100) NOT NULL,
    edat INT NOT NULL,
    id_equip INT NOT NULL,
    FOREIGN KEY (id_equip) REFERENCES equips(id)
);

CREATE TABLE partides (
    id INT AUTO_INCREMENT PRIMARY KEY,
    id_equip_local INT NOT NULL,
    id_equip_visitant INT NOT NULL,
    punts_local INT NOT NULL,
    punts_visitant INT NOT NULL,
    data DATE NOT NULL,
    joc VARCHAR(50) NOT NULL,
    FOREIGN KEY (id_equip_local) REFERENCES equips(id),
    FOREIGN KEY (id_equip_visitant) REFERENCES equips(id)
);

-- Equips
INSERT INTO equips (nom, ciutat, any_fundacio) VALUES
('Phoenix Esports', 'Barcelona', 2019),
('Barcelona Wolves', 'Barcelona', 2020),
('Madrid Thunder', 'Madrid', 2018),
('Valencia Storm', 'València', 2021),
('Sevilla Raptors', 'Sevilla', 2020),
('Bilbao Titans', 'Bilbao', 2019);

-- Jugadors
INSERT INTO jugadors (nickname, nom_real, edat, id_equip) VALUES
('Blaze', 'Marc Torres', 22, 1),
('Frost', 'Anna López', 19, 1),
('Shadow', 'Pau Garcia', 21, 1),
('Viper', 'Laura Martín', 23, 2),
('Storm', 'David Sánchez', 20, 2),
('Pixel', 'Clara Ruiz', 18, 2),
('Thunder', 'Javier Pérez', 24, 3),
('Byte', 'María Fernández', 21, 3),
('Ghost', 'Andrés Gil', 22, 4),
('Nova', 'Elena Vidal', 20, 4),
('Razor', 'Iker Alonso', 23, 5),
('Cipher', 'Lucía Navarro', 19, 6);

-- Partides
INSERT INTO partides (id_equip_local, id_equip_visitant, punts_local, punts_visitant, data, joc) VALUES
(1, 2, 16, 14, '2025-01-10', 'Valorant'),
(3, 1, 10, 13, '2025-01-12', 'League of Legends'),
(1, 4, 3, 1, '2025-01-15', 'Rocket League'),
(5, 1, 16, 16, '2025-01-18', 'Valorant'),
(2, 3, 8, 13, '2025-01-11', 'League of Legends'),
(4, 2, 2, 3, '2025-01-14', 'Rocket League'),
(1, 6, 13, 7, '2025-01-20', 'League of Legends'),
(6, 3, 11, 13, '2025-01-22', 'Valorant'),
(2, 5, 16, 12, '2025-01-25', 'Valorant'),
(4, 6, 2, 2, '2025-01-27', 'Rocket League'),
(3, 4, 13, 9, '2025-01-28', 'League of Legends'),
(1, 3, 14, 16, '2025-02-01', 'Valorant'),
(5, 6, 1, 3, '2025-02-03', 'Rocket League'),
(2, 1, 9, 13, '2025-02-05', 'League of Legends');
```
