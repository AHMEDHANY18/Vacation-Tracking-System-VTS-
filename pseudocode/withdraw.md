// -------------------------------------------------------
// FUNCTION: WithdrawPendingRequest
// PURPOSE:  Allows employee to withdraw a pending vacation request
// ACTORS:   Employee, Manager, System
// -------------------------------------------------------

FUNCTION WithdrawPendingRequest():

    // Step 1 – Display pending vacation requests
    DISPLAY "Vacation Summary (Last 6 Months - Next 18 Months)" TO Employee

    Employee selects a request WHERE status = "Pending Approval"

    IF selectedRequest IS NULL THEN
        SHOW "No valid pending request selected"
        RETURN
    END IF

    // Step 2 – Confirm withdrawal action
    PROMPT "Confirm withdrawal of selected vacation request?" (Yes / No)

    IF Employee selects "No" THEN
        SHOW "Withdrawal canceled"
        RETURN
    END IF

    // Step 3 – Process withdrawal
    REMOVE selectedRequest FROM ManagerPendingList
    UPDATE selectedRequest.status = "Withdrawn"

    // Step 4 – Notify the manager
    SEND email TO Manager:
        SUBJECT: "Vacation Request Withdrawn"
        BODY: "Employee [Name] has withdrawn a pending vacation request."

    // Step 5 – Log and finalize
    LOG "Request [requestID] withdrawn successfully"
    SHOW "Your vacation request has been withdrawn successfully"

    REFRESH Employee vacation summary
    RETURN

END FUNCTION


FUNCTION ValidatePendingRequest(request):

    IF request.status != "Pending Approval" THEN
        RETURN "Invalid"
    ELSE
        RETURN "Valid"
    END IF

END FUNCTION
