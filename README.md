# mysql_sys.schema_index_statistics-

SELECT 
    `performance_schema`.`table_io_waits_summary_by_index_usage`.`OBJECT_SCHEMA` AS `table_schema`,
    `performance_schema`.`table_io_waits_summary_by_index_usage`.`OBJECT_NAME` AS `table_name`,
    `performance_schema`.`table_io_waits_summary_by_index_usage`.`INDEX_NAME` AS `index_name`,
    `performance_schema`.`table_io_waits_summary_by_index_usage`.`COUNT_FETCH` AS `rows_selected`,
    FORMAT_PICO_TIME(`performance_schema`.`table_io_waits_summary_by_index_usage`.`SUM_TIMER_FETCH`) AS `select_latency`,
    `performance_schema`.`table_io_waits_summary_by_index_usage`.`COUNT_INSERT` AS `rows_inserted`,
    FORMAT_PICO_TIME(`performance_schema`.`table_io_waits_summary_by_index_usage`.`SUM_TIMER_INSERT`) AS `insert_latency`,
    `performance_schema`.`table_io_waits_summary_by_index_usage`.`COUNT_UPDATE` AS `rows_updated`,
    FORMAT_PICO_TIME(`performance_schema`.`table_io_waits_summary_by_index_usage`.`SUM_TIMER_UPDATE`) AS `update_latency`,
    `performance_schema`.`table_io_waits_summary_by_index_usage`.`COUNT_DELETE` AS `rows_deleted`,
    FORMAT_PICO_TIME(`performance_schema`.`table_io_waits_summary_by_index_usage`.`SUM_TIMER_DELETE`) AS `delete_latency`
FROM
    `performance_schema`.`table_io_waits_summary_by_index_usage`
WHERE
    (`performance_schema`.`table_io_waits_summary_by_index_usage`.`INDEX_NAME` IS NOT NULL)
ORDER BY `performance_schema`.`table_io_waits_summary_by_index_usage`.`SUM_TIMER_WAIT` DESC
