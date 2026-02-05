# EXAMEN 1: BiblioTech — Gestió de Biblioteca

## EXAMEN UF1 — Avaluació RA3 (5 punts)

**Durada: 1 hora**

1. Desenvolupa la següent aplicació: (5p)

Crea el directori **nomCognomExamenM9** amb els fitxers `index.html` i `query.php` (com a mínim, pots crear més fitxers si ho necessites).

**No s'ha de tindre en compte el control d'errors, suposarem que l'usuari escriu tot correctament.**

**Es poden consultar els apunts i pràctiques realitzades. La detecció d'ús de qualsevol altre pàgina o ús d'alguna IA (durant o després de l'examen), comporta un 0 a tota la prova d'avaluació.**

**S'ha d'utilitzar la llibreria i funcions explicades a classe.**

Importa el fitxer `bibliotech.sql` a la teva base de dades i segueix les instruccions:

## 📄 enunciat_bibliotech.txt

```
EXAMEN RA3 — BiblioTech (Gestió de Biblioteca)

1. Importa el fitxer bibliotech.sql a la teva base de dades.

2. index.html
   - Crea un formulari amb un camp de text on l'usuari pugui escriure
     un GÈNERE de llibre (ex: "Ciència-ficció", "Fantasia", "Terror"...).
   - El formulari enviarà les dades a query.php mitjançant POST.

3. query.php
   - Connecta't a la base de dades.
   - Realitza una consulta que mostri tots els llibres del gènere introduït,
     juntament amb el nom de l'autor i el seu país.
   - Mostra els resultats en una TAULA HTML amb les columnes:
     Títol | Autor | País | Any Publicació
   - A sota de la taula, mostra:
     · El nombre total de llibres trobats.
     · L'any de publicació més antic i el més recent.
   - Si no es troben resultats, mostra el missatge:
     "No s'han trobat llibres del gènere indicat."
```

### CRITERIS
- Connexió a la BBDD (1,25p)
- Consulta (1,5p)
- Tractament de dades (2,25p)

### ENTREGA
S'ha de penjar tot al Moodle abans de finalitzar l'hora d'examen.

## 💾 bibliotech.sql

```sql
-- =============================================
-- BiblioTech — Gestió de Biblioteca
-- =============================================

DROP DATABASE IF EXISTS bibliotech;
CREATE DATABASE bibliotech CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
USE bibliotech;

CREATE TABLE autors (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nom VARCHAR(100) NOT NULL,
    pais VARCHAR(50) NOT NULL,
    any_naixement INT NOT NULL
);

CREATE TABLE llibres (
    id INT AUTO_INCREMENT PRIMARY KEY,
    titol VARCHAR(150) NOT NULL,
    genere VARCHAR(50) NOT NULL,
    any_publicacio INT NOT NULL,
    id_autor INT NOT NULL,
    FOREIGN KEY (id_autor) REFERENCES autors(id)
);

-- Autors
INSERT INTO autors (nom, pais, any_naixement) VALUES
('Isaac Asimov', 'Rússia', 1920),
('Ursula K. Le Guin', 'Estats Units', 1929),
('J.R.R. Tolkien', 'Regne Unit', 1892),
('Stephen King', 'Estats Units', 1947),
('Agatha Christie', 'Regne Unit', 1890),
('Gabriel García Márquez', 'Colòmbia', 1927),
('Liu Cixin', 'Xina', 1963),
('Mary Shelley', 'Regne Unit', 1797),
('Frank Herbert', 'Estats Units', 1920),
('Terry Pratchett', 'Regne Unit', 1948);

-- Llibres
INSERT INTO llibres (titol, genere, any_publicacio, id_autor) VALUES
('Fundació', 'Ciència-ficció', 1951, 1),
('Jo, Robot', 'Ciència-ficció', 1950, 1),
('El fin de la eternidad', 'Ciència-ficció', 1955, 1),
('La mà esquerra de la foscor', 'Ciència-ficció', 1969, 2),
('Els desposseïts', 'Ciència-ficció', 2001, 2),
('El Senyor dels Anells', 'Fantasia', 1954, 3),
('El Hòbbit', 'Fantasia', 1937, 3),
('It', 'Terror', 1986, 4),
('El resplandor', 'Terror', 1977, 4),
('Misery', 'Terror', 1987, 4),
('Assassinat a l\'Orient Express', 'Misteri', 1934, 5),
('Deu negrets', 'Misteri', 1939, 5),
('Cent anys de solitud', 'Realisme màgic', 1967, 6),
('L\'amor en els temps del còlera', 'Realisme màgic', 1985, 6),
('El problema dels tres cossos', 'Ciència-ficció', 2008, 7),
('El bosc fosc', 'Ciència-ficció', 2015, 7),
('Frankenstein', 'Terror', 1818, 8),
('Dune', 'Ciència-ficció', 1965, 9),
('El color de la màgia', 'Fantasia', 1983, 10),
('Mort', 'Fantasia', 1987, 10);
```