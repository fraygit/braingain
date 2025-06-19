# Overview 
Create a web application for teacher to manage their students and their progress. This application will let the teacher create an adaptive learning plan for their students. The application will also let the teacher track the progress of their students. The application will also let the teacher create an adaptive assessment for their students. The application will also let the teacher create an adaptive test for their students. The learning plan will be based on New Zealand curriculum and the refreshed New Zealand curriculum. The application will use Claude AI API to create the adaptive learning plan, adaptive assessment and adaptive test.

# Technology Stack
1. Visual Studio project
    1. a visual studio solution contains 3 projects:
    2. the solution should be named "braingain". Use the same name as base namespace.
    3. a class library project, name the project "braingain.core"
    4. an asp.net c# core web api project, name the project "braingain.api"
    5. an angular project version 19, name the project "braingain.dashboard"

# Projects
## braingain.core

This will be the core library for the application. It will contain all the business logic and data access logic. This will be used by the api project and the dashboard project.

1. the class library project will be C# .net core 8.0
2. add the latest entity framework core
3. create an abstract base class "baseEntity" with virtual properties
    1. id (primary key) - integer identity
    2. createdAt (default value is current date and time)
    3. updatedAt (default value is current date and time)
4. add the following entity models in a folder named "Models". Each model should be in a separate class file. inherit all entities from the "baseEntity" class.
    1. "user" with properties
        1. firstName
        2. lastName
        3. gender (enum: male, female, other)
        4. dateOfBirth
        5. email
        6. password
    2. "organisation" with properties
        1. name
        2. description
    3. "userOrganisation" to link a many to many relationship between user and organisation with properties
        1. userId
        2. organisationId
    4. "student" with properties
        1. firstName
        2. lastName
        3. dateOfBirth
        4. gender (enum: male, female, other)
        5. email
        6. password
    5. "studentOrganisation" to link a many to many relationship between student and organisation with properties
        1. studentId
        2. organisationId
    6. "teacherOrganisation" to link a many to many relationship between user and organisation with properties
        1. userId
        2. organisationId
    7. "LearningPath" with properties
        1. name
        2. description
        3. organisationId
        4. year (enum: 1, 2, 3, 4, 5, 6, 7, 8, 9, 10, 11, 12)
        5. term (enum: 1, 2, 3, 4)
        6. learningAreas (enum: english, arts, math and statistics, science, social 
        studies, technology, health and physical education)
        7. schoolYear 
    8. "LearningPathStudent" to link a many to many relationship between LearningPath and student with properties
        1. learningPathId
        2. studentId
    9. "LearningPathTeacher" to link a many to many relationship between LearningPath and teacher with properties
        1. learningPathId
        2. teacherId
    11. "Assessment" with properties
        1. name
        2. description
        3. learningPathId
        4. assessmentType (enum: formative, summative)
        5. assessmentMethod (enum: paper, online)
        6. assessmentDate
        7. assessmentDuration
        8. assessmentWeight
        9. assessmentStatus (enum: draft, published)
    12. "Question" with properties
        1. questionText
        2. questionType (enum: single choice, multiple choice, true false)
        3. questionWeight
    13. "Answer" with properties
        1. answerText
        2. isCorrect
    14. "OnlineQuiz" with properties
        1. assessmentId
        2. Title
        3. Description
        4. Status (enum: draft, published)
        5. sortOrder
    15. "OnlineQuizQuestionAnswer" with properties
        1. onlineQuizId
        2. questionId
        3. answerId
    16. "StudentOnlineQuiz" with properties
        1. onlineQuizId
        2. studentId
        3. totalScore
        4. feedback
        5. dateTaken
        6. duration
        7. status (enum: started, completed)
    17. "StudentOnlineQuizQuestionAnswer" with properties
        1. studentOnlineQuizId
        2. onlineQuizQuestionAnswerId
        3. answerId
        4. isCorrect
        5. dateAnswered        
5. implement a repository pattern for each entity.
6. create a folder named "Interfaces". In this folder create an interface for each entity repository. exclude the "baseEntity" interface. exclude the "userOrganisation" interface. exclude the "studentOrganisation" interface. exclude the "teacherOrganisation" interface.
7. implement a unit of work pattern for the repository.
8. create a folder named "Services". In this folder implement a service pattern for each entity. exclude the "baseEntity" interface. exclude the "userOrganisation" interface. exclude the "studentOrganisation" interface. exclude the "teacherOrganisation" interface.
9. in each service, add the functions for the repository to create, read, update and delete. include the create, read, update and delete functions for the relationships.
10. implement a unit of work pattern for the service.
11. do not create a migration for the database.
12. do not create a seed data for the database.
13. create a folder "sql" in the root directory. In this folder create a sql file named "braingain.sql". This file will contain the database schema.
14. create a service called "NZCurriculumService" and "INZCurriculumService". This service will be used to get the NZ curriculum data from the API.
    1. use Claude AI API, add the api key to the appsettings.json file.
    2. implement the following methods:
        1. GenerateAdaptiveTest
            1. the method will take the following parameters:
                1. LearningPathId
                2. StudentId
                3. TeacherId
                4. OrganisationId
                5. number of questions
            2. call the claude sdk to generate the adaptive test.
                1. generate a system prompt message to say that you are a teacher in new zealand and an expert in adaptive learning.
                2. generate a user prompt message to say that you want to generate an adaptive test for a student. include the student year, term, learning areas, and the learning path.
                3. if the student has a past assessment, include the past assessment in the user prompt message.
                4. give an example of a return json object with the following properties:
                    1. questions
                    2. answers
            3. return the adaptive test as a json object. 

# braingain.api

this is a c# .net 8 REST API project.

1. add the latest swagger
2. add the latest logging
3. add cors policy for *.*
4. add reference to the braingain.core project
5. inject the unit of work pattern for the service
6. create a folder named "Controllers". In this folder implement a controller pattern for each entity. exclude the "baseEntity" interface. exclude the "userOrganisation" interface. exclude the "studentOrganisation" interface. exclude the "teacherOrganisation" interface.
7. implement a unit of work pattern for the controller.
8. create a controller for authentication. This controller will have functions for login and register. Use the User entity for authentication. return a JWT token.

# braingain.dashboard
1. the dashboard project will be angular. use angular 20.
2. add the latest angular router
3. add the latest angular http client
4. create a service to call the braingain.api rest API
5. use the free tailwind template tailadmin from https://github.com/TailAdmin/tailadmin-free-tailwind-dashboard-template   
6. create a login page.
    1. use the template https://github.com/TailAdmin/tailadmin-free-tailwind-dashboard-template/blob/main/src/signin.html as the login page. 
    2. use the braingain.api rest API to authenticate the user. 
    3. implement a canActivate guard to check if the user is authenticated. if not, redirect to login page.
7. create a dashboard page.
    1. use the template https://github.com/TailAdmin/tailadmin-free-tailwind-dashboard-template/blob/main/src/index.html as the dashboard page. 
    2. implement a canActivate guard to check if the user is authenticated. if not, redirect to login page.
    3. Add the following navigation items to the dashboard page:
        1. Dashboard
        2. Organisations
            1. List of Organisations
            2. Add Organisation
            3. Edit Organisation
            4. Delete Organisation
            5. View Organisation
            6. use the braingain.api rest API create, read, update and delete the organisations.
            7. add a teacher to the organisation.
            8. add a student to the organisation.
        3. Students
            1. List of Students
            2. Add Student
            3. Edit Student
            4. Delete Student
            5. View Student
            6. use the braingain.api rest API create, read, update and delete the students.
        4. Teachers
            1. List of Teachers
            2. Add Teacher
            3. Edit Teacher
            4. Delete Teacher
            5. View Teacher
            6. use the braingain.api rest API create, read, update and delete the teachers.
        5. Learning Paths
            1. List of Learning Paths
            2. Add Learning Path
            3. Edit Learning Path
            4. Delete Learning Path
            5. View Learning Path
            6. use the braingain.api rest API create, read, update and delete the learning paths.
            7. add learning path to the organisation.
            8. add a student to the learning path.
            9. add a teacher to the learning path.

    