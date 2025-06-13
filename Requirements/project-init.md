Visual Studio project
1. a visual studio solution contains 3 projects:
    1. a class library project, name the project "braingain-core"
    2. an angular project version 19, name the project "braingain-dashboard"
    3. an asp.net c# core web api project, name the project "braingain-api"
2. the solution should be named "braingain"

# braingain-core
1. the class library project will be C# .net core 8.0
2. add the latest entity framework core
4. add the following entity models in a folder named "Models". Each model should be in a separate class file.
    1. "user" with properties
        1. firstName
        2. lastName
        3. email
        4. password
    2. "organisation" with properties
        1. name
        2. description
    3. "userOrganisation" to link a many to many relationship between user and organisation with properties
        1. userId
        2. organisationId
    4. "student" with properties
        1. firstName
        2. lastName
        3. email
        4. password
    5. "studentOrganisation" to link a many to many relationship between student and organisation with properties
        1. studentId
        2. organisationId
    6. "teacherOrganisation" to link a many to many relationship between user and organisation with properties
        1. userId
        2. organisationId
6. create an abstract base class "baseEntity" with virtual properties
    1. id (primary key) - integer identity
    2. createdAt (default value is current date and time)
    3. updatedAt (default value is current date and time)
5. inherit the all entities from the "baseEntity" class
6. implement a repository pattern for each entity.
7. create a folder named "Interfaces". In this folder create an interface for each entity repository. exclude the "baseEntity" interface. exclude the "userOrganisation" interface. exclude the "studentOrganisation" interface. exclude the "teacherOrganisation" interface.
8. implement a unit of work pattern for the repository.
9. create a folder named "Services". In this folder implement a service pattern for each entity. exclude the "baseEntity" interface. exclude the "userOrganisation" interface. exclude the "studentOrganisation" interface. exclude the "teacherOrganisation" interface.
10. implement a unit of work pattern for the service.
11. do not create a migration for the database.
12. do not create a seed data for the database.
13. create a folder "sql" in the root directory. In this folder create a sql file named "braingain.sql". This file will contain the database schema.

# braingain-api
1. the api project will be C# .net core 8.0
2. add the latest swagger
3. add the latest logging
4. add the latest monitoring
5. add cors policy for *.*
6. add  
