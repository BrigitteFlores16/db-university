1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

```sql
SELECT `s`.*
FROM  `students` AS `s`
INNER JOIN `degrees` AS `d`
ON `s`.`degree_id`= `d`.`id`
WHERE `d`.`name`="corso di laurea in economia ";


```

2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di
   Neuroscienze

```sql
SELECT
     `departments`.`name` AS `nome_dipartimento`,
     `degrees`.`name` AS `nome_corso`,
     `degrees`.`level` AS `tipo_corso`
FROM `departments`
INNER JOIN `degrees`
ON `degrees`.`department_id` = `departments`.`id` AND `degrees`.`level` = 'magistrale'
WHERE `departments`.`id`=7;
```

3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)

```sql
SELECT
     `course_teacher`.`teacher_id` AS `id_insegnante`,
     `courses`.`name` AS `nome_corso`

FROM `course_teacher`
INNER JOIN `courses`
ON courses.id = `course_teacher`.`course_id`
WHERE `course_teacher`.`teacher_id`=44;

```

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui
   sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e
   nome

```sql
SELECT
     `students`.`name` AS `nome_studente`,
     `students`.`surname` AS `cognome_studente`,
     `degrees`.`name` AS `nome_corso`,
     `departments`.`name` AS `nome_dipartimento`
FROM `students`
INNER JOIN `degrees`
ON `students`.`degree_id` = `degrees`.`id`
INNER JOIN `departments`
ON `degrees`.`department_id` = `departments`.`id`
ORDER BY `students`.`surname`, `students`.`name`;

```

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti

```sql
SELECT.*
      `d`.*
      `c`.*
      `t`.*
FROM `degrees` AS `d`
INNER JOIN `course`AS `c`
ON `c`.`degree_id` = `d`.`id`
INNER JOIN `courses_teacher`AS `ct`
ON `ct`.`course_id` = `c`.`id`
INNER JOIN `teachers`AS`t`
ON `ct`.`teachers_id` = `t`.`id`;
```

6. Selezionare tutti i docenti che insegnano nel Dipartimento di
   Matematica (54)

```sql
SELECT
      `dep`.*
      `t`.*
FROM `degrees` AS `deg`
INNER JOIN `courses` AS `c`
ON `c`.`degree_id` = `deg`.`id`
INNER JOIN `courses_teacher` AS `ct`
ON `ct`.`course_id` = `c`.`id`
INNER JOIN `teachers` AS `t`
ON `ct`.`teachers_id` = `t`.`id`
INNER JOIN `departments` AS `dep`
ON `deg`.`department_id` = `dep`.`id`
WHERE `dep`.`name` = "Dipartimento di Matematica";
```

7. BONUS: Selezionare per ogni studente il numero di tentativi sostenuti
   per ogni esame, stampando anche il voto massimo. Successivamente,
   filtrare i tentativi con voto minimo 18.

```sql
SELECT
    `students`.`name` AS `nome_studente`,
    `students`.`surname` AS `cognome_studente`,
    `exam_student`.`exam_id` AS `id_esame`,
    MAX(`exam_student`.`vote`) AS `voto_massimo`,
    COUNT(`exam_student`.`vote`) AS `numero_tentativi`
FROM `students`
INNER JOIN `exam_student`
ON `exam_student`.`student_id` = `students`.`id`
WHERE `exam_student`.`vote` > 17
GROUP BY `students`.`name`, `students`.`surname`, `exam_student`.`exam_id`;

```
