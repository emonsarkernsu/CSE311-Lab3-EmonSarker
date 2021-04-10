
Activity 01
------------------------------------------------------
SELECT emps.Last_Name, emps.Hire_Date
FROM emps
WHERE emps.Hire_Date LIKE "%1994%";


Activity 02
------------------------------------------------------
SELECT emps.Last_Name, emps.Salary, emps.Commission_pct
FROM emps
ORDER BY emps.Salary DESC, emps.Commission_pct DESC;


Activiy 03
------------------------------------------------------
SELECT emps.Last_Name
FROM emps
WHERE emps.Last_Name LIKE "%a%"
UNION
SELECT emps.Last_Name
FROM emps
WHERE emps.Last_Name LIKE "%e%";


Activity 04
------------------------------------------------------
SELECT emps.Last_Name, depts.Department_id, depts.Department_Name
FROM emps, depts
WHERE emps.Department_Id = depts.Department_id;


Activity 05
------------------------------------------------------
SELECT emps.Last_Name, depts.Department_Name, depts.Location_id, locs.City
FROM emps
LEFT JOIN depts
ON emps.Department_Id=depts.Department_id
LEFT JOIN locs
ON depts.Location_id=locs.Location_id
WHERE emps.Commission_pct IS NOT NULL;


Activity 06
------------------------------------------------------
SELECT DISTINCT emps.Last_Name, emps.Job_Id, depts.Department_id, depts.Department_Name
FROM locs, emps
LEFT JOIN depts
ON emps.Department_Id = depts.Department_id
WHERE depts.Department_id IN ( SELECT Department_Id 
    			       FROM depts, locs 
    			       WHERE locs.City = "Toronto" 
				AND locs.Location_id=depts.Location_id);


Activity 07
------------------------------------------------------
SELECT emps.Last_Name, emps.Salary,emps.Commission_pct 
FROM emps 
LEFT JOIN depts 
ON emps.Department_Id = depts.Department_id 
LEFT JOIN locs 
ON depts.Location_id=locs.Location_id 
WHERE emps.Commission_pct IS NOT NULL 
ORDER BY emps.Commission_pct DESC;


Activity 08
------------------------------------------------------
SELECT e.Last_Name "Employee", e.Employee_Id "EMP#", m.Last_Name "Manager", m.Employee_Id "Mgr#" 
FROM emps e
LEFT JOIN emps m 
ON e.Manager_id = m.Employee_Id;


Activity 09
------------------------------------------------------
SELECT ROUND(MIN(Salary)) AS "Minimum", ROUND(SUM(Salary)) AS "Sum", ROUND(MAX(Salary)) AS "Maximum", ROUND(AVG(Salary)) AS "Average"
FROM emps;

Activity 10
------------------------------------------------------
SELECT Job_Id, MIN(salary), MAX(salary), SUM(salary), AVG(salary)
FROM emps 
GROUP BY job_id;

Activity 11
------------------------------------------------------
SELECT Job_Id,COUNT(*) 
FROM emps 
GROUP BY Job_Id;


Activity 12
------------------------------------------------------
SELECT Manager_id, MIN(Salary) 
FROM emps 
WHERE emps.Manager_id IS NOT NULL 
GROUP BY Manager_id HAVING MIN(Salary)>6000 
ORDER BY MIN(Salary) DESC;

HOMEWORK
-------------------------------------------------------
SELECT depts.Department_Name AS "Name", COUNT(*) "Number of People",CONCAT(locs.Street_Address,", ",locs.Postal_Code,", ",locs.City,locs.State_Province,", ",locs.Country_ID) AS "Location", AVG(Salary) AS "Salary" 
FROM emps 
JOIN depts 
ON(emps.Department_Id=depts.Department_id) 
JOIN locs 
ON(locs.Location_id=depts.Location_id) 
WHERE emps.Department_id IS NOT NULL 
GROUP BY emps.Department_Id;
