# PROG5121-POE

 ChatApp - Part 1 and Part 2: Registration, Authentication and QuickChat Messaging

ChatApp - Part 1 and Part 2: Registration, Login and QuickChat Feature Overview and Core Features The ChatApp application is a console-based Java program built using Object-Oriented Programming (OOP) principles and Test-Driven Development (TDD) in NetBeans.

Part 1 provides a complete User Registration and Authentication system with strict input validation.
Part 2 introduces the QuickChat Messaging System, allowing authenticated users to define session message quotas, draft text messages, validate recipient phone numbers, enforce character length limits, generate unique tracking hashes, and choose sending actions.

Core System Validation Rules and Messages 
Part 1: Registration and Authentication Rules

Username Validation Rule: Must contain an underscore and be no more than 5 characters long. Success Message: Username successfully captured. Failure Message: Username is not correctly formatted; please ensure that your username contains an underscore and is no more than five characters in length.

Password Complexity Validation Rule: Must be at least 8 characters long, contain an uppercase letter, a number, and a special character. Success Message: Password successfully captured. Failure Message: Password is not correctly formatted; please ensure that the password contains at least eight characters, a capital letter, a number, and a special character.

Cell Phone Number Validation Rule: Must match the South African international format of +27 followed by 9 digits. Success Message: Cell number successfully captured. Failure Message: Cell number is incorrectly formatted or does not contain an international code; please correct the number and try again.

User Login Authentication Rule: Compares entered credentials against stored registration details. Success Message: Welcome first name, last name it is great to see you again. Failure Message: Username or password incorrect, please try again.


Part 2: QuickChat Messaging Rules

Access Control Rule: Users can only access messaging after logging in successfully. Displays the welcome message "Welcome to QuickChat." 

Recipient Cell Number Validation Rule: Must match the international format (+27 followed by 9 digits). Success Message: Cell phone number successfully captured. Failure Message: Cell phone number is incorrectly formatted or does not contain an international code. Please correct the number and try again.

Message Body Length Rule: Must not exceed 250 characters. Success Message: Message ready to send. Failure Message: Message exceeds 250 characters by X; please reduce the size.

Action Menu Options (SentMessage):
Option 1 (Send Message): Message successfully sent.
Option 2 (Disregard Message): Press 0 to delete the message.
Option 3 (Store Message): Message successfully stored.


Class Architecture and Method Breakdown

Class 1: Login.java (Authentication Business Logic) Stores user credentials in private instance variables: registeredFirstName, registeredLastName, registeredUsername, registeredPassword, registeredCellNumber. 
- checkUserName: Returns true if the username contains an underscore and length is 5 or less.
 - checkPasswordComplexity: Returns true if the password meets all length, uppercase, number, and special character rules.
 - checkCellPhoneNumber: Returns true if the cell number matches the international format regex.
   - registerUser: Evaluates all input checks step by step and returns the corresponding registration text.
     - loginUser: Compares provided credentials to stored registration details and returns true on match.
       - returnLoginStatus: Returns custom welcome message on success or failure notice.
      
Class 2: Message.java (Messaging Business Logic) Stores message fields: messageID, messageNumber, recipientCell, messageText, messageHash, totalSentMessages.
         - checkMessageID: Verifies that the randomly generated Message ID is a 10-digit number. 
         -checkRecipientCell: Validates recipient phone number format and returns status text.
         - checkMessageLength: Validates message length (&lt;= 250 chars) and calculates overflow characters.
         - createMessageHash: Generates the uppercase hash signature combining ID digits, index, and border words.
         - SentMessage: Processes user selection (Send, Disregard, Store) and returns action confirmation text.
         - printMessages: Formats and returns full message record details.
         - returnTotalMessages: Returns the total count of messages sent during the session.

Class 3: Main.java (Console Interface) Controls console input and output using Java Scanner. Prompts the user for Registration, Login credentials, Session Message Quota, and presents the QuickChat numeric menu (1\. Send Messages, 2\. Show recently sent messages ["Coming Soon."], 3\. Quit). Handles message drafting loops and session total outputs.

Class 4: LoginTest.java (JUnit 4 Unit Test Suite - Part 1) Provides automated test coverage for all registration validation checks and authentication return statuses.

Class 5: MessageTest.java (JUnit 4 Unit Test Suite - Part 2) Provides automated test coverage for message ID length, recipient phone formatting, message character boundaries, hash creation, sending actions, and total message counters.


Unit Test Cases and Expected Outcomes

Part 1 Test Cases (LoginTest.java):

Username Correctly Formatted: Input: kyl\_1 | Assertion: assertTrue | Expected Output: true
Username Incorrectly Formatted: Input: kyle!!!!!!! | Assertion: assertFalse | Expected Output: false

Password Complexity Passed: Input: Ch&amp;&amp;sec@ke99! | Assertion: assertTrue | Expected Output: true 
Password Complexity Failed: Input: password | Assertion: assertFalse | Expected Output: false

Cell Phone Number Valid: Input: +27838968976 | Assertion: assertTrue | Expected Output: true 
Cell Phone Number Invalid: Input: 08966553 | Assertion: assertFalse | Expected Output: false

Login Successful: Input: kyl\_1, Ch&amp;&amp;sec@ke99! | Assertion: assertTrue | Expected Output: true 
Login Failed: Input: kyl\_1, wrongpassword | Assertion: assertFalse | Expected Output: false

Return Login Status Success: Input: true | Assertion: assertEquals | Expected Output: Welcome Kyle, Loves it is great to see you again. 
Return Login Status Failure: Input: false | Assertion: assertEquals | Expected Output: Username or password incorrect, please try again.

Part 2 Test Cases (MessageTest.java): 

Message ID Length: Input: Auto-generated ID | Assertion: assertEquals | Expected Output: 10

Recipient Number Valid: Input: +27718693002 | Assertion: assertEquals | Expected Output: Cell phone number successfully captured. 
Recipient Number Invalid: Input: 08575975889 | Assertion: assertEquals | Expected Output: Cell phone number is incorrectly formatted or does not contain an international code. Please correct the number and try again.

Message Length Valid: Input: Hi Mike, can you join us for dinner tonight? | Assertion: assertEquals | Expected Output: Message ready to send. 
Message Length Exceeded: Input: 260 character string | Assertion: assertEquals | Expected Output: Message exceeds 250 characters by 10; please reduce the size.

Message Hash Format: Input: ID + Index 0 + Dinner text | Assertion: assertTrue | Expected Output: Ends with :0:HITONIGHT

Sent Message Option 1: Input: Choice 1 | Assertion: assertEquals | Expected Output: Message successfully sent. 
Sent Message Option 2: Input: Choice 2 | Assertion: assertEquals | Expected Output: Press 0 to delete the message. 
Sent Message Option 3: Input: Choice 3 | Assertion: assertEquals | Expected Output: Message successfully stored.






