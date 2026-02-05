---
layout: default
title: "Examen 5: StreamBox - Plataforma de Streaming"
---

# EXAMEN 5: StreamBox — Plataforma de Streaming

## EXAMEN UF1 — Avaluació RA3 (5 punts)

**Durada: 1 hora**

1. Desenvolupa la següent aplicació: (5p)

Crea el directori **nomCognomExamenM9** amb els fitxers `index.html` i `query.php` (com a mínim, pots crear més fitxers si ho necessites).

**No s'ha de tindre en compte el control d'errors, suposarem que l'usuari escriu tot correctament.**

**Es poden consultar els apunts i pràctiques realitzades. La detecció d'ús de qualsevol altre pàgina o ús d'alguna IA (durant o després de l'examen), comporta un 0 a tota la prova d'avaluació.**

**S'ha d'utilitzar la llibreria i funcions explicades a classe.**

Importa el fitxer `streambox.sql` a la teva base de dades i segueix les instruccions:

## 📄 enunciat_streambox.txt

```
EXAMEN RA3 — StreamBox (Plataforma de Streaming)

1. Importa el fitxer streambox.sql a la teva base de dades.

2. index.html
   - Crea un formulari amb un camp de tipus NUMBER on l'usuari pugui
     escriure una PUNTUACIÓ MÍNIMA (de 1 a 10).
   - El formulari enviarà les dades a query.php mitjançant POST.

3. query.php
   - Connecta't a la base de dades.
   - Realitza una consulta que mostri totes les valoracions que tinguin
     una puntuació igual o superior a la indicada, juntament amb les
     dades de la sèrie i la seva categoria.
   - Mostra els resultats en una TAULA HTML amb les columnes:
     Sèrie | Categoria | Temporades | Usuari | Puntuació | Comentari
   - Els resultats han d'estar ordenats per puntuació de major a menor.
   - A sota de la taula, mostra:
     · El nombre total de valoracions trobades.
     · La puntuació mitjana de les valoracions mostrades (amb 2 decimals).
     · El nom de la sèrie amb la puntuació més alta.
   - Si no es troben resultats, mostra el missatge:
     "No s'han trobat valoracions amb la puntuació mínima indicada."
```

### CRITERIS

- Connexió a la BBDD (1,25p)
- Consulta (1,5p)
- Tractament de dades (2,25p)

### ENTREGA

S'ha de penjar tot al Moodle abans de finalitzar l'hora d'examen.
Es pot entregar mitjançant un archiu comprimit .zip o url a un repositori de github public o on zenidx sigui colaborador.
Per a aquest examen si que es tindrà en compte l'última versió/commit que hi hagi al repositori amb data dintre de l'hora d'examen.

## 💾 streambox.sql

```sql
-- =============================================
-- StreamBox — Plataforma de Streaming
-- =============================================

DROP DATABASE IF EXISTS streambox;
CREATE DATABASE streambox CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
USE streambox;

CREATE TABLE categories (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nom VARCHAR(50) NOT NULL,
    descripcio VARCHAR(200) NOT NULL
);

CREATE TABLE series (
    id INT AUTO_INCREMENT PRIMARY KEY,
    titol VARCHAR(150) NOT NULL,
    temporades INT NOT NULL,
    any_estrena INT NOT NULL,
    id_categoria INT NOT NULL,
    FOREIGN KEY (id_categoria) REFERENCES categories(id)
);

CREATE TABLE valoracions (
    id INT AUTO_INCREMENT PRIMARY KEY,
    id_serie INT NOT NULL,
    usuari VARCHAR(50) NOT NULL,
    puntuacio INT NOT NULL,
    comentari VARCHAR(200) NOT NULL,
    data DATE NOT NULL,
    FOREIGN KEY (id_serie) REFERENCES series(id)
);

-- Categories
INSERT INTO categories (nom, descripcio) VALUES
('Drama', 'Sèries amb trames emocionals i conflictes profunds'),
('Ciència-ficció', 'Sèries ambientades en futurs o realitats alternatives'),
('Comèdia', 'Sèries amb contingut humorístic i situacions còmiques'),
('Thriller', 'Sèries de suspens i tensió psicològica'),
('Fantasia', 'Sèries amb mons imaginaris i elements màgics'),
('Documental', 'Sèries basades en fets reals i investigació');

-- Sèries
INSERT INTO series (titol, temporades, any_estrena, id_categoria) VALUES
('Breaking Bad', 5, 2008, 1),
('Black Mirror', 6, 2011, 2),
('The Office', 9, 2005, 3),
('True Detective', 4, 2014, 4),
('The Witcher', 3, 2019, 5),
('Planet Earth', 3, 2006, 6),
('Stranger Things', 5, 2016, 2),
('Fleabag', 2, 2016, 3),
('Dark', 3, 2017, 2),
('Chernobyl', 1, 2019, 1),
('The Mandalorian', 3, 2019, 5),
('Making a Murderer', 2, 2015, 6);

-- Valoracions
INSERT INTO valoracions (id_serie, usuari, puntuacio, comentari, data) VALUES
(1, 'cinefil_99', 10, 'Obra mestra absoluta, cada episodi és perfecte', '2025-01-05'),
(1, 'seriesfan', 9, 'Increïble desenvolupament de personatges', '2025-01-08'),
(2, 'techlover', 8, 'Capítols molt desiguals però els millors són genials', '2025-01-10'),
(2, 'anna_bcn', 6, 'Algunes temporades baixen molt de nivell', '2025-01-12'),
(3, 'riure_sempre', 9, 'La millor comèdia de tots els temps', '2025-01-06'),
(3, 'pau_girona', 7, 'Divertida però es fa llarga', '2025-01-14'),
(4, 'mystery_fan', 9, 'La primera temporada és insuperable', '2025-01-15'),
(4, 'detectiu_amateur', 5, 'Només val la pena la T1', '2025-01-18'),
(5, 'gamer_pro', 6, 'No està a l\'altura dels llibres', '2025-01-20'),
(5, 'fantasia_cat', 8, 'Molt bona ambientació i acció', '2025-01-22'),
(6, 'natura_lover', 10, 'Imatges impressionants, imprescindible', '2025-01-09'),
(7, 'nostalgia_80', 9, 'Perfecta barreja de terror i aventura', '2025-01-11'),
(7, 'scifi_nerd', 7, 'Bona però massa fan service a les últimes', '2025-01-25'),
(8, 'comedy_queen', 10, 'Genial, curta i perfecta', '2025-01-13'),
(9, 'dark_fan', 10, 'La millor sèrie de ciència-ficció mai feta', '2025-01-16'),
(9, 'confused_viewer', 4, 'Massa complicada, em vaig perdre', '2025-01-19'),
(10, 'historia_viva', 9, 'Impactant i necessària', '2025-01-21'),
(10, 'pere_tarragona', 8, 'Molt ben feta però dura de veure', '2025-01-24'),
(11, 'starwars_fan', 8, 'El millor de Star Wars en anys', '2025-01-23'),
(11, 'cinefil_99', 7, 'Entretinguda però previsible', '2025-01-26'),
(12, 'true_crime', 8, 'Fascinant i pertorbadora', '2025-01-27'),
(12, 'anna_bcn', 6, 'Interessant però s\'allarga massa', '2025-01-28'),
(1, 'marta_vlc', 10, 'L\'he vist 3 vegades i cada cop és millor', '2025-02-01'),
(7, 'marta_vlc', 8, 'Molt recomanable per a tota la família', '2025-02-03');
```
