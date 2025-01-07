1. Selezionare tutti gli studenti nati nel 1990 (160)

```sql

SELECT *
FROM university.students
WHERE YEAR (`date_of_birth`) = 1990;

```

2. Selezionare tutti i corsi che valgono più di 10 crediti (479)

```sql
SELECT *
FROM university.courses
WHERE `cfu`> 10 ;

```

3. Selezionare tutti gli studenti che hanno più di 30 anni

```sql
SELECT *
FROM university.students
WHERE date_of_birth < DATE_SUB(CURDATE(), INTERVAL 30 YEAR);
```

4. Selezionare tutti i corsi del primo semestre del primo anno di un qualsiasi corso di
   laurea (286)

```sql
SELECT *
FROM university.courses
WHERE `period` ='I semestre' AND  `year` = 1;

```

5. Selezionare tutti gli appelli d'esame che avvengono nel pomeriggio (dopo le 14) del
   20/06/2020 (21)

```sql
SELECT *
FROM university.exams
WHERE `hour` > '14:00' AND `date` = '2020-06-20';
```

6. Selezionare tutti i corsi di laurea magistrale (38)

```sql
SELECT *
FROM university.degrees
WHERE  `level` = 'magistrale';

```

7. Da quanti dipartimenti è composta l'università? (12)

```sql
SELECT count(*)
FROM university.departments;
```

8. Quanti sono gli insegnanti che non hanno un numero di telefono? (50)

```sql
SELECT count(*)
 FROM university.teachers
 WHERE phone is null ;

```

9. Inserire nella tabella degli studenti un nuovo record con i propri dati (per il campo
   degree_id, inserire un valore casuale)

```sql

INSERT INTO university.students (name, surname, date_of_birth, degree_id, fiscal_code, registration_number, enrolment_date, email)
VALUES ('Brigitte', 'Florez', '1999-01-01', FLOOR(rand() * 1000) + 1, 'AAA', '123','1999-01-01','ciao@hotmail.com');

```

10. Cambiare il numero dell’ufficio del professor Pietro Rizzo in 126

```sql
UPDATE university.teachers
SET `office_number` = '126'
WHERE `id` = 58;
```

11. Eliminare dalla tabella studenti il record creato precedentemente al punto 9

```sql
DELETE FROM university.students
WHERE `id` = 5001;

```
