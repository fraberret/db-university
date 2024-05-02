## Group by
1. Contare quanti iscritti ci sono stati ogni anno (2018-912 | 2019-1709 | 2020-1645 | 2021-734)
```SELECT YEAR(`enrolment_date`) AS `anno`, COUNT(*) AS `numero_iscritti` FROM `students` GROUP BY YEAR(`enrolment_date`) ORDER BY `anno`;```

2. Contare gli insegnanti che hanno l'ufficio nello stesso edificio
```SELECT `office_address`, COUNT(*) AS `numero_insegnanti` FROM `teachers` GROUP BY `office_address` ORDER BY `office_address`;```

3. Calcolare la media dei voti di ogni appello d'esame
```SELECT `exams`.`id` AS `id_appelli_esame`, `exams`.`date`, AVG(`exam_student`.`vote`) AS `vote_average` FROM `exams` JOIN `exam_student` ON `exams`.`id` = `exam_student`.`exam_id` GROUP BY `exams`.`id`;```


4. Contare quanti corsi di laurea ci sono per ogni dipartimento
```SELECT `departments`.`name`, COUNT(`degrees`.`id`) AS `numero_corsi_laurea` FROM `departments` JOIN `degrees` ON `departments`.`id` = `degrees`.`department_id` GROUP BY `departments`.`id`;```



## Joins
1. Selezionare tutti gli studenti iscritti al Corso di Laurea in Economia
```SELECT `students`.`*`, `degrees`.`name` FROM `degrees` JOIN `students` ON `degrees`.`id` = `students`.`degree_id` WHERE `degrees`.`name`="Corso di Laurea in Economia";```

2. Selezionare tutti i Corsi di Laurea Magistrale del Dipartimento di       Neuroscienze
```SELECT `degrees`.`name`, `departments`.`name`, `degrees`.`level` FROM `departments` JOIN `degrees` on `departments`.`id` = `degrees`.`department_id` WHERE `departments`.`name` = "Dipartimento di Neuroscienze" AND `degrees`.`level`="magistrale";```


3. Selezionare tutti i corsi in cui insegna Fulvio Amato (id=44)
```SELECT `course_teacher`.`course_id`, `degrees`.`name`, `teachers`.`name`, `teachers`.`surname` FROM `teachers` JOIN `course_teacher` ON `teachers`.`id` = `course_teacher`.`teacher_id` JOIN `courses` ON `courses`.`id` = `course_teacher`.`course_id` JOIN `degrees` ON `degrees`.`id` = `courses`.`degree_id` WHERE `teachers`.`id` = 44;```

4. Selezionare tutti gli studenti con i dati relativi al corso di laurea a cui sono iscritti e il relativo dipartimento, in ordine alfabetico per cognome e nome
```SELECT `students`.`*`, `degrees`.`name`, `departments`.`name` FROM `degrees` JOIN `students` on `degrees`.`id` = `students`.`degree_id` JOIN `departments` ON `departments`.`id` = `degrees`.`department_id` ORDER BY `students`.`surname`, `students`.`name`;```

5. Selezionare tutti i corsi di laurea con i relativi corsi e insegnanti
```SELECT `courses`.`name`, `degrees`.`name`, `teachers`.`name`, `teachers`.`surname` FROM `degrees` JOIN `courses` ON `degrees`.`id` = `courses`.`degree_id` JOIN `course_teacher` on `courses`.`id` = `course_teacher`.`course_id` JOIN `teachers` ON `teachers`.`id` = `course_teacher`.`teacher_id`;```

6. Selezionare tutti i docenti che insegnano nel Dipartimento di Matematica (54)


### BONUS
 Selezionare per ogni studente il numero di tentativi sostenuti per ogni esame, stampando anche il voto massimo. Successivamente, filtrare i tentativi con voto minimo 18.