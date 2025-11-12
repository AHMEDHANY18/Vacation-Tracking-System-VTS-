// -------------------------------------------------------
// FUNCTION: EditPendingRequest
// PURPOSE:  Allows employee to edit, withdraw, or cancel a pending vacation request
// ACTORS:   Employee, Manager, System
// -------------------------------------------------------

FUNCTION EditPendingRequest():

    // Step 1 – Display pending requests
    DISPLAY "Vacation Summary (Last 6 Months - Next 18 Months)" TO Employee

    Employee selects a request WHERE status = "Pending Approval"

    IF selectedRequest IS NULL THEN
        SHOW "No pending request selected"
        RETURN
    END IF

    // Step 2 – Display editable form
    DISPLAY editable form WITH fields:
        (Title, Comments, Dates, Hours)

    PROMPT "Choose Action: Edit / Withdraw / Cancel"

    SWITCH (EmployeeAction)
        CASE "Edit":
            CALL HandleEdit(selectedRequest)
        CASE "Withdraw":
            CALL HandleWithdraw(selectedRequest)
        CASE "Cancel":
            SHOW "No changes made"
            RETURN
    END SWITCH
END FUNCTION

FUNCTION HandleEdit(request):

    // Step 1 – Employee modifies fields
    Employee modifies Title, Comments, Dates, Hours

    // Step 2 – Validate new data
    CALL ValidateRequestChanges(request)

    IF validationResult == "Invalid" THEN
        SHOW "Please fix highlighted errors"
        RETURN
    END IF

    // Step 3 – Check available balance
    CALL CheckAvailableBalance(request)

    IF balanceCheck == "Insufficient" THEN
        SHOW "Requested time exceeds available balance"
        RETURN
    END IF

    // Step 4 – Save changes
    UPDATE request IN Database:
        request.title = newTitle
        request.comments = newComments
        request.date = newDate
        request.hours = newHours
        request.status = "Pending Approval"

    LOG "Request [requestID] updated successfully"
    SHOW "Your request has been updated successfully"
    REFRESH Employee summary
    RETURN
END FUNCTION
FUNCTION HandleWithdraw(request):

    PROMPT "Are you sure you want to withdraw this request?" (Yes / No)

    IF Employee selects "No" THEN
        SHOW "Withdrawal canceled"
        RETURN
    END IF

    UPDATE request.status = "Withdrawn"
    LOG "Request [requestID] withdrawn by employee"

    SEND email TO Manager:
        SUBJECT: "Vacation Request Withdrawn"
        BODY: "Employee has withdrawn a pending vacation request."

    SHOW "Request withdrawn successfully"
    REFRESH Employee summary
    RETURN
END FUNCTION
FUNCTION CheckAvailableBalance(request):

    FETCH currentBalance FROM Database FOR Employee

    IF request.hours > currentBalance THEN
        RETURN "Insufficient"
    ELSE
        RETURN "Sufficient"
    END IF

END FUNCTION
