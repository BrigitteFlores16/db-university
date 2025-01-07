1. Contare quanti iscritti ci sono stati ogni anno

```sql
SELECT year(enrolment_date) as year, count(*) as iscritti_tot_per_anno
FROM university.students
GROUP BY year(enrolment_date)
ORDER BY year(enrolment_date);

```

2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio

```sql
SELECT office_address, count(*) as insegnanti_nel_edificio
FROM university.teachers
GROUP BY office_address
ORDER BY office_address;

```

3. Calcolare la media dei voti di ogni appello d'esame

```sql
SELECT `exam_id`, AVG(`vote`) as media
FROM university.exam_student
GROUP BY `exam_id`;

```

4. Contare quanti corsi di laurea ci sono per ogni dipartimento

```sql
SELECT `department_id`, count(*) as degree_count
FROM university.degrees
GROUP BY `department_id`;

```
