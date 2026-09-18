# PROG5121-POE
ChatApp - Part 1: Registration and Login Feature

1. Overview and Core Features Part 1 of the ChatApp application is a console-based User Registration and Authentication system built in Java. It is developed using Object-Oriented Programming (OOP) principles and Test-Driven Development (TDD) in NetBeans. It allows users to register an account with specific validation rules and log into the system.
   

2. Core System Validation Rules and Messages

Username Validation Rule: Must contain an underscore and be no more than 5 characters long. Success Message: Username successfully captured. Failure Message: Username is not correctly formatted; please ensure that your username contains an underscore and is no more than five characters in length.

Password Complexity Validation Rule: Must be at least 8 characters long, contain an uppercase letter, a number, and a special character. Success Message: Password successfully captured. Failure Message: Password is not correctly formatted; please ensure that the password contains at least eight characters, a capital letter, a number, and a special character.

Cell Phone Number Validation Rule: Must match the South African international format of +27 followed by 9 digits. Success Message: Cell phone number successfully added. Failure Message: Cell number is incorrectly formatted or does not contain international code; please correct the number and try again.

User Login Authentication Rule: Compares entered credentials against stored registration details. Success Message: Welcome first name, last name it is great to see you again. Failure Message: Username or password incorrect, please try again.


3. Class Architecture and Method Breakdown

Class 1: Login.java (Business Logic) Stores user credentials in private variables: registeredFirstName, registeredLastName, registeredUsername, registeredPassword, registeredCellNumber.

* checkUserName: Returns true if the username contains an underscore and length is 5 or less.
* checkPasswordComplexity: Returns true if the password meets all length, uppercase, number, and special character rules.
* checkCellPhoneNumber: Returns true if the cell number matches the international format regex.
* registerUser: Evaluates all input checks step by step and returns the corresponding registration text.
* loginUser: Compares provided credentials to stored registration details and returns true on match.

Class 2: Main.java (Console Interface) Controls console input and output using Java Scanner. Prompts the user for First Name, Last Name, Username, Password, and Cell Phone Number. Displays registration validation output messages to the user. Prompts for login credentials if registration succeeds and displays the login status.

Class 3: LoginTest.java (JUnit 4 Unit Test Suite) Provides automated test coverage for all validation and authentication logic. Uses test user data (username: kyl\_1, password: Ch&amp;&amp;sec@ke99!, cell number: +27838968976).


4. Unit Test Cases and Expected Outcomes

Username Correctly Formatted: Input: kyl\_1 Assertion: assertTrue Expected Output: true

Username Incorrectly Formatted: Input: kyle!!!!!!! Assertion: assertFalse Expected Output: false

Password Complexity Passed: Input: Ch&amp;&amp;sec@ke99! Assertion: assertTrue Expected Output: true

Password Complexity Failed: Input: password Assertion: assertFalse Expected Output: false

Cell Phone Number Valid: Input: +27838968976 Assertion: assertTrue Expected Output: true

Cell Phone Number Invalid: Input: 08966553 Assertion: assertFalse Expected Output: false

Login Successful: Input: kyl\_1, Ch&amp;&amp;sec@ke99! Assertion: assertTrue Expected Output: true
