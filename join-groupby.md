GROUP BY queries:

1.
    SELECT COUNT(*) AS `numero_iscritti`, YEAR(`enrolment_date`) AS `anno_di_iscrizione`
    FROM `students`
    GROUP BY YEAR(`enrolment_date`);

2.
    SELECT COUNT(*) AS `numero_insegnanti`, `office_address`
    FROM `teachers`
    GROUP BY `office_address`;

3.
    SELECT AVG(`vote`) AS `media_voto`, `exam_id`
    FROM `exam_student`
    GROUP BY `exam_id`;

4.
    SELECT `department_id`, COUNT(*) AS `numero_cdl`
    FROM `degrees`
    GROUP BY `department_id`;

JOIN queries:

1.
    SELECT `degrees`.`name` AS `degree_name`, `students`.*
    FROM `degrees`
    INNER JOIN `students`
    ON `degrees`.`id` = `students`.`degree_id`
    WHERE `degrees`.`name` = 'Corso di Laurea in Economia';

2.
    SELECT *
    FROM `departments`
    INNER JOIN `degrees`
    ON `departments`.`id` = `degrees`.`department_id`
    WHERE `departments`.`name` = 'Dipartimento di Neuroscienze'
    AND `degrees`.`level` = 'magistrale';

3. 
    SELECT CONCAT(`teachers`.`name`, ' ', `teachers`.`surname`) AS `teacher`, `courses`.*
    FROM `teachers`
    JOIN `course_teacher`
    ON `teachers`.`id` = `course_teacher`.`teacher_id`
    JOIN `courses`
    ON `course_teacher`.`course_id` = `courses`.`id`
    WHERE `teachers`.`id` = 44;

4.
    SELECT `students`.`surname` AS `student_surname`, `students`.`name` AS `student_name`, `degrees`.*, `departments`.*
    FROM `departments`
    JOIN `degrees`
    ON `departments`.`id` = `degrees`.`department_id`
    JOIN `students`
    ON `degrees`.`id` = `students`.`degree_id`
    ORDER BY `students`.`surname`, `students`.`name`;

5.
    SELECT `degrees`.`name` AS `degree_name`, `courses`.*, `teachers`.*
    FROM `degrees`
    JOIN `courses`
    ON `degrees`.`id` = `courses`.`degree_id`
    JOIN `course_teacher`
    ON `courses`.`id` = `course_teacher`.`course_id`
    JOIN `teachers`
    ON `course_teacher`.`teacher_id` = `teachers`.`id`
    ORDER BY `courses`.`degree_id`;

6.
    SELECT DISTINCT `teachers`.`surname` AS `teacher_surname`, `teachers`.`name` AS `teacher_name`,`departments`.`name`
    FROM `departments`
    JOIN `degrees`
    ON `departments`.`id` = `degrees`.`department_id`
    JOIN `courses`
    ON `degrees`.`id` = `courses`.`degree_id`
    JOIN `course_teacher`
    ON `courses`.`id` = `course_teacher`.`course_id`
    JOIN `teachers`
    ON `course_teacher`.`teacher_id` = `teachers`.`id`
    WHERE `departments`.`name` = 'Dipartimento di Matematica'
    ORDER BY `teachers`.`surname`;

7.
    SELECT `students`.`surname`, `students`.`name`, `exams`.`course_id`, COUNT(*) AS `numero_tentativi`
    FROM `students`
    JOIN `exam_student`
    ON `students`.`id` = `exam_student`.`student_id`
    JOIN `exams`
    ON `exam_student`.`exam_id` = `exams`.`id`
    GROUP BY `students`.`name`, `students`.`surname`, `exams`.`course_id`  
    ORDER BY `students`.`surname` ASC, `students`.`name` ASC;