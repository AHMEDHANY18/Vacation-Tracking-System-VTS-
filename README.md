# 🧾 Vacation Tracking System (VTS)

A complete web-based system for managing employee vacation and leave requests — developed as part of the **Object-Oriented Analysis and Design (OOAD)** coursework.

---

## 🧩 Overview
The **Vacation Tracking System (VTS)** automates the process of requesting, approving, and tracking employee vacations.
It minimizes manual HR workload and ensures accurate, transparent, and rules-based vacation management.

---

## 📘 UML Diagrams

### 1️⃣ Use Case Diagrams
Each use case focuses on a specific scenario of the system.

- ![Create Request](./usecases/usecase-create.png)
- ![Edit Pending Request](./usecases/usecase-edit.png)
- ![Withdraw Pending Request](./usecases/usecase-withdraw.png)
- ![Cancel Approved Request](./usecases/usecase-cancel.png)

---

### 2️⃣ Flowcharts
Detailed visual flow of how each process executes.

- ![Create Flowchart](./flows/flowchart-create.png)
- ![Edit Flowchart](./flows/flowchart-edit.png)
- ![Withdraw Flowchart](./flows/flowchart-withdraw.png)
- ![Cancel Flowchart](./flows/flowchart-cancel.png)

---

### 3️⃣ Sequence Diagrams
Illustrate the interaction between **Employee**, **System**, and **Manager** step-by-step.

- ![Create Sequence](./sequences/seq-create.png)
- ![Edit Sequence](./sequences/seq-edit.png)
- ![Withdraw Sequence](./sequences/seq-withdraw.png)
- ![Cancel Sequence](./sequences/seq-cancel.png)

---

### 4️⃣ Class Diagram
![Class Diagram](./diagrams/calss.png)

Defines the structural relationships between classes like `Employee`, `Manager`, `VacationRequest`, `LeaveCategory`, and supporting services (e.g. EmailService, ValidationService).

---

### 5️⃣ Entity Relationship Diagram (ERD)
![ERD](./diagrams/ERD.png)

Describes database tables, relationships, and entity dependencies for VTS.

---

### 6️⃣ State Machine Diagram
![State Machine](./docs/state-machine.png)

Represents the full lifecycle of a vacation request (Created → Pending → Approved → HR Pending → HR Approved → Completed/Rejected/Withdrawn/Canceled).

---

## 🗂️ Documentation

| Category | File | Description |
|-----------|------|-------------|
| 🧾 Requirements | [Requirements.md](./docs/Requirements.md) | System goals, functional & non-functional requirements |
| ⚙️ Pseudocode | [Create](./pseudocode/create.md) – [Edit](./pseudocode/edit.md) – [Withdraw](./pseudocode/withdraw.md) – [Cancel](./pseudocode/cancel.md) | Step-by-step pseudocode for each major flow |
| 🧭 HR Scenario | [HR Approval](./docs/hr_approval.md) | Describes the HR-level approval process |
| 🧠 State Machine | [state-machine.png](./docs/state-machine.png) | State transition visualization |
| 🧩 UI Mockups | [Employee UI](./ui/employee-ui.md) & [Manager UI](./ui/manager-ui.md) | Layout and design sketches for both user interfaces |

---

## 🧱 System Features

### 👤 Employee
- Submit vacation requests
- Edit or withdraw pending requests
- Cancel approved requests (if applicable)
- View vacation history and remaining balance

### 🧑‍💼 Manager
- View pending requests
- Approve or reject vacation requests
- View request history per employee
- Forward certain requests to HR

### 🏢 HR Department
- Review HR-level approvals
- Manage employee leave balances
- Access and audit vacation history

---

## ⚙️ Technologies & Tools
| Type | Tool / Platform |
|------|-----------------|
| **Design & Diagrams** | [Excalidraw](https://excalidraw.com), Draw.io |
| **Documentation** | Markdown (`.md`) |
| **Version Control** | Git & GitHub |
| **Modeling Standard** | UML 2.0 & OOAD Principles |

---

## 🔍 System Highlights
- Fully modular structure (flows, pseudocode, sequences, use cases)
- Clear separation between **Employee**, **Manager**, and **HR** layers
- Comprehensive documentation following **OOAD standards**
- Designed for future scalability (e.g., adding `HR_Approval` or `Finance_Check`)
- Consistent naming and visual structure for professional readability

---

## 👨‍💻 Author
**Ahmed Hany**
_Object-Oriented Analysis and Design Project_
Faculty of Computers and Artificial Intelligence – Cairo University

---

⭐ **If you find this project helpful, please give it a star on GitHub!**
