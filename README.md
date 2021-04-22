# Test for Analytics

Design tests for Analytics functionality on a Battery Monitoring System.

Fill the parts marked '_enter' in the **Tasks** section below.

## Analysis-functionality to be tested

This section lists the Analysis for which _tests_ must be written.

Battery Telemetrics are collected and stored on a server.
Data for a month is stored in a [csv file](https://en.wikipedia.org/wiki/Comma-separated_values).

Analysis must be done on this csv file to find the following:
- minimum
- maximum
- count of breaches (how many times did it cross the threshold in a month?)
- record trends (date & time when the reading was continuously increasing for 30 minutes)

A PDF report of the analysis must be stored every week.
Notification must be sent when a new report is available.

## Tasks

### List Dependencies

List the dependencies of the Analysis-functionality.

1. Access to the Server containing the telemetrics in a csv file
2. Read and write access to csv files in the server.
3. PDF report generator(when this report needs to be generate)
4. Mail server Notification details
5. Maximum storage capacity of the server for storing the PDF reports

(add more if needed)

### Mark the System Boundary

What is included in the software unit-test? What is not? Fill this table.

| Item                      | Included?     | Reasoning / Assumption
|---------------------------|---------------|---
Battery Data-accuracy       | No            | We do not test the accuracy of data
Computation of maximum      | Yes           | This is part of the software being developed
Off-the-shelf PDF converter | Yes           | This is part of the software being developed
Counting the breaches       | Yes           | Counting the breaches is used to verify if crossed the threshold in a month.
Detecting trends            | Yes           | This is part of the software being developed
Notification utility        | Yes           | To check whether the notifications are reached as expected .

### List the Test Cases

Write tests in the form of `<expected output or action>` from `<input>` / when `<event>`

Add to these tests:

1. Write minimum and maximum to the PDF from a csv containing positive and negative readings
2. Write "Invalid input" to the PDF when the csv doesn't contain expected data
3. Write "Access denied" to the PDF when the there is no access to the server containing the file
4. Write "Breach counts" to the PDF when the input cross the threshold.
5. Write "File Not Found" to the PDF when the csv file is not available in the server.
6. Write "Date and time" to the pdf,when the reading was continuously increasing for 30 minutes.
7. Verify whether Notification is sent, when a new report is available.
8. Print "Notification details not found" when the email and mobile number details are not found
9. Print "Notify Success /Failed" when email/messages are sent
10.Verify memory,when the storage memory of the server reaches 90%


### Recognize Fakes and Reality

Consider the tests for each functionality below.
In those tests, identify inputs and outputs.
Enter one part that's real and another part that's faked/mocked.

| Functionality            | Input        | Output                      | Faked/mocked part
|--------------------------|--------------|-----------------------------|---
Read input from server     | csv file     | internal data-structure     | Fake the server store
Validate input             | csv data     | valid / invalid             | None - it's a pure function
Notify report availability | Notification message/Recipient info      | message sent/failed         | Mock the Notification function
Report inaccessible server | Fake server address |Error message         | Fake the server address
Find minimum and maximum   | csv file     | Minimum & Maximum value     | None - it's a pure function
Detect trend               | csv file     | Timestamp details           | None - it's a pure function
Write to PDF               | Internal data| PDF File                    | Mock - PDF file generation
