---
layout: default
title: "Examen 4: FestSound - Festival de Música"
---

# EXAMEN 4: FestSound — Festival de Música

## EXAMEN UF1 — Avaluació RA3 (5 punts)

**Durada: 1 hora**

1. Desenvolupa la següent aplicació: (5p)

Crea el directori **nomCognomExamenM9** amb els fitxers `index.html` i `query.php` (com a mínim, pots crear més fitxers si ho necessites).

**No s'ha de tindre en compte el control d'errors, suposarem que l'usuari escriu tot correctament.**

**Es poden consultar els apunts i pràctiques realitzades. La detecció d'ús de qualsevol altre pàgina o ús d'alguna IA (durant o després de l'examen), comporta un 0 a tota la prova d'avaluació.**

**S'ha d'utilitzar la llibreria i funcions explicades a classe.**

Importa el fitxer `festsound.sql` a la teva base de dades i segueix les instruccions:

## 📄 enunciat_festsound.txt

```
EXAMEN RA3 — FestSound (Festival de Música)

1. Importa el fitxer festsound.sql a la teva base de dades.

2. index.html
   - Crea un formulari amb un camp de tipus DATE on l'usuari pugui
     seleccionar una DATA (ex: 2025-07-18, 2025-07-19...).
   - El formulari enviarà les dades a query.php mitjançant POST.

3. query.php
   - Connecta't a la base de dades.
   - Realitza una consulta que mostri totes les actuacions programades
     per al dia seleccionat, juntament amb les dades de l'artista
     i de l'escenari.
   - Mostra els resultats en una TAULA HTML amb les columnes:
     Hora Inici | Hora Fi | Artista | Gènere | Escenari | Capacitat | Preu (€)
   - Els resultats han d'estar ordenats per hora d'inici.
   - A sota de la taula, mostra:
     · El nombre total d'actuacions del dia.
     · El preu mitjà de les entrades (amb 2 decimals).
     · L'escenari amb més capacitat que s'utilitza aquell dia.
   - Si no es troben resultats, mostra el missatge:
     "No hi ha actuacions programades per a la data indicada."
```

### CRITERIS

- Connexió a la BBDD (1,25p)
- Consulta (1,5p)
- Tractament de dades (2,25p)

### ENTREGA

S'ha de penjar tot al Moodle abans de finalitzar l'hora d'examen.

## 💾 festsound.sql

```sql
-- =============================================
-- FestSound — Festival de Música
-- =============================================

DROP DATABASE IF EXISTS festsound;
CREATE DATABASE festsound CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
USE festsound;

CREATE TABLE escenaris (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nom VARCHAR(100) NOT NULL,
    capacitat INT NOT NULL,
    ubicacio VARCHAR(100) NOT NULL
);

CREATE TABLE artistes (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nom VARCHAR(100) NOT NULL,
    genere_musical VARCHAR(50) NOT NULL,
    pais VARCHAR(50) NOT NULL
);

CREATE TABLE actuacions (
    id INT AUTO_INCREMENT PRIMARY KEY,
    id_artista INT NOT NULL,
    id_escenari INT NOT NULL,
    data DATE NOT NULL,
    hora_inici TIME NOT NULL,
    hora_fi TIME NOT NULL,
    preu DECIMAL(5,2) NOT NULL,
    FOREIGN KEY (id_artista) REFERENCES artistes(id),
    FOREIGN KEY (id_escenari) REFERENCES escenaris(id)
);

-- Escenaris
INSERT INTO escenaris (nom, capacitat, ubicacio) VALUES
('Escenari Principal', 15000, 'Zona Central'),
('Escenari Platja', 5000, 'Zona Platja'),
('Escenari Electrònic', 8000, 'Zona Nord'),
('Escenari Acústic', 2000, 'Zona Jardins'),
('Carpa Indie', 3000, 'Zona Sud');

-- Artistes
INSERT INTO artistes (nom, genere_musical, pais) VALUES
('Rosalía', 'Pop/Flamenc', 'Espanya'),
('Bad Bunny', 'Reggaeton', 'Puerto Rico'),
('Gorillaz', 'Rock Alternatiu', 'Regne Unit'),
('Daft Punk Legacy', 'Electrònica', 'França'),
('Manel', 'Indie Pop', 'Espanya'),
('Bomba Estéreo', 'Electrocúmbia', 'Colòmbia'),
('Disclosure', 'House', 'Regne Unit'),
('Sopa de Cabra', 'Rock', 'Espanya'),
('Peggy Gou', 'Techno', 'Corea del Sud'),
('Oques Grasses', 'Pop/Festiu', 'Espanya'),
('Nathy Peluso', 'R&B/Rap', 'Argentina'),
('Jamie xx', 'Electrònica', 'Regne Unit');

-- Actuacions (3 dies de festival: 18, 19 i 20 de juliol)
INSERT INTO actuacions (id_artista, id_escenari, data, hora_inici, hora_fi, preu) VALUES
-- Dia 18
(5, 5, '2025-07-18', '17:00:00', '18:00:00', 25.00),
(10, 4, '2025-07-18', '18:00:00', '19:30:00', 20.00),
(8, 2, '2025-07-18', '19:00:00', '20:30:00', 30.00),
(6, 1, '2025-07-18', '20:30:00', '22:00:00', 35.00),
(9, 3, '2025-07-18', '22:00:00', '00:30:00', 28.00),
(7, 3, '2025-07-18', '23:30:00', '01:30:00', 32.00),
-- Dia 19
(10, 5, '2025-07-19', '17:30:00', '18:30:00', 22.00),
(11, 2, '2025-07-19', '19:00:00', '20:30:00', 35.00),
(3, 1, '2025-07-19', '21:00:00', '22:30:00', 45.00),
(4, 3, '2025-07-19', '22:30:00', '00:30:00', 40.00),
(12, 3, '2025-07-19', '23:00:00', '01:00:00', 30.00),
-- Dia 20
(5, 4, '2025-07-20', '17:00:00', '18:00:00', 20.00),
(6, 2, '2025-07-20', '18:30:00', '20:00:00', 30.00),
(11, 5, '2025-07-20', '19:00:00', '20:00:00', 28.00),
(1, 1, '2025-07-20', '21:00:00', '23:00:00', 55.00),
(2, 1, '2025-07-20', '23:30:00', '01:30:00', 60.00),
(9, 3, '2025-07-20', '23:00:00', '02:00:00', 35.00);
```
