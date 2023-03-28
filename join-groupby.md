GROUP BY queries:

1.
    SELECT COUNT(*) AS `numero_iscritti`, YEAR(`enrolment_date`) AS `anno_di_iscrizione`
    FROM `students`
    GROUP BY YEAR(`enrolment_date`);

2.

    SELECT COUNT(*) AS `numero_insegnanti`, `office_address`
    FROM `teachers`
    GROUP BY `office_address`;