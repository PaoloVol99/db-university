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