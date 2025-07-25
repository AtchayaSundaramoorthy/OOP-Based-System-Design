# OOP-Based-System-Design

## Objective

Design and simulate a course management system using core **Object-Oriented Programming (OOP)** principles in JavaScript.

---

## Features

- User Roles: `Student`, `Instructor`
- Course Creation by Instructor
- Student Enrollment
- Assignment Upload by Students
- Assignment Grading by Instructor
- Role-based functionality using polymorphism

---

## Class Structure

### User (Superclass)
- `id`, `name`, `email`
- Methods: `login()`, `logout()`, `getRole()` ← overridden

### Student
- Properties: `enrolledCourses`, `grades`
- Methods: `enroll(course)`, `uploadAssignment()`, `getRole()`

### Instructor
- Properties: `createdCourses`
- Methods: `createCourse()`, `gradeAssignment()`, `getRole()`

### Course
- Properties: `id`, `title`, `instructor`, `students[]`, `assignments[]`
- Methods: `addStudent()`, `addAssignment()`

### Assignment
- Properties: `id`, `title`, `course`, `submissions`
- Methods: `submit()`, `getSubmission()`

### Grade
- Properties: `assignment`, `student`, `score`
- Method: `getGrade()`

---

## OOP Concepts Used

| Concept        | Applied In                                                   |
|----------------|---------------------------------------------------------------|
| Abstraction     | Classes hide internal logic and represent real-world roles. |
| Encapsulation   | Private properties and controlled access via getters/setters |
| Inheritance     | Student & Instructor extend User                             |
| Polymorphism    | `getRole()` method overridden in subclasses                  |

---

## 🔍 Code

```
class User {
  constructor(id, name, email) {
    this._id = id;
    this._name = name;
    this._email = email;
  }

  login() {
    console.log(`${this._name} logged in.`);
  }

  logout() {
    console.log(`${this._name} logged out.`);
  }

  getRole() {
    return "User";
  }

  get name() {
    return this._name;
  }

  set name(newName) {
    this._name = newName;
  }
}
class Student extends User {
  constructor(id, name, email) {
    super(id, name, email);
    this.enrolledCourses = [];
    this.grades = [];
  }

  enroll(course) {
    course.addStudent(this);
    this.enrolledCourses.push(course);
  }

  uploadAssignment(assignment, file) {
    assignment.submit(this, file);
  }

  getRole() {
    return "Student";
  }
}

class Instructor extends User {
  constructor(id, name, email) {
    super(id, name, email);
    this.createdCourses = [];
  }

  createCourse(id, title) {
    const course = new Course(id, title, this);
    this.createdCourses.push(course);
    return course;
  }

  gradeAssignment(assignment, student, score) {
    const grade = new Grade(assignment, student, score);
    student.grades.push(grade);
    return grade;
  }

  getRole() {
    return "Instructor";
  }
}

class Course {
  constructor(id, title, instructor) {
    this.id = id;
    this.title = title;
    this.instructor = instructor;
    this.students = [];
    this.assignments = [];
  }

  addStudent(student) {
    this.students.push(student);
  }

  addAssignment(assignment) {
    this.assignments.push(assignment);
  }
}

class Assignment {
  constructor(id, title, course) {
    this.id = id;
    this.title = title;
    this.course = course;
    this.submissions = new Map(); 
  }

  submit(student, file) {
    this.submissions.set(student, file);
  }

  getSubmission(student) {
    return this.submissions.get(student);
  }
}

class Grade {
  constructor(assignment, student, score) {
    this.assignment = assignment;
    this.student = student;
    this.score = score;
  }

  getGrade() {
    return this.score;
  }
}
```
## UML Diagram
![Uploading online course system design.jpg…]()

## Conclusion

This project helped me understand and apply OOP concepts to build a basic course management system with real-world features like enrollment, assignment submission, and grading

