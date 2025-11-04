# Vacation Tracking System (VTS) – Requirements Document

## Vision
The **Vacation Tracking System (VTS)** is designed to automate and simplify the management of employee vacation and leave requests within an organization. Traditionally, this process was entirely manual and paper-based, requiring HR staff to verify available leave balances and managers to review and approve each request. This often resulted in unnecessary delays, redundant approvals, and a heavy administrative workload.

The new **VTS** provides a modern, web-based solution that allows employees to view their vacation history for the previous six months and plan future requests up to 18 months ahead. The system enables managers to review and approve requests directly, while HR retains control over leave balances and policy rules without being involved in every individual transaction.

By implementing a flexible, rules-based validation engine, the system ensures accuracy, consistency, and fairness in managing leave requests. Additionally, automated email notifications, audit logs, and seamless integration with the company’s intranet and HR legacy systems enhance efficiency and transparency.

Ultimately, the vision of the **Vacation Tracking System** is to **empower employees**, **reduce HR overhead**, and **streamline organizational workflows** through an intuitive, secure, and easy-to-use platform.

---

## Functional Requirements
1. The system shall allow employees to log in through the company’s intranet using single sign-on (SSO).
2. The system shall display an employee’s vacation history for the past six months.
3. The system shall allow employees to create new vacation requests by selecting leave type, dates, and hours.
4. The system shall validate each request based on available leave balance and company policies.
5. The system shall send an email notification to the manager upon a new vacation request submission.
6. The system shall allow managers to review, approve, or reject requests.
7. The system shall require a reason when a request is rejected.
8. The system shall automatically update the employee’s leave balance upon approval.
9. The system shall send an email notification to the employee when the manager approves or rejects a request.
10. The system shall allow HR staff and administrators to override rules with logging of such actions.
11. The system shall maintain logs of all activities and approvals.
12. The system shall integrate with the HR legacy database to sync employee information and leave data.

---

## Non-Functional Requirements
1. The system shall be **easy to use** with an intuitive and responsive web interface.
2. The system shall provide secure authentication using the company’s SSO framework.
3. The system shall ensure that all data transfers are encrypted.
4. The system shall be available **24/7** with at least 99.5% uptime.
5. The system shall process and display responses within **2 seconds** under normal load.
6. The system shall be scalable to support an increasing number of employees.
7. The system shall log all user and administrative actions for auditing.
8. The system shall integrate smoothly with the existing intranet portal and email services.
9. The system shall provide error handling and user-friendly feedback messages.
10. The system shall support future extensions such as mobile access or reporting dashboards.

---

## Constraints
1. The system must operate within the company’s existing **intranet and middleware environment**.
2. The system must use the existing **HR database and data structure**.
3. The system shall rely on the organization’s **email infrastructure** for notifications.
4. Development must comply with the company’s **IT security and privacy policies**.
5. Only web technologies approved by the IT department may be used.
6. Deployment must be compatible with the organization’s current web servers and hardware.

---

## Assumptions
1. All employees and managers have access to the company’s intranet portal and a valid company email account.
2. HR data in the legacy systems is accurate and regularly updated.
3. Managers are responsible for approving or rejecting vacation requests for their direct subordinates.
4. Each employee has a predefined vacation balance in the HR system.
5. The organization’s network and email systems are fully functional and reliable.
6. Only authorized users can access or modify vacation data.
7. All employees are familiar with the company’s vacation policy and request procedure.

---

*End of Document*
