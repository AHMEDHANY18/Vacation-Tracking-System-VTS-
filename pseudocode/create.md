# Vacation Management System - Pseudocode

## Overview
This document describes the pseudocode for the employee vacation time management system.

---

## Main Function: ManageTime()

### Preconditions
- Employee is already authenticated by the portal
- Employee has permission to manage their vacation time

### Process Flow

```
FUNCTION ManageTime():

    // Display current vacation status
    DISPLAY "Vacation Status and Available Balance" TO employee

    // Employee selects vacation type
    Employee selects vacationType

    // Check if balance is available
    IF vacationType.balance <= 0 THEN
        SHOW "You have no available balance for this vacation type"
        RETURN
    END IF

    // Request vacation details
    PROMPT "Enter vacation dates and hours per day"
    Employee enters requestedDates, requestedHours, title, description

    // Validate input data
    CALL ValidateData(requestedDates, requestedHours, title, description)
    IF validationResult == "Invalid" THEN
        SHOW "Please fix highlighted errors"
        RETURN
    END IF

    // Check if requested hours exceed available balance
    totalRequestedHours = SUM(requestedHours)
    IF totalRequestedHours > vacationType.balance THEN
        SHOW "Requested time exceeds available balance"
        RETURN
    END IF

    // Save vacation request
    SAVE vacationRequest WITH status = "Pending Approval"
    SHOW "Your request has been submitted successfully"

    // Notify manager
    SEND email TO Manager WITH subject = "New Vacation Request Pending Approval"

    // Wait for manager decision
    WAIT for Manager decision

    // Handle approval/rejection
    IF Manager approves THEN
        UPDATE vacationRequest.status = "Approved"
        SEND email TO Employee: "Your vacation request has been approved"
    ELSE
        UPDATE vacationRequest.status = "Rejected"
        REQUIRE Manager to provide rejectionReason
        SEND email TO Employee: "Your vacation request has been rejected. Reason: rejectionReason"
    END IF

    RETURN

END FUNCTION
```

---

## Helper Function: ValidateData()

### Purpose
Validates user input for vacation request

### Parameters
- `dates`: Array of requested vacation dates
- `hours`: Array of requested hours per day
- `title`: Title of the vacation request
- `description`: Description of the vacation request

### Validation Rules

```
FUNCTION ValidateData(dates, hours, title, description):

    // Validate dates
    IF dates ARE empty OR invalid THEN
        RETURN "Invalid"
    END IF

    // Validate hours
    IF hours ARE empty OR <= 0 THEN
        RETURN "Invalid"
    END IF

    // Validate title
    IF title IS empty OR length(title) > 100 THEN
        RETURN "Invalid"
    END IF

    // Validate description
    IF length(description) > 500 THEN
        RETURN "Invalid"
    END IF

    // All validations passed
    RETURN "Valid"

END FUNCTION
```

---

## Data Structures

### VacationRequest
- `requestId`: Unique identifier
- `employeeId`: Employee identifier
- `vacationType`: Type of vacation (annual, sick, etc.)
- `requestedDates`: Array of dates
- `requestedHours`: Hours requested per day
- `totalHours`: Total hours calculated
- `title`: Request title (max 100 characters)
- `description`: Request description (max 500 characters)
- `status`: Current status (Pending/Approved/Rejected)
- `rejectionReason`: Reason for rejection (if applicable)
- `createdDate`: Request creation timestamp
- `updatedDate`: Last update timestamp

### VacationType
- `typeId`: Vacation type identifier
- `typeName`: Name of vacation type
- `balance`: Available hours/days
- `maxPerRequest`: Maximum allowed per request

---

## System States

1. **Initial**: Display vacation balance
2. **Input**: Employee enters vacation details
3. **Validation**: System validates input
4. **Pending**: Awaiting manager approval
5. **Approved**: Request approved by manager
6. **Rejected**: Request rejected by manager

---

## Notifications

### To Manager
- Email notification when new vacation request is submitted
- Subject: "New Vacation Request Pending Approval"

### To Employee
- Success message upon submission
- Email notification for approval: "Your vacation request has been approved"
- Email notification for rejection: "Your vacation request has been rejected. Reason: {rejectionReason}"

---

## Error Handling

- **No Balance**: Show message and exit
- **Invalid Input**: Highlight errors and request correction
- **Insufficient Balance**: Show message and exit
- **Required Rejection Reason**: Manager must provide reason when rejecting