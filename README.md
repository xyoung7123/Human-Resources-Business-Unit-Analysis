# Human-Resources-Business-Unit-Analysis
Project 2: SQL Code used in Organizing, Cleaning and Preparation of Data for Visualization in the Human Resources Business Unit

--Human Resources Data Analysis
select * from  [HumanResources].[Employee];
select * from [HumanResources].[EmployeeDepartmentHistory]
select * from [HumanResources].[Department]
select * from [HumanResources].[EmployeePayHistory]

--Cleaning Table  [HumanResources].[Employee];

select BusinessEntityID, OrganizationLevel, JobTitle, BirthDate, MaritalStatus, 
Gender, HireDate, VacationHours, SickLeaveHours from  [HumanResources].[Employee]

select distinct  businessEntityID from [HumanResources].[Employee]

--IDENTIFYING THE DUPLICATE VALUES
select COUNT(businessEntityID) from [HumanResources].[Employee]
select COUNT(DISTINCT businessEntityID) from [HumanResources].[Employee]

select COUNT(OrganizationLevel) from [HumanResources].[Employee]

-- IDENTIFYING THE NULL VALUES
select COUNT(BusinessEntityID), COUNT(OrganizationLevel), COUNT(JobTitle), COUNT(BirthDate), COUNT(MaritalStatus), 
COUNT(Gender), COUNT(HireDate), COUNT(VacationHours), COUNT(SickLeaveHours) from  [HumanResources].[Employee]

select BusinessEntityID, OrganizationLevel, JobTitle, BirthDate, MaritalStatus, 
Gender, HireDate, VacationHours, SickLeaveHours from  [HumanResources].[Employee]
WHERE OrganizationLevel IS NULL

 --replacing the null value with 1
Update [HumanResources].[Employee]
SET OrganizationLevel = REPLACE(OrganizationLevel, 'NULL', '1')
where OrganizationLevel IS NOT NULL

select REPLACE(OrganizationLevel, NULL, 1) from [HumanResources].[Employee]
select coalesce(OrganizationLevel, 1) OrganizationLevel from [HumanResources].[Employee]

select BusinessEntityID, coalesce(OrganizationLevel, 1) OrganizationLevel, JobTitle, BirthDate, MaritalStatus, 
Gender, HireDate, VacationHours, SickLeaveHours from  [HumanResources].[Employee]

--Cleaning and Organizing Table [HumanResources].[EmployeeDepartmentHistory]
select * from [HumanResources].[EmployeeDepartmentHistory]
select BusinessEntityID, DepartmentID, ShiftID, 
StartDate, EndDate from [HumanResources].[EmployeeDepartmentHistory]

--CLeaning and Organizing [HumanResources].[Department]
select * from [HumanResources].[Department]
select departmentID, Name, GroupName from [HumanResources].[Department]

select count(departmentID), count(Name), count(GroupName) from [HumanResources].[Department]


--CLeaning and Organizing Table [HumanResources].[EmployeePayHistory]
select * from [HumanResources].[EmployeePayHistory]
select BusinessEntityID, Rate, PayFrequency from [HumanResources].[EmployeePayHistory]

--Joining the tables 2 and 3
select BusinessEntityID, [HumanResources].[EmployeeDepartmentHistory].DepartmentID, ShiftID, 
StartDate, EndDate, [HumanResources].[Department].DepartmentID, Name, GroupName from [HumanResources].[EmployeeDepartmentHistory]
inner join [HumanResources].[Department]
on [HumanResources].[EmployeeDepartmentHistory].DepartmentID = [HumanResources].[Department].DepartmentID


--Joining the tables 1 and 4
select [HumanResources].[Employee].BusinessEntityID, coalesce(OrganizationLevel, 1) OrganizationLevel, 
JobTitle, BirthDate, MaritalStatus, Gender, HireDate, VacationHours, SickLeaveHours, 
[HumanResources].[EmployeePayHistory].BusinessEntityID, 
Rate, PayFrequency from [HumanResources].[Employee] 
inner join [HumanResources].[EmployeePayHistory] 
ON [HumanResources].[Employee].BusinessEntityID = [HumanResources].[EmployeePayHistory].BusinessEntityID

