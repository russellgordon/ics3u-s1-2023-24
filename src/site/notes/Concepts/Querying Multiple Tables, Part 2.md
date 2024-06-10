---
{"dg-publish":true,"permalink":"/concepts/querying-multiple-tables-part-2/","dgHomeLink":true,"dgShowToc":true}
---

# Querying Multiple Tables, Part 2

When completing [[Tutorials/Creating a To-do List App, Part 6\|part six of the to-do list tutorial series]] you learned how to use the MVVM design pattern to query a single table hosted at Supabase.

In part one of this guide, you learned how to [[Concepts/Querying Multiple Tables\|query and display results from two tables joined by a  one-to-many / many-to-one relationship]].

In this second and final part of this guide, you will learn how to query, display, and update data in tables joined by a *many-to-many* relationship.

## Students and courses

How is a student related to a course? How is a course related to a student?

### ER diagram

Consider this entity-relationship diagram identifying how a student is related to a course, for the purposes of enrolment – tracking which student is taking which course:

![IMG_4313 Large.png](/img/user/Media/IMG_4313%20Large.png)

> [!NOTE]
> The diagram is deliberately simplified. In a complete database meant for this purpose, there would be additional attributes on the entities shown, and additional entities – such as, but not limited to, a `teacher` entity to keep track of what teacher(s) are teaching a given course.

Thinking of the relationship in each direction:

- student to course
	- A given student enrols in *many* courses.
- course to student
	- A given course has *many* students enrolled in it.

Looking from student to course, overall now, there is a *many-to-many* relationship.

Looking from course to student, overall now, there is a *many-to-many* relationship.

### Creating a database

Using a [[Concepts/Entity-Relationship Diagrams#Conversion to a database\|large language model such as ChatGPT]], we can obtain SQL that will create a database that matches the ER diagram above, and populate it with sample data.

Here is the prompt Mr. Gordon used to do so:

```
This is a photo of a hand-drawn conceptual entity-relationship diagram. The diagram describes the relationship between students and courses, for the purposes of enrolment.

Please convert this image into valid SQL that will create database tables with columns, primary keys, and foreign keys where appropriate based on the cardinality described in the diagram. Ensure that table and column names are lowercased.

Do your best to infer data types for table columns based on the name of attributes given for each entity.

Be certain that the SQL you generate is compatible with the PostgreSQL database software.

Once you have produced SQL that creates a database that matches this ER diagram, please create some reasonable sample data for each table.

When creating the sample data ensure all of the following criteria are met:

1. There are ten and only ten courses listed.
2. The courses must be from grade 11 level of the Ontario secondary school curriculum. For example, one course at this level has a short code of ICS3U and a name of "Introduction to Computer Science". Another course example is MCR3U, named "Functions". Another course is ENG3U, named "English".
3. The sample data is meant to describe enrolment in courses for a single half-year semester at a typical Ontario secondary school – all that this means is that a given student must be enrolled in exactly four courses for the semester.
4. All students must be enrolled in ENG3U and MCR3U.
```

ChatGPT produced an accurate representation of the ER diagram, and met the sample data requirements, but there were three issues that Mr. Gordon wanted to correct:

1. There were too many students – three will be sufficient for the purposes of this guide.
2. The LLM did not produce an explanation of the purpose of each database table beyond the comments included in the SQL it generated.
3. The way that sample data was added to the `enrols_in` table made the purpose of that table less than clear.

Mr. Gordon started with the following prompt:

```
Please expand on the purpose of each table you have created. With reference to the sample data for the students named Emily Jones and John Doe, explain how the data added to the "enrols_in" table tracks the many-to-many relationship between the "student" and "course" tables.
```

Mr. Gordon received a decent explanation, but he realized he could make a third prompt to address all three concerns noted above.

He provided a third prompt as follows:

```
That explanation is very helpful. The original SQL you produced is also an accurate representation of the entity-relationship diagram I provided.

However, I would like to make some adjustments so that the SQL you have produced is easier for beginners to understand. Here are the changes I would like you to make:

1. Please produce sample data for only three students.
2. When populating the "enrols_in" table, populate the "course_id" column by assuming the "id" value based on the insertion order of data in the "course" table.
3. Please provide an explanation of each table again, like you did before. With reference to the sample data for two of the three students, explain how the data added to the "enrols_in" table tracks the many-to-many relationship between the "student" and "course" tables.
```

This time, Mr. Gordon received a good response. The response is included below:

> Sure, I'll make the adjustments as requested. I'll provide sample data for only three students, populate the `course_id` column by assuming the `id` value based on the insertion order of data in the `course` table, and provide an explanation of each table again.

> **SQL to Create Tables**

```sql
-- Create the student table
CREATE TABLE student (
    id SERIAL PRIMARY KEY,
    first_name VARCHAR(50),
    last_name VARCHAR(50)
);

-- Create the course table
CREATE TABLE course (
    id SERIAL PRIMARY KEY,
    short_code VARCHAR(10) UNIQUE,
    name VARCHAR(100)
);

-- Create the enrols_in table to represent the many-to-many relationship
CREATE TABLE enrols_in (
    student_id INT REFERENCES student(id),
    course_id INT REFERENCES course(id),
    PRIMARY KEY (student_id, course_id)
);
```

> **SQL to Insert Sample Data**

```sql
-- Insert sample courses
INSERT INTO course (short_code, name) VALUES
('ICS3U', 'Introduction to Computer Science'), -- id = 1
('MCR3U', 'Functions'), -- id = 2
('ENG3U', 'English'), -- id = 3
('SCH3U', 'Chemistry'), -- id = 4
('SPH3U', 'Physics'), -- id = 5
('SBI3U', 'Biology'), -- id = 6
('CGG3O', 'Travel and Tourism: A Regional Geographic Perspective'), -- id = 7
('CHW3M', 'World History to the End of the Fifteenth Century'), -- id = 8
('FSF3U', 'Core French'), -- id = 9
('AVI3M', 'Visual Arts'); -- id = 10

-- Insert sample students
INSERT INTO student (first_name, last_name) VALUES
('John', 'Doe'), -- id = 1
('Jane', 'Smith'), -- id = 2
('Emily', 'Jones'); -- id = 3

-- Insert sample enrolments ensuring each student is enrolled in exactly four courses including ENG3U and MCR3U
INSERT INTO enrols_in (student_id, course_id) VALUES
-- John Doe
(1, 3), -- ENG3U
(1, 2), -- MCR3U
(1, 1), -- ICS3U
(1, 4), -- SCH3U

-- Jane Smith
(2, 3), -- ENG3U
(2, 2), -- MCR3U
(2, 5), -- SPH3U
(2, 6), -- SBI3U

-- Emily Jones
(3, 3), -- ENG3U
(3, 2), -- MCR3U
(3, 7), -- CGG3O
(3, 8); -- CHW3M
```

> **Explanation of Each Table**
> 
> 1. **student Table**
>    - **Purpose:** Stores information about students.
>    - **Columns:**
>      - `id`: A unique identifier for each student (Primary Key).
>      - `first_name`: The first name of the student.
>      - `last_name`: The last name of the student.
> 
> 2. **course Table**
>    - **Purpose:** Stores information about courses.
>    - **Columns:**
>      - `id`: A unique identifier for each course (Primary Key).
>      - `short_code`: A short code for the course (e.g., ENG3U for "English"), which is unique.
>      - `name`: The full name of the course.
> 
> 3. **enrols_in Table**
>    - **Purpose:** Tracks the enrolment of students in courses, representing the many-to-many relationship between students and courses.
>    - **Columns:**
>      - `student_id`: The ID of the student (Foreign Key referencing `student(id)`).
>      - `course_id`: The ID of the course (Foreign Key referencing `course(id)`).
> 
> **Tracking the Many-to-Many Relationship**
> 
> The `enrols_in` table is the junction table that links students to the courses they are enrolled in. Each row in the `enrols_in` table represents a unique enrolment of a student in a course. This allows a student to be enrolled in multiple courses and a course to have multiple students.
> 
> **Example: Emily Jones and John Doe**
> 
> **Emily Jones**
> - **Student ID:** 3
> - **Courses Enrolled:**
>   - `ENG3U` (English) - `course_id` = 3
>   - `MCR3U` (Functions) - `course_id` = 2
>   - `CGG3O` (Travel and Tourism: A Regional Geographic Perspective) - `course_id` = 7
>   - `CHW3M` (World History to the End of the Fifteenth Century) - `course_id` = 8
> 
> **John Doe**
> - **Student ID:** 1
> - **Courses Enrolled:**
>   - `ENG3U` (English) - `course_id` = 3
>   - `MCR3U` (Functions) - `course_id` = 2
>   - `ICS3U` (Introduction to Computer Science) - `course_id` = 1
>   - `SCH3U` (Chemistry) - `course_id` = 4
> 
> **Sample Data in the `enrols_in` Table:**
```sql
-- Enrolments for Emily Jones
INSERT INTO enrols_in (student_id, course_id) VALUES
(3, 3), -- ENG3U
(3, 2), -- MCR3U
(3, 7), -- CGG3O
(3, 8); -- CHW3M

-- Enrolments for John Doe
INSERT INTO enrols_in (student_id, course_id) VALUES
(1, 3), -- ENG3U
(1, 2), -- MCR3U
(1, 1), -- ICS3U
(1, 4); -- SCH3U
```

> **Explanation:**
> 
> 1. **Emily Jones**
>    - `student_id` = 3 (Emily Jones)
>    - `course_id` values are assigned based on the insertion order in the `course` table:
>      - `ENG3U` (English) - `course_id` = 3
>      - `MCR3U` (Functions) - `course_id` = 2
>      - `CGG3O` (Travel and Tourism: A Regional Geographic Perspective) - `course_id` = 7
>      - `CHW3M` (World History to the End of the Fifteenth Century) - `course_id` = 8
>    - Each pair (3, course_id) is inserted into the `enrols_in` table, representing Emily's enrolments.
> 
> 2. **John Doe**
>    - `student_id` = 1 (John Doe)
>    - `course_id` values are assigned based on the insertion order in the `course` table:
>      - `ENG3U` (English) - `course_id` = 3
>      - `MCR3U` (Functions) - `course_id` = 2
>      - `ICS3U` (Introduction to Computer Science) - `course_id` = 1
>      - `SCH3U` (Chemistry) - `course_id` = 4
>    - Each pair (1, course_id) is inserted into the `enrols_in` table, representing John's enrolments.
> 
> By using the `student_id` and `course_id` pairs, the `enrols_in` table effectively manages and tracks the enrolments, allowing you to query which students are enrolled in which courses and vice versa. This structure supports the many-to-many relationship between students and courses.

It's always important to model good manners (even when interacting with a non-sentient large language model that produces responses based on statistical probabilities and associations between words) so Mr. Gordon finished with this prompt:

```
Thank-you! That response is what I was looking for.
```

Here is the response received:

>  You're welcome! I'm glad it was helpful and met your needs. If you have any more questions or need further assistance with SQL or any other topic, feel free to ask!

### Reviewing the schema

Mr. Gordon next created a new project at [Supabase](https://supabase.com), then pasted the SQL into the SQL Editor and ran the query to create tables:

![Screenshot 2024-06-09 at 9.38.05 AM.png](/img/user/Media/Screenshot%202024-06-09%20at%209.38.05%E2%80%AFAM.png)

Next he ran the query to create the sample data:

![Screenshot 2024-06-09 at 9.39.07 AM.png](/img/user/Media/Screenshot%202024-06-09%20at%209.39.07%E2%80%AFAM.png)

By then navigating to the **Database** panel:

![Screenshot 2024-06-09 at 9.41.07 AM.png](/img/user/Media/Screenshot%202024-06-09%20at%209.41.07%E2%80%AFAM.png)

Then selecting **Schema Visualizer**:

![Screenshot 2024-06-09 at 9.40.16 AM.png](/img/user/Media/Screenshot%202024-06-09%20at%209.40.16%E2%80%AFAM.png)

Mr. Gordon was able to obtain a visual representation of the table structure – this is called the *schema* for a database.

> [!NOTE]
> You can drag tables around to better see the connections between them in the Schema Visualizer.

Let's compare the ER diagram to the database schema:

![Screenshot 2024-06-09 at 9.47.08 AM.png](/img/user/Media/Screenshot%202024-06-09%20at%209.47.08%E2%80%AFAM.png)

Three tables were created; attributes that are underlined are converted into *primary keys*. A primary key is a unique identifier for a row in a database. Values are typically integers that are auto-incremented for each new row that is added to the database table.

The `enrols_in` table is a *junction* table, which also referred to as a *look-up* table. The `enrols_in` table tracks the relationship between the `student` table and the `course` table. It's foreign key connections to the `student` table and the `course` table allow us to see, for a given student, what courses they are enrolled in. Looking in the other direction, for a given course, we can see what students enrolled.

### Reviewing the sample data

For example, we can look up what courses Jane Smith is enrolled in:

![Screenshot 2024-06-09 at 9.52.29 AM.png](/img/user/Media/Screenshot%202024-06-09%20at%209.52.29%E2%80%AFAM.png)

From the other direction, we can look up what students enrolled in Functions:

![Screenshot 2024-06-09 at 9.52.29 AM 1.png](/img/user/Media/Screenshot%202024-06-09%20at%209.52.29%E2%80%AFAM%201.png)

### Creating a project

To query the data in this newly created database, Mr. Gordon:

- created a new project in Xcode, ensuring source control was enabled
- created a GitHub remote
- created groups for the model, views, view models, and helper code
- created a file named `Supabase.swift` that contains the database information required to connect to his database hosted at Supabase

Like this:

![Screenshot 2024-06-09 at 10.10.40 AM.png](/img/user/Media/Screenshot%202024-06-09%20at%2010.10.40%E2%80%AFAM.png)

The database connection information was obtained from the **API** section of **Project Settings**:

![Screenshot 2024-06-09 at 10.10.56 AM.png](/img/user/Media/Screenshot%202024-06-09%20at%2010.10.56%E2%80%AFAM.png)

Next Mr. Gordon added the [[Tutorials/Creating a To-do List App, Part 6#Adding the Supabase framework\|package dependency for Supabase]]:

![Screenshot 2024-06-09 at 10.12.58 AM.png](/img/user/Media/Screenshot%202024-06-09%20at%2010.12.58%E2%80%AFAM.png)

He then made sure that all six package products were being compiled into the app:

![Screenshot 2024-06-09 at 10.13.41 AM.png](/img/user/Media/Screenshot%202024-06-09%20at%2010.13.41%E2%80%AFAM.png)

Before proceeding, Mr. Gordon committed his work.

### App interface

A three-tab interface might work for this app.

Here is Mr. Gordon's rough plan for that, with a `LandingView` added that the app opens to, and three starter views:

1. A view to show enrolments: `EnrolmentsView`.
2. A view to list courses; a sheet accessible from this view will allow new courses to be added: `CoursesListView`.
3. A view to list students; a sheet accessible from this view will allow new students to be added: `StudentsListView`.

This is what that looks like, from the app entry point:

![Screenshot 2024-06-09 at 10.29.09 AM.png](/img/user/Media/Screenshot%202024-06-09%20at%2010.29.09%E2%80%AFAM.png)

From `LandingView`:

![Screenshot 2024-06-09 at 10.29.01 AM.png](/img/user/Media/Screenshot%202024-06-09%20at%2010.29.01%E2%80%AFAM.png)

Here is a short demo:

![RocketSim_Recording_iPhone_15_Pro_6.1_2024-06-09_10.30.15.gif|350](/img/user/Media/RocketSim_Recording_iPhone_15_Pro_6.1_2024-06-09_10.30.15.gif)

Mr. Gordon then committed his work.

### Listing courses

To get started with simply listing the courses in the database, Mr. Gordon at first modified `CoursesListView` to display a few static values:

![Screenshot 2024-06-09 at 11.27.29 AM.png](/img/user/Media/Screenshot%202024-06-09%20at%2011.27.29%E2%80%AFAM.png)

After committing that work, Mr. Gordon next created a `Course` model:

![Screenshot 2024-06-09 at 11.32.30 AM.png](/img/user/Media/Screenshot%202024-06-09%20at%2011.32.30%E2%80%AFAM.png)

... to match the `course` database table:

![Screenshot 2024-06-09 at 11.29.54 AM.png](/img/user/Media/Screenshot%202024-06-09%20at%2011.29.54%E2%80%AFAM.png)

After committing that work, Mr. Gordon then created a view model, to load courses data from the database:

![Screenshot 2024-06-09 at 11.37.08 AM.png](/img/user/Media/Screenshot%202024-06-09%20at%2011.37.08%E2%80%AFAM.png)

After committing that work, Mr. Gordon then made the view use the view model, rather than simply showing static data:

![Screenshot 2024-06-09 at 11.39.36 AM.png](/img/user/Media/Screenshot%202024-06-09%20at%2011.39.36%E2%80%AFAM.png)

Mr. Gordon then committed his work.

### Creating courses

An app to track course enrolments in a school would need the ability to create a new course, when the school decides to offer something new to students.

This is relatively straightforward, since a course can exist in the `course` table on it's own, without any references to data from other tables. In other words, a new course will not have any students enrolled in it.

So, we need to:

1. Add a function to the view model to create a course.
2. Make a view that allows the user to provide details for a new course.
3. Provide access to the view that allows for addition of a new course from the courses list view.

First, Mr. Gordon modified `CoursesListViewModel`, so that it has a function that allows a new course to be created:

![Screenshot 2024-06-09 at 11.46.26 AM.png](/img/user/Media/Screenshot%202024-06-09%20at%2011.46.26%E2%80%AFAM.png)

The current contents of the `course` table at Supabase are:

![Screenshot 2024-06-09 at 11.47.53 AM.png](/img/user/Media/Screenshot%202024-06-09%20at%2011.47.53%E2%80%AFAM.png)

To test that the function to create a course is working, Mr. Gordon temporarily added this code to `CoursesListView` – it will be run once when the view appears:

![Screenshot 2024-06-09 at 11.52.17 AM.png](/img/user/Media/Screenshot%202024-06-09%20at%2011.52.17%E2%80%AFAM.png)

Mr. Gordon knew that the function worked, because the new course now appears in the user interface. As expected, this is what is now in the `courses` table at Supabase:

![Screenshot 2024-06-09 at 11.51.23 AM.png](/img/user/Media/Screenshot%202024-06-09%20at%2011.51.23%E2%80%AFAM.png)

Knowing that the new function in the view model is working, Mr. Gordon removed the temporary code from `CoursesListView`:

![Screenshot 2024-06-09 at 11.54.51 AM.png](/img/user/Media/Screenshot%202024-06-09%20at%2011.54.51%E2%80%AFAM.png)

...and then committed his work.

Next, Mr. Gordon created a view that allows the user to enter course details:

![Screenshot 2024-06-09 at 12.03.33 PM.png](/img/user/Media/Screenshot%202024-06-09%20at%2012.03.33%E2%80%AFPM.png)

The view to add a course needs access to the view model, which it receives through the environment.

> [!NOTE]
> To be able to test the appearance of the view in isolation within the Xcode Previews interface, Mr. Gordon provides the preview with an instance of the view model and shows the new view inside a sheet.

Mr. Gordon then committed his work.

Finally, Mr. Gordon added the necessary code to `CourseListView` so that it can present the sheet to add a new course:

![Screenshot 2024-06-09 at 12.17.15 PM.png](/img/user/Media/Screenshot%202024-06-09%20at%2012.17.15%E2%80%AFPM.png)

> [!IMPORTANT]
> Since `AddCourseView` pulls the view model out of the environment, `CoursesListView` must insert it into the environment. An alternative would be [[Tutorials/Creating a To-do List App, Part 6#Using @Bindable\|passing a reference to the child view as a binding]].

Here is how the app looks and works at this point:

![RocketSim_Recording_iPhone_15_Pro_6.1_2024-06-09_12.21.46.gif|350](/img/user/Media/RocketSim_Recording_iPhone_15_Pro_6.1_2024-06-09_12.21.46.gif)

Mr. Gordon then committed his work.

Mr. Gordon realized that the courses were showing up in the order they were originally inserted into the `courses` table.

It would likely be better that those courses be sorted by their short codes.

So, Mr. Gordon modified the view model, like so:

![Screenshot 2024-06-09 at 12.24.42 PM.png](/img/user/Media/Screenshot%202024-06-09%20at%2012.24.42%E2%80%AFPM.png)

Courses are now listed in alphabetical order, ascending, based on their short codes:

![RocketSim_Screenshot_iPhone_15_Pro_6.1_2024-06-09_12.25.04.png|350](/img/user/Media/RocketSim_Screenshot_iPhone_15_Pro_6.1_2024-06-09_12.25.04.png)

Mr. Gordon committed his work at this point.

### Listing and creating students

If you consider the database schema:

![Screenshot 2024-06-09 at 12.27.03 PM.png](/img/user/Media/Screenshot%202024-06-09%20at%2012.27.03%E2%80%AFPM.png)

... you can see that the `student` table is very similar to the `course` table.

A row in the `student` table can exist in its own, without a reference to any other data. This would represent, perhaps, a new student who has registered at the school, but not yet enrolled in any courses.

The point here is that the process of listing and creating students in the app is identical to the process of listing and creating courses. 

This will be true of any two entities, or two tables in a database, that relate to each other in a many-to-many relationship. 

So, to ensure this guide does not get too long, here is the series of changes Mr. Gordon made to list students:

1. [Modified `StudentsListView` so it displays a few static values.](https://github.com/lcs-rgordon/StudentsAndCourses/commit/7f3a9f88a6c8885b158d9a63491280753fb35854)
2. [Made a `Student` model to match the `student` table in the database.](https://github.com/lcs-rgordon/StudentsAndCourses/commit/ffff628bf259c1ac44b51a261d78402812dd43c2)
3. [Made a `StudentsListViewModel` to load students data from the database.](https://github.com/lcs-rgordon/StudentsAndCourses/commit/3654825e42daf76f36cd4feeedb245bf3e5114ee)
4. [Modified `StudentsListView` so that it uses the view model.](https://github.com/lcs-rgordon/StudentsAndCourses/commit/0e3c7cc680e8bcaa61021bf32fdf1d346628987c)

And here are the series of changes Mr. Gordon made to create new students:

1. [Added a function to `StudentsListViewModel` to create a student.](https://github.com/lcs-rgordon/StudentsAndCourses/commit/c0c3eb2256c72a5a927c707bfea8658ffe119211)
2. [Made a view that allows the user to provide details for a new student.](https://github.com/lcs-rgordon/StudentsAndCourses/commit/201aa49f4744c1fda0a97546aced475cf400c4a5)
3. [Provided access to the view that allows for addition of a new student from the students list view.](https://github.com/lcs-rgordon/StudentsAndCourses/commit/462d5fbf8d6c177ad62d1ac0b178e1e4707bfe63)

Here is how the app now looks and works at this point:

![RocketSim_Recording_iPhone_15_Pro_6.1_2024-06-09_13.03.22.gif|350](/img/user/Media/RocketSim_Recording_iPhone_15_Pro_6.1_2024-06-09_13.03.22.gif)

### Listing enrolments

When listing enrolments, we can approach the relationship from two sides:

![Screenshot 2024-06-09 at 12.27.03 PM.png](/img/user/Media/Screenshot%202024-06-09%20at%2012.27.03%E2%80%AFPM.png)

1. From the point of view of a student – what courses are they enrolled in?
2. From the point of view of a course – what students have enrolled in that course?

To first help us understand how this will look in the app, we can mock it out with static data.

Mr. Gordon started this process by modifying `EnrolmentsView` like so:

![Screenshot 2024-06-09 at 3.24.30 PM.png](/img/user/Media/Screenshot%202024-06-09%20at%203.24.30%E2%80%AFPM.png)

Let's say the user chooses to view enrolments by course, from that screen.

When they arrive at `EnrolmentsByCourseView` they should see all courses.

Let's stay instead that the user chooses to view enrolments by student, from that screen above.

When they arrive at `EnrolmentsByStudentView` they should see all students.

For now, Mr. Gordon mocked this out by adding static data for a few courses:

![Screenshot 2024-06-09 at 3.38.07 PM.png](/img/user/Media/Screenshot%202024-06-09%20at%203.38.07%E2%80%AFPM.png)

Then, for a few students:

![Screenshot 2024-06-09 at 3.36.48 PM.png](/img/user/Media/Screenshot%202024-06-09%20at%203.36.48%E2%80%AFPM.png)

Then he hooked those two new views up to `EnrolmentsView` so that he could navigate down to them:

![Screenshot 2024-06-09 at 3.41.10 PM.png](/img/user/Media/Screenshot%202024-06-09%20at%203.41.10%E2%80%AFPM.png)

The app now works like this beginning at `EnrolmentsView`:

![RocketSim_Recording_iPhone_15_Pro_6.1_2024-06-09_15.42.24.gif|350](/img/user/Media/RocketSim_Recording_iPhone_15_Pro_6.1_2024-06-09_15.42.24.gif)

Mr. Gordon then committed that work.

Of course, all of those enrolment views are operating with static data, so next it is time to hook the views up to the database to show live data instead.

#### By course

To view enrolments by course, first we need a model file that encapsulates the join that will occur across the `enrols_in` lookup table.

Mr. Gordon created the `CourseStudent` model file like so:

![Screenshot 2024-06-09 at 3.46.17 PM.png](/img/user/Media/Screenshot%202024-06-09%20at%203.46.17%E2%80%AFPM.png)

Next we need a view model that can fetch all courses, and by joining to the `student` table, include what students are enrolled in each course.

Mr. Gordon created the `EnrolmentsByCourseViewModel`:

![Screenshot 2024-06-09 at 3.51.52 PM.png](/img/user/Media/Screenshot%202024-06-09%20at%203.51.52%E2%80%AFPM.png)

The `select` statement on line 30 in that screenshot is equivalent to running this raw SQL directly against the database:

![Screenshot 2024-06-09 at 3.57.33 PM.png](/img/user/Media/Screenshot%202024-06-09%20at%203.57.33%E2%80%AFPM.png)

One of the really nice things about the Supabase framework is that it is able to automatically determine when two tables are joined in a many-to-many relationship based on the foreign keys that are present. As a programmer using their framework, selecting from the `course` table and joining to the `student` table, we can omit any mention of the `enrols_in` table. Supabase takes care of the tedious part of the join process for us.

When the `getCoursesWithStudents` function is invoked in the view model, Supabase returns this JSON-formatted data:

```json
[
   {
      "id":1,
      "short_code":"ICS3U",
      "name":"Introduction to Computer Science",
      "student":[
         {
            "id":1,
            "last_name":"Doe",
            "first_name":"John"
         }
      ]
   },
   {
      "id":2,
      "short_code":"MCR3U",
      "name":"Functions",
      "student":[
         {
            "id":1,
            "last_name":"Doe",
            "first_name":"John"
         },
         {
            "id":2,
            "last_name":"Smith",
            "first_name":"Jane"
         },
         {
            "id":3,
            "last_name":"Jones",
            "first_name":"Emily"
         }
      ]
   },
   {
      "id":3,
      "short_code":"ENG3U",
      "name":"English",
      "student":[
         {
            "id":1,
            "last_name":"Doe",
            "first_name":"John"
         },
         {
            "id":2,
            "last_name":"Smith",
            "first_name":"Jane"
         },
         {
            "id":3,
            "last_name":"Jones",
            "first_name":"Emily"
         }
      ]
   },
   {
      "id":4,
      "short_code":"SCH3U",
      "name":"Chemistry",
      "student":[
         {
            "id":1,
            "last_name":"Doe",
            "first_name":"John"
         }
      ]
   },
   {
      "id":5,
      "short_code":"SPH3U",
      "name":"Physics",
      "student":[
         {
            "id":2,
            "last_name":"Smith",
            "first_name":"Jane"
         }
      ]
   },
   {
      "id":6,
      "short_code":"SBI3U",
      "name":"Biology",
      "student":[
         {
            "id":2,
            "last_name":"Smith",
            "first_name":"Jane"
         }
      ]
   },
   {
      "id":7,
      "short_code":"CGG3O",
      "name":"Travel and Tourism: A Regional Geographic Perspective",
      "student":[
         {
            "id":3,
            "last_name":"Jones",
            "first_name":"Emily"
         }
      ]
   },
   {
      "id":8,
      "short_code":"CHW3M",
      "name":"World History to the End of the Fifteenth Century",
      "student":[
         {
            "id":3,
            "last_name":"Jones",
            "first_name":"Emily"
         }
      ]
   },
   {
      "id":9,
      "short_code":"FSF3U",
      "name":"Core French",
      "student":[
         
      ]
   },
   {
      "id":10,
      "short_code":"AVI3M",
      "name":"Visual Arts",
      "student":[
         
      ]
   },
   {
      "id":11,
      "short_code":"ADA3M",
      "name":"Drama",
      "student":[
         
      ]
   },
   {
      "id":23,
      "short_code":"AMU3M",
      "name":"Music",
      "student":[
         
      ]
   }
]
```

The view and view model we wrote above take care of converting this JSON-formatted data into the `coursesWithStudents` array for us:

![Screenshot 2024-06-09 at 4.09.47 PM.png](/img/user/Media/Screenshot%202024-06-09%20at%204.09.47%E2%80%AFPM.png)

Take note of this key code in the model – on line 23 – it provides a hint to the Swift compiler, telling it to decode the array of `student` data provided in the JSON response into the Swift array named `students`:

![Screenshot 2024-06-09 at 4.12.01 PM.png](/img/user/Media/Screenshot%202024-06-09%20at%204.12.01%E2%80%AFPM.png)

Finally, Mr. Gordon will hook up the view model to the `EnrolmentsByCourseView` so that it shows live data rather than the mock, static data:

![Screenshot 2024-06-09 at 4.29.33 PM.png](/img/user/Media/Screenshot%202024-06-09%20at%204.29.33%E2%80%AFPM.png)

> [!IMPORTANT]
> Note that `EnrolmentsByCourseView` does not create its own instance of  `EnrolmentsByCourseViewModel`. Instead, it asks to be provided with an instance of the view model as an argument to populate the stored property. The reason for this choice will be explained shortly.

Since `EnrolmentsByCourseView` expects to be provided with its view model by the view that creates it (the caller, or parent view) we must modify `EnrolmentsView` to do so:

![Screenshot 2024-06-09 at 4.30.28 PM.png](/img/user/Media/Screenshot%202024-06-09%20at%204.30.28%E2%80%AFPM.png)

Like this:

![Screenshot 2024-06-09 at 4.31.02 PM.png](/img/user/Media/Screenshot%202024-06-09%20at%204.31.02%E2%80%AFPM.png)

Now, we can navigate down to see the live enrolment data by course, provided by the database:

![Screen Recording 2024-06-09 at 4.32.41 PM.gif](/img/user/Media/Screen%20Recording%202024-06-09%20at%204.32.41%E2%80%AFPM.gif)

This is good progress, so Mr. Gordon committed his changes.

Although we can see all the courses, the information is not very useful at this point in time.

One way we can improve the view is to show how many students are enrolled in each course:

![Screenshot 2024-06-09 at 4.38.35 PM.png](/img/user/Media/Screenshot%202024-06-09%20at%204.38.35%E2%80%AFPM.png)

At this point Mr. Gordon noticed that the courses appear to be listed by the order that the courses were added to the database.

Instead, it will be better to list the courses alphabetically, by the course short code.

This requires a change to the view model:

![Screenshot 2024-06-09 at 4.42.03 PM.png](/img/user/Media/Screenshot%202024-06-09%20at%204.42.03%E2%80%AFPM.png)

That looks better in the view:

![Screenshot 2024-06-09 at 4.42.23 PM.png](/img/user/Media/Screenshot%202024-06-09%20at%204.42.23%E2%80%AFPM.png)

This is good for now, although more changes here will be made later.

Mr. Gordon committed his work at this point.

#### By student

If you consider the database schema:

![Screenshot 2024-06-09 at 12.27.03 PM.png](/img/user/Media/Screenshot%202024-06-09%20at%2012.27.03%E2%80%AFPM.png)

... you can see that the `student` table is very similar to the `course` table.

A row in the `student` table can exist in its own, without a reference to any other data. This would represent, perhaps, a new student who has registered at the school, but not yet enrolled in any courses.

The point here is that the process of listing all students, and showing how many courses they are enrolled in, is very similar to the process we just engaged in when showing courses and the number of students enrolled in each course.

This will be true of any two entities, or two tables in a database, that relate to each other in a many-to-many relationship. 

So, to ensure this guide does not get too long, here is the series of changes Mr. Gordon made to list students and the count of courses they are enrolled in:

1. [Add a model to represent live student enrolment data.](https://github.com/lcs-rgordon/StudentsAndCourses/commit/ad0cc49af84302b5c9d60e7fae45ddedb1c42446)
2. [Add a view model to query the student table and join to the courses table.](https://github.com/lcs-rgordon/StudentsAndCourses/commit/8945516bddfa26612854a5b3df88dc5465e22698)
3. [Made view changes so we can see live student enrolment data.](https://github.com/lcs-rgordon/StudentsAndCourses/commit/dffd8aff4031c1d136753bb253ab62745926d756)

Here is how the app now looks and works at this point:

![RocketSim_Recording_iPhone_15_Pro_6.1_2024-06-09_17.50.31.gif|350](/img/user/Media/RocketSim_Recording_iPhone_15_Pro_6.1_2024-06-09_17.50.31.gif)

#### Using selected course, limit the students shown

When we see a list of courses, and that for a given course, there are, say, three students enrolled... we want to see *who* those students are for that course:

![RocketSim_Screenshot_iPhone_15_Pro_6.1_2024-06-09_19.54.25.png|350](/img/user/Media/RocketSim_Screenshot_iPhone_15_Pro_6.1_2024-06-09_19.54.25.png)

Like this:

![RocketSim_Recording_iPhone_15_Pro_6.1_2024-06-09_19.55.46.gif|350](/img/user/Media/RocketSim_Recording_iPhone_15_Pro_6.1_2024-06-09_19.55.46.gif)

Selecting a course and seeing the students enrolled in it is equivalent to running this raw SQL query – note the `WHERE` clause:

![Screenshot 2024-06-10 at 6.14.08 AM.png](/img/user/Media/Screenshot%202024-06-10%20at%206.14.08%E2%80%AFAM.png)

To do this in the app interface, we must enable navigation from `EnrolmentsByCourseView` to `EnrolmentsByStudentView`. When we arrive at `EnrolmentsByStudentView`, we want to see just the students enrolled in the selected course, instead of all students.

First, we modify `EnrolmentsByStudentViewModel`  and add a function that limits the results returned based on a provided course:

![Screenshot 2024-06-10 at 5.52.24 AM.png](/img/user/Media/Screenshot%202024-06-10%20at%205.52.24%E2%80%AFAM.png)

In the same view model, at the top of the file, we:

1.  modify the initializer so that it:
	- optionally accepts a course (if one is not provided, course is set to `nil`)
	- saves that course in a stored property
	- checks whether a course has been provided, and then invokes the appropriate function to populate the `studentsWithCourses` array
2.  add a stored property to track the course we are filtering on (if any)
3.  add a computed property to make it easier to tell when this view model is filtering student enrolments based on a course

Here are those edits, annotated so that it's clear where each change was made:

![Screenshot 2024-06-10 at 5.53.53 AM.png](/img/user/Media/Screenshot%202024-06-10%20at%205.53.53%E2%80%AFAM.png)

To be able to select a course, and then navigate down to see only the students enrolled in that course, we need to modify `EnrolmentsByCourseView` to use a `NavigationLink`:

![Screenshot 2024-06-10 at 6.02.49 AM.png](/img/user/Media/Screenshot%202024-06-10%20at%206.02.49%E2%80%AFAM.png)

> [!IMPORTANT]
> Where previously we just showed information about a course, now that information is the label for a navigation link.
> 
> The navigation link leads to the page that shows enrolments by student – which will now be limited to those students who are enrolled in the course the user selects.

Finally, when we are showing students enrolled in a specific course (as opposed to showing all students) the way `EnrolmentsByStudentView` presents information should differ:

![Screenshot 2024-06-10 at 6.06.21 AM.png](/img/user/Media/Screenshot%202024-06-10%20at%206.06.21%E2%80%AFAM.png)

Here we have:

1. Made the course name show up when filtering by a course.
2. Made the enrolled course count only show up when *not* filtering by a course.
3. Made the course short code show as the navigation title when filtering by a course.

Here is how these changes look in the app:

![RocketSim_Recording_iPhone_15_Pro_6.1_2024-06-10_06.07.48.gif|350](/img/user/Media/RocketSim_Recording_iPhone_15_Pro_6.1_2024-06-10_06.07.48.gif)

These are a lot of important changes, so [Mr. Gordon committed his work at this point](https://github.com/lcs-rgordon/StudentsAndCourses/commit/31fc36720960c7fe05731710114c2e530ba5d1d8).

#### Using selected student, limit the courses shown

Likewise, when we see a list of students, and that a given student has enrolled in four courses... we want to see *which* courses those are:

![RocketSim_Screenshot_iPhone_15_Pro_6.1_2024-06-09_20.42.53.png|350](/img/user/Media/RocketSim_Screenshot_iPhone_15_Pro_6.1_2024-06-09_20.42.53.png)

Like this:

![RocketSim_Recording_iPhone_15_Pro_6.1_2024-06-09_20.40.56.gif|350](/img/user/Media/RocketSim_Recording_iPhone_15_Pro_6.1_2024-06-09_20.40.56.gif)

Selecting a student and seeing the courses they are enrolled in is equivalent to running this raw SQL query – note the `WHERE` clause:

![Screenshot 2024-06-10 at 6.17.22 AM.png](/img/user/Media/Screenshot%202024-06-10%20at%206.17.22%E2%80%AFAM.png)

To do this in the app interface, we must enable navigation from `EnrolmentsByStudentView` to `EnrolmentsByCourseView`. When we arrive at `EnrolmentsByCourseView`, we want to see just the courses the selected student enrolled in, instead of all courses.

First, we modify the `EnrolmentsByCourseViewModel` to add a function that limits the results returned based on a provided student:

![Screenshot 2024-06-10 at 6.21.27 AM.png](/img/user/Media/Screenshot%202024-06-10%20at%206.21.27%E2%80%AFAM.png)

In the same view model, at the top of the file, we:

1. modify the initializer so that it:
	- optionally accepts a student (if one is not provided, student is set to `nil`)
	- saves that student in a stored property
	- checks whether a student has been provided, and then invokes the appropriate function to populate the `coursesWithStudents` array
2. add a stored property to track the student we are filtering on (if any)
3. add a computed property to make it easier to tell when this view model is filtering the courses shown to be those a given student is enrolled in

Here are those edits, annotated so that it's clear where each change was made:

![Screenshot 2024-06-10 at 6.23.23 AM.png](/img/user/Media/Screenshot%202024-06-10%20at%206.23.23%E2%80%AFAM.png)

To be able to select a student, and then navigate down to see only the courses that student is enrolled in, we need to modify `EnrolmentsByStudentView` to use a `NavigationLink`:

![Screenshot 2024-06-10 at 6.28.45 AM.png](/img/user/Media/Screenshot%202024-06-10%20at%206.28.45%E2%80%AFAM.png)

> [!IMPORTANT]
> Where previously we just showed information about a student, now that information is the label for a navigation link.
> 
> The navigation link leads to the page that shows enrolments by course – only those courses that the student is enrolled in will be shown.


Finally, when we are showing courses that a particular student is enrolled in (as opposed to showing all courses) the way `EnrolmentsByCourseView` presents information should differ:

![Screenshot 2024-06-10 at 6.32.18 AM.png](/img/user/Media/Screenshot%202024-06-10%20at%206.32.18%E2%80%AFAM.png)

Here we:

1. Only show the enrolled student count when *not* filtering by a student.
2. Made the navigation title show the student name when we *are* filtering by a student.

When those edits have been made, the result is as follows:

![RocketSim_Recording_iPhone_15_Pro_6.1_2024-06-10_06.33.14.gif](/img/user/Media/RocketSim_Recording_iPhone_15_Pro_6.1_2024-06-10_06.33.14.gif)

These are a lot of important changes, so [Mr. Gordon committed his work at this point](https://github.com/lcs-rgordon/StudentsAndCourses/commit/383ea6344530a1d21dcf0eb2a1ebc0e828c2819c).

#### So that's why it's called a NavigationStack!

Consider the database schema one more time:

![Screenshot 2024-06-09 at 12.27.03 PM.png](/img/user/Media/Screenshot%202024-06-09%20at%2012.27.03%E2%80%AFPM.png)

After making the edits in the last two sections, we have allowed our user to explore enrolments – the data stored in the `enrols_in` lookup table – from both directions.

For example, we can look up what courses Jane Smith is enrolled in:

![Screenshot 2024-06-09 at 9.52.29 AM.png](/img/user/Media/Screenshot%202024-06-09%20at%209.52.29%E2%80%AFAM.png)

This is how that now looks, through our app's user interface:

![RocketSim_Recording_iPhone_15_Pro_6.1_2024-06-09_20.49.10.gif|350](/img/user/Media/RocketSim_Recording_iPhone_15_Pro_6.1_2024-06-09_20.49.10.gif)

From the other direction, we can look up what students enrolled in Functions:

![Screenshot 2024-06-09 at 9.52.29 AM 1.png](/img/user/Media/Screenshot%202024-06-09%20at%209.52.29%E2%80%AFAM%201.png)

This is how that now looks, through our app's user interface:

![RocketSim_Recording_iPhone_15_Pro_6.1_2024-06-09_20.51.03.gif|350](/img/user/Media/RocketSim_Recording_iPhone_15_Pro_6.1_2024-06-09_20.51.03.gif)

What's really fun, though? Regardless of how the user begins exploring enrolments (either by student, or by course) they can now go as deep as they want, exploring that data. Check it out:

![RocketSim_Recording_iPhone_15_Pro_6.1_2024-06-09_21.06.31.gif|350](/img/user/Media/RocketSim_Recording_iPhone_15_Pro_6.1_2024-06-09_21.06.31.gif)

When the user wants to get back to their entry point, they can long-press on the **Back** button, and navigate all the way up to the top of the stack – or anywhere in between. That functionality is a little more useful when there are many courses and many students – but it's very cool. We are moving through the many-to-many relationship repeatedly – *as many times as we want*. That's some awesome abstraction! 🚀


### Creating new enrolments

There is a final bit of functionality needed to complete this app.

When looking at the enrolments a student has, we might want to add a course.

When looking at enrolments for a course, we might want to add a student.

#### Add a course for a student

We want to add a course that a student will take, when viewing their current enrolments, like this:

<< ADD ANIMATION >>

This is equivalent to adding a row to the `enrols_in` table using raw SQL, like this:

![Screenshot 2024-06-10 at 6.40.41 AM.png](/img/user/Media/Screenshot%202024-06-10%20at%206.40.41%E2%80%AFAM.png)

To do this, first we need a model file to represent a new row in the `enrols_in` table:

![Screenshot 2024-06-10 at 6.49.14 AM.png](/img/user/Media/Screenshot%202024-06-10%20at%206.49.14%E2%80%AFAM.png)

Next we need a new view model – the first job of this view model is to find what courses are available to the student:

![Screenshot 2024-06-10 at 10.02.26 AM.png](/img/user/Media/Screenshot%202024-06-10%20at%2010.02.26%E2%80%AFAM.png)

Here, we need to step back and discuss what is happening in the `getCourses` function shown. This code is running a database function named `get_available_courses`. This function was defined by Mr. Gordon on the database. What does it do, though? And why do we need to use a function?

First, let's explore this using raw SQL queries.

Given a student ID, we can find what courses they are already enrolled in by running a query like this:

![Screenshot 2024-06-10 at 10.05.09 AM.png](/img/user/Media/Screenshot%202024-06-10%20at%2010.05.09%E2%80%AFAM.png)

That result shows the courses that the student John Doe is enrolled in, which we can confirm here by inspection of the raw data in the tables:

![Screenshot 2024-06-10 at 10.13.26 AM (2).png](/img/user/Media/Screenshot%202024-06-10%20at%2010.13.26%E2%80%AFAM%20(2).png)

If we use that query as a sub-query, we can find all the courses that a given student has not already signed up for, like this:

![Screenshot 2024-06-10 at 10.18.10 AM.png](/img/user/Media/Screenshot%202024-06-10%20at%2010.18.10%E2%80%AFAM.png)

Here, we can see that the courses available to John Doe are all the courses whose ID is not 1, 2, 3, or 4.

**The issue is this** – at present time, there does not seem to be an easy way to run a query that contains a sub-query through the Supabase framework directly from our SwiftUI app.

So instead, we define a function, like this:

```sql
CREATE OR REPLACE FUNCTION get_available_courses(
  for_student_id int
) 
RETURNS TABLE (
  id int,
  short_code varchar,
  name varchar
)
LANGUAGE plpgsql
AS 
$$

BEGIN
  RETURN QUERY
  -- Courses available to a student
  SELECT course.id as "id", course.short_code as "short_code", course.name as "name"
  FROM course
  WHERE course.id NOT IN (
    -- Courses a given student is already enrolled in
    SELECT
      enrols_in.course_id as "enrolment_course_id"
    FROM enrols_in
    WHERE enrols_in.student_id = for_student_id       -- Only select courses this student is in
  )
  ORDER BY name;

END;
$$;
```

That syntax is *ugly*, but, it does what we need. It accepts a parameter named `for_student_id`. It returns the list of courses a student has not already enrolled in. You are welcome to adapt this function as needed for your own purposes in your own project.

To create the function on our database, we just run it in the SQL Editor:

![Screenshot 2024-06-10 at 10.26.07 AM.png](/img/user/Media/Screenshot%202024-06-10%20at%2010.26.07%E2%80%AFAM.png)

We can try out this function directly on our database through the SQL Editor:

![Screenshot 2024-06-10 at 10.23.03 AM.png](/img/user/Media/Screenshot%202024-06-10%20at%2010.23.03%E2%80%AFAM.png)

That is the function we are invoking in the view model:

![Screenshot 2024-06-10 at 10.24.07 AM.png](/img/user/Media/Screenshot%202024-06-10%20at%2010.24.07%E2%80%AFAM.png)

The idea is that the view model will only supply courses the student has not already enrolled in, so they do not pick a duplicate.

If we temporarily place this code on `LandingView`:

![Screenshot 2024-06-10 at 10.29.25 AM.png](/img/user/Media/Screenshot%202024-06-10%20at%2010.29.25%E2%80%AFAM.png)

We can run the app in the Simulator, and see the debug output from that `dump` statement:

![Screenshot 2024-06-10 at 10.30.07 AM.png](/img/user/Media/Screenshot%202024-06-10%20at%2010.30.07%E2%80%AFAM.png)

... and we can see they are the same courses we get when running the raw SQL query against the database:

![Screenshot 2024-06-10 at 10.18.10 AM.png](/img/user/Media/Screenshot%202024-06-10%20at%2010.18.10%E2%80%AFAM.png)

This is less elegant that Mr. Gordon would like, but it will have to do.

Mr. Gordon next removed the temporary code from `LandingView`, then, he created this view to allow a new course enrolment to be created for a student:

![Screenshot 2024-06-10 at 10.44.30 AM.png](/img/user/Media/Screenshot%202024-06-10%20at%2010.44.30%E2%80%AFAM.png)

The view receives a reference to it's view model. This allows the picker to be populated with the list of courses available to the student.

Before continuing, Mr. Gordon [chose to commit his work](https://github.com/lcs-rgordon/StudentsAndCourses/commit/4f907504ebbe3f304a815033b8ad62d8aebcaac0). Although the job of saving a new course enrolment for a student is not finished, what we have so far works. It's worth stopping to commit before continuing.

Now, in the screenshot above, note that on line 45, Mr. Gordon has defined a "to-do" – a bit of code that needs to be filled in. We need to add the enrolment for a given student.

To start on this, Mr. Gordon modified the view model to hold on to a reference to the student we are working with:

![Screenshot 2024-06-10 at 10.51.09 AM.png](/img/user/Media/Screenshot%202024-06-10%20at%2010.51.09%E2%80%AFAM.png)

Now, we will add a function to the view model that saves the enrolment in the selected course:

![Screenshot 2024-06-10 at 12.01.12 PM.png](/img/user/Media/Screenshot%202024-06-10%20at%2012.01.12%E2%80%AFPM.png)

Then we can come back to the view and invoke this function when the user presses the **Enrol** button:

![Screenshot 2024-06-10 at 12.02.29 PM.png](/img/user/Media/Screenshot%202024-06-10%20at%2012.02.29%E2%80%AFPM.png)

#### Add a student to a course

We want to add a student, when viewing the list of students enrolled in a course:

<< ADD ANIMATION >>

To do this, we need to...

<< FILL THIS IN >>

### Summary

Overall, the app now looks and functions like this:

<< ADD SUMMARY ANIMATION SHOWING ALL FUNCTIONALITY >>

We can see all courses that exist at the school, and add new courses.

We can see all students that exist at the school, and add new students.

We can see enrolments, starting with courses and seeing students enrolled in a selected course. If desired, we can enrol students in that course.

We can see enrolments, starting with students and seeing courses that a selected student is enrolled in. If desired, we can add a course that the selected student will be enrolled in.

### Source code

If you wish to review the source used in these examples, commit-by-commit, [you can do so here](ADD NEW LINK).

If you click the link at right for any given commit:

<< ADD SCREENSHOT >>

... you can then see the changes that were made in that commit:

<< ADD SCREENSHOT >>

Lines shown in green were added; lines shown in red were removed.