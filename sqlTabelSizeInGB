/* SQL code
		Extract the number of rows and size (in GB) of the existing tables in a given SQL server  
		and order them by size.
*/

SELECT	s.Name AS SchemaName,
     		t.Name AS Tablename,
				SUM(p.ROWS) AS RowCounts,
        ((SUM(a.data_pages) * 8)/ 1024)/1000.0 AS DataSpaceGB
FROM sys.tables AS T
	INNER JOIN
		sys.schemas AS s 
			ON t.SCHEMA_ID = s.SCHEMA_ID
	INNER JOIN
		sys.indexes AS i 
			ON t.OBJECT_ID = i.OBJECT_ID
	INNER JOIN
		sys.partitions AS p 
			ON i.OBJECT_ID = p.OBJECT_ID
				AND
				 i.INDEX_ID = p.INDEX_ID
	INNER JOIN
		sys.allocation_units AS a
			ON p.PARTITION_ID = a.CONTAINER_ID
	WHERE t.NAME NOT LIKE 'dt%'
GROUP BY  s.NAME, 
					t.NAME
ORDER BY 	DataSpaceGB DESC;	
