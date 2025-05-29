# SQL_interview_Ascendeum


with WeeklyHours as (
  
    SELECT
        resource_id,
        strftime('%W', start_time) AS WeekNumber, 
        SUM(
            (julianday(end_time) - julianday(start_time)) * 24
        ) AS WeeklyWorkingHours -- Convert days to hours
    FROM
        tabl
    WHERE
        start_time IS NOT NULL AND end_time IS NOT NULL AND end_time > start_time
    GROUP BY
        resource_id,
        WeekNumber
)

SELECT
    resource_id,
    round(AVG(WeeklyWorkingHours),2) AS AverageWeeklyWorkingHours
FROM WeeklyHours
GROUP BY
    resource_id;
