FUNCTION CancelApprovedRequest():

    // Step 1 – Display all approved requests
    DISPLAY "Vacation Summary (Last 6 Months - Next 18 Months)" TO Employee

    Employee selects a request WHERE status = "Approved"

    IF selectedRequest IS NULL THEN
        SHOW "No approved vacation request selected"
        RETURN
    END IF

    // Step 2 – Validate cancellation eligibility
    CALL ValidateRequestDate(selectedRequest.startDate)

    IF validationResult == "Invalid" THEN
        SHOW "This request cannot be canceled (date too old or invalid)"
        RETURN
    END IF

    // Step 3 – Determine cancellation type
    IF selectedRequest.startDate IS IN Future THEN
        PROMPT "Confirm cancellation of this future request?" (Yes / No)

        IF Employee selects "No" THEN
            SHOW "Cancellation aborted"
            RETURN
        END IF

        CALL ProcessCancellation(selectedRequest, requiresReason = False)

    ELSE IF selectedRequest.startDate IS IN RecentPast (≤ 5 business days) THEN
        PROMPT "Provide reason for cancellation and confirm (Yes / No)"

        IF Employee selects "No" OR reason IS EMPTY THEN
            SHOW "Cancellation aborted - reason required"
            RETURN
        END IF

        CALL ProcessCancellation(selectedRequest, requiresReason = True, reason)
    END IF

    SHOW "Vacation request canceled successfully"
    RETURN

END FUNCTION


FUNCTION ValidateRequestDate(startDate):

    today = CURRENT_DATE()

    IF startDate < today - 5 business days THEN
        RETURN "Invalid"

    RETURN "Valid"
END FUNCTION


FUNCTION RestoreVacationBalance(request):

    FETCH employeeBalance FROM Database WHERE employeeId = request.employeeId
    employeeBalance += request.totalHours
    UPDATE employeeBalance IN Database

    RETURN
END FUNCTION
