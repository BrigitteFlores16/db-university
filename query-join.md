1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia

```sql
SELECT
     `degrees`.`id` AS `id_corso`,
     `degrees`.`name` AS `nome_corso`,
     `students`.`name` AS `nome_studente`
FROM `degrees`
INNER JOIN `students`
ON `degrees`.`id`= `students`.`degree_id`
WHERE `degrees`.`id`=53;

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
SELECT
     `degrees`.`name` AS `nome_corso_di_laurea`,
     `courses`.`name` AS `nome_corso`,
     `teachers`.`name` AS `nome_insegnante`,
     `teachers`.`surname` AS `cognome_insegnante`
FROM `teachers`
INNER JOIN `course_teacher`
ON `teachers`.`id` = `course_teacher`.`teacher_id`
INNER JOIN `courses`
ON `course_teacher`.`course_id` = `courses`.`id`
INNER JOIN `degrees`
ON `degrees`.`id` = `courses`.`degree_id`;

```

6. Selezionare tutti i docenti che insegnano nel Dipartimento di
   Matematica (54)

```sql
SELECT
     `teachers`.`name` AS `nome_insegnanti`,
     `teachers`.`surname` AS `cognome_insegnanti`,
     `departments`.`name` AS `nome_dipartimento`
FROM `teachers`
INNER JOIN `course_teacher`
ON `teachers`.`id` = `course_teacher`.`teacher_id`
INNER JOIN `courses`
ON `courses`.`id` = `course_teacher`.`course_id`
INNER JOIN `degrees`
ON `courses`.`degree_id` = `degrees`.`id`
INNER JOIN `departments`
ON `degrees`.`department_id` = `departments`.`id`
WHERE `departments`.`id` = 5;

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
