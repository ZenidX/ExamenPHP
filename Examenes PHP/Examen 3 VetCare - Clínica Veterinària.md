# EXAMEN 3: VetCare — Clínica Veterinària

## EXAMEN UF1 — Avaluació RA3 (5 punts)

**Durada: 1 hora**

1. Desenvolupa la següent aplicació: (5p)

Crea el directori **nomCognomExamenM9** amb els fitxers `index.html` i `query.php` (com a mínim, pots crear més fitxers si ho necessites).

**No s'ha de tindre en compte el control d'errors, suposarem que l'usuari escriu tot correctament.**

**Es poden consultar els apunts i pràctiques realitzades. La detecció d'ús de qualsevol altre pàgina o ús d'alguna IA (durant o després de l'examen), comporta un 0 a tota la prova d'avaluació.**

**S'ha d'utilitzar la llibreria i funcions explicades a classe.**

Importa el fitxer `vetcare.sql` a la teva base de dades i segueix les instruccions:

## 📄 enunciat_vetcare.txt

```
EXAMEN RA3 — VetCare (Clínica Veterinària)

1. Importa el fitxer vetcare.sql a la teva base de dades.

2. index.html
   - Crea un formulari amb un camp de text on l'usuari pugui escriure
     una ESPÈCIE de mascota (ex: "Gos", "Gat", "Conill"...).
   - El formulari enviarà les dades a query.php mitjançant POST.

3. query.php
   - Connecta't a la base de dades.
   - Realitza una consulta que mostri totes les visites de mascotes
     de l'espècie indicada, juntament amb les dades de la mascota
     i del propietari.
   - Mostra els resultats en una TAULA HTML amb les columnes:
     Mascota | Raça | Propietari | Telèfon | Data Visita | Diagnòstic | Cost (€)
   - A sota de la taula, mostra:
     · El nombre total de visites trobades.
     · El cost total de totes les visites.
     · El cost mitjà per visita (amb 2 decimals).
   - Si no es troben resultats, mostra el missatge:
     "No s'han trobat visites per a l'espècie indicada."
```

### CRITERIS

- Connexió a la BBDD (1,25p)
- Consulta (1,5p)
- Tractament de dades (2,25p)

### ENTREGA

S'ha de penjar tot al Moodle abans de finalitzar l'hora d'examen.

## 💾 vetcare.sql

```sql
-- =============================================
-- VetCare — Clínica Veterinària
-- =============================================

DROP DATABASE IF EXISTS vetcare;
CREATE DATABASE vetcare CHARACTER SET utf8mb4 COLLATE utf8mb4_general_ci;
USE vetcare;

CREATE TABLE propietaris (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nom VARCHAR(100) NOT NULL,
    telefon VARCHAR(15) NOT NULL,
    email VARCHAR(100) NOT NULL
);

CREATE TABLE mascotes (
    id INT AUTO_INCREMENT PRIMARY KEY,
    nom VARCHAR(50) NOT NULL,
    especie VARCHAR(30) NOT NULL,
    raca VARCHAR(50) NOT NULL,
    edat INT NOT NULL,
    id_propietari INT NOT NULL,
    FOREIGN KEY (id_propietari) REFERENCES propietaris(id)
);

CREATE TABLE visites (
    id INT AUTO_INCREMENT PRIMARY KEY,
    id_mascota INT NOT NULL,
    data_visita DATE NOT NULL,
    diagnostic VARCHAR(200) NOT NULL,
    cost DECIMAL(6,2) NOT NULL,
    FOREIGN KEY (id_mascota) REFERENCES mascotes(id)
);

-- Propietaris
INSERT INTO propietaris (nom, telefon, email) VALUES
('Maria Puig', '612345678', 'maria.puig@email.com'),
('Joan Ferrer', '623456789', 'joan.ferrer@email.com'),
('Laura Costa', '634567890', 'laura.costa@email.com'),
('Pere Soler', '645678901', 'pere.soler@email.com'),
('Anna Vives', '656789012', 'anna.vives@email.com'),
('Oriol Mas', '667890123', 'oriol.mas@email.com'),
('Carla Roca', '678901234', 'carla.roca@email.com');

-- Mascotes
INSERT INTO mascotes (nom, especie, raca, edat, id_propietari) VALUES
('Max', 'Gos', 'Pastor Alemany', 5, 1),
('Luna', 'Gat', 'Siamès', 3, 1),
('Rocky', 'Gos', 'Bulldog', 7, 2),
('Mishi', 'Gat', 'Persa', 4, 3),
('Nemo', 'Peix', 'Peix Pallasso', 1, 3),
('Toby', 'Gos', 'Golden Retriever', 2, 4),
('Cleo', 'Gat', 'Bengalí', 6, 5),
('Bugs', 'Conill', 'Holland Lop', 2, 5),
('Thor', 'Gos', 'Husky Siberià', 4, 6),
('Mia', 'Gat', 'Maine Coon', 5, 7),
('Kiwi', 'Conill', 'Rex', 1, 7);

-- Visites
INSERT INTO visites (id_mascota, data_visita, diagnostic, cost) VALUES
(1, '2025-01-05', 'Vacunació anual', 45.00),
(1, '2025-01-20', 'Revisió de pell - dermatitis', 65.50),
(2, '2025-01-08', 'Esterilització', 120.00),
(3, '2025-01-10', 'Problemes articulars', 85.00),
(3, '2025-02-01', 'Seguiment articulacions', 40.00),
(4, '2025-01-12', 'Neteja dental', 55.00),
(5, '2025-01-15', 'Revisió general', 25.00),
(6, '2025-01-18', 'Vacunació cadell', 50.00),
(6, '2025-02-02', 'Desparasitació', 30.00),
(7, '2025-01-22', 'Infecció ocular', 70.00),
(8, '2025-01-25', 'Revisió dental', 35.00),
(9, '2025-01-28', 'Vacunació anual', 45.00),
(9, '2025-02-03', 'Tall d\'ungles i revisió', 20.00),
(10, '2025-01-30', 'Control de pes', 30.00),
(11, '2025-02-04', 'Revisió general', 35.00),
(1, '2025-02-05', 'Control dermatitis', 55.00);
```
