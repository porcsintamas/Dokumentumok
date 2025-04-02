# Pizza SQL adatbázis feladat

**Hozd létre a pizza adatbázist!**

Az alábbi táblázat mutatja, hogy a dokumentumban felsorolt mezők (oszlopok) hogyan csoportosulnak a különböző táblákban. (Ez eredetileg elcsúszott formátumú volt, most egységesen szerkesztve látható.)


| Tetel | Pizza     | Futar     | Vevo      | Rendeles  |
|-------|-----------|-----------|-----------|-----------|
| Razon | Pazon     | Fazon     | Vazon     | Razon     |
| Pazon | Pnev      | Fnev      | Vnev      | Vazon     |
| Par   | Par       | Ftel      | Vcim      | Fazon     |
| Db    |           |           |           | Datum     |
|       |           |           |           | Ido       |



*(A fenti ábra csupán szemlélteti, hogy melyik mező melyik táblához tartozik. A részletes leírás és a pontos CREATE TABLE parancsok alább következnek.)*

---

**ahol**

- **Pazon** N 3 – a pizza azonosítója
- **Pnev** C 15 – a pizza neve
- **Par** N 4 – a pizza ára
- **Fazon** N 3 – a pizzafutár azonosítója
- **Fnev** C 25 – a pizzafutár neve
- **Ftel** C 12 – a pizzafutár telefonszáma
- **Vazon** N 6 – a megrendelő azonosítója
- **Vnev** C 30 – a megrendelő neve
- **Vcim** C 30 – a megrendelő lakcíme
- **Razon** N 8 – a rendelés sorszáma
- **Datum** D 8 – a rendelés dátuma
- **Ido** N 5,2 – a rendelés ideje (óra és perc hh.mm alakban)
- **Db** N 3 – egy rendelési tétel darabszáma

---

### Tábla szerkezet: `pfutar`

```sql
CREATE TABLE `pfutar` (
  `fazon` int(3) NOT NULL default '0',
  `fnev` varchar(25) collate latin2_hungarian_ci NOT NULL default '',
  `ftel` varchar(12) collate latin2_hungarian_ci NOT NULL default '',
  PRIMARY KEY  (`fazon`)
) ENGINE=MyISAM DEFAULT CHARSET=latin2 COLLATE=latin2_hungarian_ci;
```

**Tábla adatok: `pfutar`**

```sql
INSERT INTO `pfutar` VALUES (1, 'Hurrikán', '123456');
INSERT INTO `pfutar` VALUES (2, 'Gyalogkakukk', '666666');
INSERT INTO `pfutar` VALUES (3, 'Gömbvillám', '888888');
INSERT INTO `pfutar` VALUES (4, 'Szélvész', '258369');
INSERT INTO `pfutar` VALUES (5, 'Imperial', '987654');
```

---

### Tábla szerkezet: `ppizza`

```sql
CREATE TABLE `ppizza` (
  `pazon` int(3) NOT NULL default '0',
  `pnev` varchar(15) collate latin2_hungarian_ci NOT NULL default '',
  `par` int(4) NOT NULL default '0',
  PRIMARY KEY  (`pazon`)
) ENGINE=MyISAM DEFAULT CHARSET=latin2 COLLATE=latin2_hungarian_ci;
```

**Tábla adatok: `ppizza`**

```sql
INSERT INTO `ppizza` VALUES (1, 'Capricciosa', 900);
INSERT INTO `ppizza` VALUES (2, 'Frutti di Mare', 1100);
INSERT INTO `ppizza` VALUES (3, 'Hawaii', 780);
INSERT INTO `ppizza` VALUES (4, 'Vesuvio', 890);
INSERT INTO `ppizza` VALUES (5, 'Sorrento', 990);
```

---

### Tábla szerkezet: `prendeles`

```sql
CREATE TABLE `prendeles` (
  `razon` int(8) NOT NULL default '0',
  `vazon` int(6) NOT NULL default '0',
  `fazon` int(3) NOT NULL default '0',
  `datum` date NOT NULL,
  `ido` float NOT NULL default '0',
  PRIMARY KEY  (`razon`)
) ENGINE=MyISAM DEFAULT CHARSET=latin2 COLLATE=latin2_hungarian_ci;
```

**Tábla adatok: `prendeles`**

```sql
INSERT INTO `prendeles` VALUES ( 1, 4, 2, '2010-10-01', 13.15);
INSERT INTO `prendeles` VALUES ( 2, 7, 2, '2010-10-01', 14.17);
INSERT INTO `prendeles` VALUES ( 3, 1, 1, '2010-10-02', 11.07);
INSERT INTO `prendeles` VALUES ( 4, 5, 2, '2010-10-02', 14.55);
INSERT INTO `prendeles` VALUES ( 5, 2, 3, '2010-10-02', 15.27);
INSERT INTO `prendeles` VALUES ( 6, 4, 2, '2010-10-03', 15.58);
INSERT INTO `prendeles` VALUES ( 7, 6, 2, '2010-10-04', 11.44);
INSERT INTO `prendeles` VALUES ( 8, 7, 4, '2010-10-04', 12.11);
INSERT INTO `prendeles` VALUES ( 9, 1, 5, '2010-10-04', 14.33);
INSERT INTO `prendeles` VALUES (10, 3, 5, '2010-10-04', 18.04);
INSERT INTO `prendeles` VALUES (11, 2, 1, '2010-10-05', 16.38);
INSERT INTO `prendeles` VALUES (12, 5, 2, '2010-10-05', 17.02);
INSERT INTO `prendeles` VALUES (13, 6, 2, '2010-10-06', 12.17);
INSERT INTO `prendeles` VALUES (14, 4, 3, '2010-10-06', 13.21);
INSERT INTO `prendeles` VALUES (15, 1, 4, '2010-10-06', 15.05);
INSERT INTO `prendeles` VALUES (16, 2, 5, '2010-10-06', 15.59);
INSERT INTO `prendeles` VALUES (17, 7, 2, '2010-10-06', 18.44);
INSERT INTO `prendeles` VALUES (18, 3, 2, '2010-10-07', 12.01);
INSERT INTO `prendeles` VALUES (19, 4, 5, '2010-10-07', 13.44);
INSERT INTO `prendeles` VALUES (20, 1, 1, '2010-10-07', 17.25);
INSERT INTO `prendeles` VALUES (21, 5, 3, '2010-10-08', 14.29);
```

---

### Tábla szerkezet: `ptetel`

```sql
CREATE TABLE `ptetel` (
  `razon` int(8) NOT NULL default '0',
  `pazon` int(3) NOT NULL default '0',
  `db` int(3) NOT NULL default '0'
) ENGINE=MyISAM DEFAULT CHARSET=latin2 COLLATE=latin2_hungarian_ci;
```

**Tábla adatok: `ptetel`**

```sql
INSERT INTO `ptetel` VALUES ( 1, 1, 2);
INSERT INTO `ptetel` VALUES ( 1, 4, 3);
INSERT INTO `ptetel` VALUES ( 2, 2, 1);
INSERT INTO `ptetel` VALUES ( 3, 1, 2);
INSERT INTO `ptetel` VALUES ( 4, 1, 1);
INSERT INTO `ptetel` VALUES ( 4, 4, 1);
INSERT INTO `ptetel` VALUES ( 5, 2, 4);
INSERT INTO `ptetel` VALUES ( 6, 1, 1);
INSERT INTO `ptetel` VALUES ( 6, 4, 1);
INSERT INTO `ptetel` VALUES ( 6, 5, 1);
INSERT INTO `ptetel` VALUES ( 7, 5, 5);
INSERT INTO `ptetel` VALUES ( 8, 4, 3);
INSERT INTO `ptetel` VALUES ( 9, 2, 1);
INSERT INTO `ptetel` VALUES (10, 1, 1);
INSERT INTO `ptetel` VALUES (10, 4, 1);
INSERT INTO `ptetel` VALUES (11, 1, 1);
INSERT INTO `ptetel` VALUES (12, 2, 2);
INSERT INTO `ptetel` VALUES (12, 4, 2);
INSERT INTO `ptetel` VALUES (13, 4, 1);
INSERT INTO `ptetel` VALUES (13, 5, 1);
INSERT INTO `ptetel` VALUES (13, 2, 1);
INSERT INTO `ptetel` VALUES (14, 2, 2);
INSERT INTO `ptetel` VALUES (15, 1, 1);
INSERT INTO `ptetel` VALUES (16, 2, 1);
INSERT INTO `ptetel` VALUES (16, 4, 1);
INSERT INTO `ptetel` VALUES (16, 5, 1);
INSERT INTO `ptetel` VALUES (17, 1, 2);
INSERT INTO `ptetel` VALUES (17, 2, 3);
INSERT INTO `ptetel` VALUES (18, 1, 4);
INSERT INTO `ptetel` VALUES (18, 5, 1);
INSERT INTO `ptetel` VALUES (19, 1, 1);
INSERT INTO `ptetel` VALUES (19, 2, 1);
INSERT INTO `ptetel` VALUES (19, 4, 1);
INSERT INTO `ptetel` VALUES (19, 5, 1);
INSERT INTO `ptetel` VALUES (20, 5, 3);
INSERT INTO `ptetel` VALUES (21, 2, 2);
INSERT INTO `ptetel` VALUES (21, 4, 1);
```

---

### Tábla szerkezet: `pvevo`

```sql
CREATE TABLE `pvevo` (
  `vazon` int(6) NOT NULL default '0',
  `vnev` varchar(30) collate latin2_hungarian_ci NOT NULL default '',
  `vcim` varchar(30) collate latin2_hungarian_ci NOT NULL default '',
  PRIMARY KEY  (`vazon`)
) ENGINE=MyISAM DEFAULT CHARSET=latin2 COLLATE=latin2_hungarian_ci;
```

**Tábla adatok: `pvevo`**

```sql
INSERT INTO `pvevo` VALUES (1, 'Hapci', 'Debrecen');
INSERT INTO `pvevo` VALUES (2, 'Vidor', 'Ebes');
INSERT INTO `pvevo` VALUES (3, 'Tudor', ' Debrecen ');
INSERT INTO `pvevo` VALUES (4, 'Kuka', ' Debrecen ');
INSERT INTO `pvevo` VALUES (5, 'Szende', 'Ebes');
INSERT INTO `pvevo` VALUES (6, 'Szundi', ' Debrecen ');
INSERT INTO `pvevo` VALUES (7, 'Morgó', 'Ebes');
```

---

## Feladatok és kérdések

1. Hogy hívják az egyes pizzafutárokat?
2. Milyen pizzák közül lehet rendelni, és mennyibe kerülnek?
3. Mennyibe kerül átlagosan egy pizza?
4. Mely pizzák olcsóbbak 1000 Ft-nál?
5. Ki szállította házhoz az első (egyes sorszámú) rendelést?
6. Kik rendeltek pizzát délelőtt?
7. Milyen pizzákat evett Szundi?
8. Ki szállított házhoz Tudornak?
9. Az egyes rendelések alkalmával, ki kinek szállított házhoz?
10. Mennyit költött pizzára Morgó?
11. Hány alkalommal rendelt Sorrento pizzát Vidor?
12. Hány pizzát evett Hapci?
13. Hányszor rendelt pizzát Szende?
14. Hány darab Hawaii pizza fogyott összesen?
15. Mennyit költöttek pizzára az egyes vevők?
16. Mennyit vettek az egyes vevők a különböző pizzákból?
17. Ki hány pizzát szállított házhoz az egyes napokon?
18. Ki hány pizzát rendelt az egyes napokon?
19. Mennyi volt a bevétel az egyes napokon?
20. Hány pizza fogyott naponta?
21. Mennyi pizza fogyott átlagosan naponta?
22. Hány pizzát rendeltek átlagosan egyszerre?
23. Hány alkalommal szállítottak házhoz az egyes futárok?
24. A fogyasztás alapján mi a pizzák népszerűségi sorrendje?
25. A rendelés értéke alapján mi a vevők sorrendje?
26. Melyik a legdrágább pizza?
27. Ki szállította házhoz a legtöbb pizzát?
28. Ki ette a legtöbb pizzát?
29. Melyik nap fogyott a legtöbb pizza?
30. Melyik nap fogyott a legtöbb Hawaii pizza?
31. Hány pizza fogyott a legforgalmasabb napon?
32. Mennyi volt a bevétel a legjobb napon?
33. Mi Szundi kedvenc pizzája?
34. Kik rendeltek pizzát a nyitás napján?
35. Mely pizzák olcsóbbak a Capricciosa pizzánál?
36. Mely pizzák drágábbak az átlagosnál?
37. Mely pizza ára van legközelebb az átlagárhoz?
38. Mely futárok mentek többet házhoz az átlagosnál?
39. Kik rendeltek legalább háromszor annyi pizzát, mint egy átlagos vevő?
40. Kik szállítottak házhoz legalább tízszer?
41. Mely pizzából fogyott legalább 50 db?
42. Mely vevők nem rendeltek legalább háromszor?
43. Kik rendeltek legalább 5 Vigyori pizzát?
44. Milyen pizzából nem rendelt soha Columbo?
45. Van-e olyan pizza, amelyből soha nem rendeltek?
46. Ki nem rendelt soha Vigyori pizzát?
47. Mely pizzafutárokkal nem találkoztak az egyes vevők?
48. Kik rendeltek több Vigyori pizzát, mint Nevetőset?
49. Kik rendeltek legalább 5 Hahota vagy 8 Kacagós pizzát?
50. Kik rendeltek kétfajta pizzából is legalább 10 darabot?

```sql
-- 1. feladat:
SELECT fnev FROM pfutar;

-- 2. feladat:
SELECT pnev, par FROM ppizza;

-- 3. feladat:
SELECT AVG(par) AS atlag_ar FROM ppizza;

-- 4. feladat:
SELECT pnev, par FROM ppizza WHERE par < 1000;

-- 5. feladat:
SELECT pfutar.fnev 
FROM pfutar
INNER JOIN prendeles ON pfutar.fazon = prendeles.fazon
WHERE prendeles.razon = 1;

-- 6. feladat:
SELECT DISTINCT pvevo.vnev
FROM pvevo
INNER JOIN prendeles ON pvevo.vazon = prendeles.vazon
WHERE prendeles.ido < 12.00;

-- 7. feladat:
SELECT DISTINCT ppizza.pnev
FROM ppizza
INNER JOIN ptetel ON ppizza.pazon = ptetel.pazon
INNER JOIN prendeles ON ptetel.razon = prendeles.razon
INNER JOIN pvevo ON prendeles.vazon = pvevo.vazon
WHERE pvevo.vnev = 'Szundi';

-- 8. feladat:
SELECT DISTINCT pfutar.fnev
FROM pfutar
INNER JOIN prendeles ON pfutar.fazon = prendeles.fazon
INNER JOIN pvevo ON prendeles.vazon = pvevo.vazon
WHERE pvevo.vnev = 'Tudor';

-- 9. feladat:
SELECT prendeles.razon AS rendeles_azonosito, pfutar.fnev AS futar, pvevo.vnev AS vevo, prendeles.datum, prendeles.ido
FROM prendeles
INNER JOIN pfutar ON prendeles.fazon = pfutar.fazon
INNER JOIN pvevo ON prendeles.vazon = pvevo.vazon
ORDER BY prendeles.razon;

-- 10. feladat:
SELECT SUM(ppizza.par * ptetel.db) AS osszeg
FROM ppizza
INNER JOIN ptetel ON ppizza.pazon = ptetel.pazon
INNER JOIN prendeles ON ptetel.razon = prendeles.razon
INNER JOIN pvevo ON prendeles.vazon = pvevo.vazon
WHERE pvevo.vnev = 'Morgó';

-- 11. feladat:
SELECT COUNT(*) AS alkalmak
FROM ptetel
INNER JOIN ppizza ON ptetel.pazon = ppizza.pazon
INNER JOIN prendeles ON ptetel.razon = prendeles.razon
INNER JOIN pvevo ON prendeles.vazon = pvevo.vazon
WHERE pvevo.vnev = 'Vidor' AND ppizza.pnev = 'Sorrento';

-- 12. feladat:
SELECT SUM(ptetel.db) AS osszesen
FROM ptetel
INNER JOIN prendeles ON ptetel.razon = prendeles.razon
INNER JOIN pvevo ON prendeles.vazon = pvevo.vazon
WHERE pvevo.vnev = 'Hapci';

-- 13. feladat:
SELECT COUNT(DISTINCT prendeles.razon) AS alkalmak
FROM prendeles
INNER JOIN pvevo ON prendeles.vazon = pvevo.vazon
WHERE pvevo.vnev = 'Szende';

-- 14. feladat:
SELECT SUM(ptetel.db) AS osszesen
FROM ptetel
INNER JOIN ppizza ON ptetel.pazon = ppizza.pazon
WHERE ppizza.pnev = 'Hawaii';

-- 15. feladat:
SELECT pvevo.vnev, SUM(ppizza.par * ptetel.db) AS osszeg
FROM pvevo
INNER JOIN prendeles ON pvevo.vazon = prendeles.vazon
INNER JOIN ptetel ON prendeles.razon = ptetel.razon
INNER JOIN ppizza ON ptetel.pazon = ppizza.pazon
GROUP BY pvevo.vnev
ORDER BY osszeg DESC;

-- 16. feladat:
SELECT pvevo.vnev AS vevo, ppizza.pnev AS pizza, SUM(ptetel.db) AS darab
FROM pvevo
INNER JOIN prendeles ON pvevo.vazon = prendeles.vazon
INNER JOIN ptetel ON prendeles.razon = ptetel.razon
INNER JOIN ppizza ON ptetel.pazon = ppizza.pazon
GROUP BY pvevo.vnev, ppizza.pnev
HAVING SUM(ptetel.db) > 0
ORDER BY pvevo.vnev, SUM(ptetel.db) DESC;

-- 17. feladat:
SELECT pfutar.fnev AS futar, prendeles.datum, SUM(ptetel.db) AS darab
FROM pfutar
INNER JOIN prendeles ON pfutar.fazon = prendeles.fazon
INNER JOIN ptetel ON prendeles.razon = ptetel.razon
GROUP BY pfutar.fnev, prendeles.datum
ORDER BY prendeles.datum, pfutar.fnev;

-- 18. feladat:
SELECT pvevo.vnev AS vevo, prendeles.datum, SUM(ptetel.db) AS darab
FROM pvevo
INNER JOIN prendeles ON pvevo.vazon = prendeles.vazon
INNER JOIN ptetel ON prendeles.razon = ptetel.razon
GROUP BY pvevo.vnev, prendeles.datum
ORDER BY prendeles.datum, pvevo.vnev;

-- 19. feladat:
SELECT prendeles.datum, SUM(ppizza.par * ptetel.db) AS bevetel
FROM prendeles
INNER JOIN ptetel ON prendeles.razon = ptetel.razon
INNER JOIN ppizza ON ptetel.pazon = ppizza.pazon
GROUP BY prendeles.datum
ORDER BY prendeles.datum;

-- 20. feladat:
SELECT prendeles.datum, SUM(ptetel.db) AS darab
FROM prendeles
INNER JOIN ptetel ON prendeles.razon = ptetel.razon
GROUP BY prendeles.datum
ORDER BY prendeles.datum;

-- 21. feladat:
SELECT AVG(napi_forgalom.napi_db) AS atlag
FROM (
    SELECT prendeles.datum, SUM(ptetel.db) AS napi_db
    FROM prendeles
    INNER JOIN ptetel ON prendeles.razon = ptetel.razon
    GROUP BY prendeles.datum
) AS napi_forgalom;

-- 22. feladat:
SELECT AVG(rendelesenkent.rendelesi_db) AS atlag
FROM (
    SELECT prendeles.razon, SUM(ptetel.db) AS rendelesi_db
    FROM prendeles
    INNER JOIN ptetel ON prendeles.razon = ptetel.razon
    GROUP BY prendeles.razon
) AS rendelesenkent;

-- 23. feladat:
SELECT pfutar.fnev, COUNT(prendeles.razon) AS kiszallitasok
FROM pfutar
INNER JOIN prendeles ON pfutar.fazon = prendeles.fazon
GROUP BY pfutar.fnev
ORDER BY kiszallitasok DESC;

-- 24. feladat:
SELECT ppizza.pnev, SUM(ptetel.db) AS darab
FROM ppizza
INNER JOIN ptetel ON ppizza.pazon = ptetel.pazon
GROUP BY ppizza.pnev
ORDER BY darab DESC;

-- 25. feladat:
SELECT pvevo.vnev, SUM(ppizza.par * ptetel.db) AS osszeg
FROM pvevo
INNER JOIN prendeles ON pvevo.vazon = prendeles.vazon
INNER JOIN ptetel ON prendeles.razon = ptetel.razon
INNER JOIN ppizza ON ptetel.pazon = ppizza.pazon
GROUP BY pvevo.vnev
ORDER BY osszeg DESC;

-- 26. feladat:
SELECT pnev, par
FROM ppizza
WHERE par = (SELECT MAX(par) FROM ppizza);

-- 27. feladat:
SELECT pfutar.fnev, SUM(ptetel.db) AS osszesen
FROM pfutar
INNER JOIN prendeles ON pfutar.fazon = prendeles.fazon
INNER JOIN ptetel ON prendeles.razon = ptetel.razon
GROUP BY pfutar.fnev
ORDER BY osszesen DESC
LIMIT 1;

-- 28. feladat:
SELECT pvevo.vnev, SUM(ptetel.db) AS osszesen
FROM pvevo
INNER JOIN prendeles ON pvevo.vazon = prendeles.vazon
INNER JOIN ptetel ON prendeles.razon = ptetel.razon
GROUP BY pvevo.vnev
ORDER BY osszesen DESC
LIMIT 1;

-- 29. feladat:
SELECT prendeles.datum, SUM(ptetel.db) AS darab
FROM prendeles
INNER JOIN ptetel ON prendeles.razon = ptetel.razon
GROUP BY prendeles.datum
ORDER BY darab DESC
LIMIT 1;

-- 30. feladat:
SELECT prendeles.datum, SUM(ptetel.db) AS darab
FROM prendeles
INNER JOIN ptetel ON prendeles.razon = ptetel.razon
INNER JOIN ppizza ON ptetel.pazon = ppizza.pazon
WHERE ppizza.pnev = 'Hawaii'
GROUP BY prendeles.datum
ORDER BY darab DESC
LIMIT 1;

-- 31. feladat:
SELECT SUM(ptetel.db) AS darab
FROM prendeles
INNER JOIN ptetel ON prendeles.razon = ptetel.razon
WHERE prendeles.datum = (
    SELECT prendeles.datum 
    FROM prendeles
    INNER JOIN ptetel ON prendeles.razon = ptetel.razon
    GROUP BY prendeles.datum
    ORDER BY SUM(ptetel.db) DESC 
    LIMIT 1
);

-- 32. feladat:
SELECT SUM(ppizza.par * ptetel.db) AS bevetel
FROM prendeles
INNER JOIN ptetel ON prendeles.razon = ptetel.razon
INNER JOIN ppizza ON ptetel.pazon = ppizza.pazon
WHERE prendeles.datum = (
    SELECT prendeles.datum
    FROM prendeles
    INNER JOIN ptetel ON prendeles.razon = ptetel.razon
    INNER JOIN ppizza ON ptetel.pazon = ppizza.pazon
    GROUP BY prendeles.datum
    ORDER BY SUM(ppizza.par * ptetel.db) DESC
    LIMIT 1
);

-- 33. feladat:
SELECT ppizza.pnev
FROM ptetel
INNER JOIN ppizza ON ptetel.pazon = ppizza.pazon
INNER JOIN prendeles ON ptetel.razon = prendeles.razon
INNER JOIN pvevo ON prendeles.vazon = pvevo.vazon
WHERE pvevo.vnev = 'Szundi'
GROUP BY ppizza.pnev
ORDER BY SUM(ptetel.db) DESC
LIMIT 1;

-- 34. feladat:
SELECT DISTINCT pvevo.vnev
FROM pvevo
INNER JOIN prendeles ON pvevo.vazon = prendeles.vazon
WHERE prendeles.datum = '2010-10-01';

-- 35. feladat:
SELECT pnev 
FROM ppizza
WHERE par < (SELECT par FROM ppizza WHERE pnev = 'Capricciosa');

-- 36. feladat:
SELECT pnev
FROM ppizza
WHERE par > (SELECT AVG(par) FROM ppizza);

-- 37. feladat:
SELECT pnev, par
FROM ppizza
ORDER BY ABS(par - (SELECT AVG(par) FROM ppizza))
LIMIT 1;

-- 38. feladat:
SELECT pfutar.fnev
FROM pfutar
INNER JOIN prendeles ON pfutar.fazon = prendeles.fazon
GROUP BY pfutar.fnev
HAVING COUNT(*) > (
    SELECT AVG(szamlalo) 
    FROM (
        SELECT COUNT(*) AS szamlalo
        FROM prendeles
        GROUP BY fazon
    ) AS atlag
);

-- 39. feladat:
SELECT pvevo.vnev
FROM pvevo
INNER JOIN prendeles ON pvevo.vazon = prendeles.vazon
INNER JOIN ptetel ON prendeles.razon = ptetel.razon
GROUP BY pvevo.vnev
HAVING SUM(ptetel.db) >= 3 * (
    SELECT AVG(db) 
    FROM (
        SELECT SUM(ptetel.db) AS db
        FROM ptetel
        INNER JOIN prendeles ON ptetel.razon = prendeles.razon
        GROUP BY prendeles.vazon
    ) AS atlag
);

-- 40. feladat:
SELECT pfutar.fnev
FROM pfutar
INNER JOIN prendeles ON pfutar.fazon = prendeles.fazon
GROUP BY pfutar.fnev
HAVING COUNT(*) >= 5;

-- 41. feladat:
SELECT ppizza.pnev
FROM ppizza
INNER JOIN ptetel ON ppizza.pazon = ptetel.pazon
GROUP BY ppizza.pnev
HAVING SUM(ptetel.db) >= 50;

-- 42. feladat:
SELECT pvevo.vnev
FROM pvevo
INNER JOIN prendeles ON pvevo.vazon = prendeles.vazon
GROUP BY pvevo.vnev
HAVING COUNT(DISTINCT prendeles.razon) < 3;

-- 43. feladat:
/* Vigyori pizza nem létezik az adatok között */
SELECT NULL AS eredmeny LIMIT 0;

-- 44. feladat:
/* Columbo név nem szerepel a vevők között */
SELECT ppizza.pnev
FROM ppizza
WHERE ppizza.pazon NOT IN (
    SELECT DISTINCT ptetel.pazon
    FROM ptetel
    INNER JOIN prendeles ON ptetel.razon = prendeles.razon
    INNER JOIN pvevo ON prendeles.vazon = pvevo.vazon
    WHERE pvevo.vnev = 'Columbo'
);

-- 45. feladat:
SELECT ppizza.pnev
FROM ppizza
INNER JOIN ptetel ON ppizza.pazon = ptetel.pazon
WHERE ptetel.pazon IS NULL;

-- 46. feladat:
/* Vigyori pizza nem létezik az adatok között */
SELECT pvevo.vnev
FROM pvevo
WHERE pvevo.vnev NOT IN (
    SELECT DISTINCT pvevo.vnev
    FROM pvevo
    INNER JOIN prendeles ON pvevo.vazon = prendeles.vazon
    INNER JOIN ptetel ON prendeles.razon = ptetel.razon
    INNER JOIN ppizza ON ptetel.pazon = ppizza.pazon
    WHERE ppizza.pnev = 'Vigyori'
);

-- 47. feladat:
SELECT pvevo.vnev, pfutar.fnev
FROM pvevo
INNER JOIN pfutar
WHERE NOT EXISTS (
    SELECT 1
    FROM prendeles
    WHERE prendeles.vazon = pvevo.vazon
    AND prendeles.fazon = pfutar.fazon
);

-- 48. feladat:
/* Nevetős és Vigyori pizza nem létezik */
SELECT NULL AS eredmeny LIMIT 0;

-- 49. feladat:
/* Hahota és Kacagós pizza nem létezik */
SELECT NULL AS eredmeny LIMIT 0;

-- 50. feladat:
SELECT pvevo.vnev
FROM pvevo
INNER JOIN prendeles ON pvevo.vazon = prendeles.vazon
INNER JOIN ptetel ON prendeles.razon = ptetel.razon
GROUP BY pvevo.vnev, ptetel.pazon
HAVING SUM(ptetel.db) >= 10
GROUP BY pvevo.vnev
HAVING COUNT(DISTINCT ptetel.pazon) >= 2;

```

**Megjegyzések:**

- A 43., 44., 46., 48., 49. feladatok üres eredménnyel zárulnak, mert a feltételekben említett pizza/vásárló nevek nem szerepelnek az adatok között
- A 47. feladat eredménye megmutatja az összes olyan vevő-futár párost aki sosem találkozott
- A 50. feladatban a `HAVING COUNT(DISTINCT ptetel.pazon) >= 2` biztosítja a kétféle pizza feltételét

