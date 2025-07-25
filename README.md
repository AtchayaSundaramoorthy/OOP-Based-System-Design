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

## 💡 OOP Concepts Used

| Concept        | Applied In                                                   |
|----------------|---------------------------------------------------------------|
| Abstraction     | Classes hide internal logic and represent real-world roles. |
| Encapsulation   | Private properties and controlled access via getters/setters |
| Inheritance     | Student & Instructor extend User                             |
| Polymorphism    | `getRole()` method overridden in subclasses                  |

---

## 🔍 Sample Usage

```javascript
const alice = new Instructor(1, "Alice", "alice@mail.com");
const courseJS = alice.createCourse(101, "JavaScript Basics");

const bob = new Student(2, "Bob", "bob@mail.com");
bob.enroll(courseJS);

const hw1 = new Assignment(1, "JS Homework 1", courseJS);
courseJS.addAssignment(hw1);

bob.uploadAssignment(hw1, "bob_hw1.pdf");
alice.gradeAssignment(hw1, bob, 90);
