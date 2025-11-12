# 🧑‍💼 HR Approval Scenario – Vacation Tracking System (VTS)

## 🎯 Goal
To add an additional approval layer by the **HR Department** after a manager approves a vacation request.

---

## ⚙️ Preconditions
- The employee has a **vacation request** that has been approved by their manager.
- HR personnel are authenticated via the intranet portal.
- The system automatically forwards approved requests to HR for review.

---

## 🔁 Main Flow

1. The system changes the request status to `HR Pending Approval` after manager approval.
2. The HR officer logs in to the system.
3. The HR dashboard displays all requests with status = `HR Pending Approval`.
4. The HR officer selects a request to review.
5. The system displays full employee details:
   - Vacation dates, type, and duration.
   - Employee department and remaining balance.
   - List of other employees on vacation during the same period.
6. HR reviews the request and takes one of the following actions:
   - ✅ **Approve** → The system updates status to `HR Approved`.
   - ❌ **Reject** → The system updates status to `HR Rejected`.
7. The system sends an email notification to:
   - Employee (status update)
   - Manager (for awareness)
8. The request moves to the final state depending on HR’s decision.

---

## 🧾 Postconditions
| **Status** | **Description** |
|-------------|----------------|
| `HR Approved` | The vacation is fully authorized and finalized. |
| `HR Rejected` | HR has denied the vacation request due to policy conflict or scheduling issues. |

---

## 🔔 Notifications
- **To Employee:** "Your vacation request has been reviewed by HR – Status: Approved / Rejected."
- **To Manager:** "HR has completed review of [Employee Name]’s vacation request."

---

## 🧠 Notes
- HR can override manager decisions when scheduling conflicts occur.
- System logs every HR action for auditing.
- HR dashboard includes filters for department, dates, and request status.

---

## 🔄 State Transition Summary
| **From** | **Action** | **To** |
|-----------|------------|--------|
| `Approved` | Forward to HR | `HR Pending Approval` |
| `HR Pending Approval` | HR Approves | `HR Approved` |
| `HR Pending Approval` | HR Rejects | `HR Rejected` |
