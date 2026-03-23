# Product Requirements Document (PRD) - TODO App Upgrade

## 1. Overview

We are upgrading the current TODO app, which today supports only a task title and completion state, to make task management more practical while keeping the implementation simple and teachable. The MVP focuses on adding due dates, priorities, and date-based filters without backend changes. Additional UX behavior such as overdue highlighting and multi-criteria sorting is intentionally deferred to Post-MVP. Several advanced capabilities remain explicitly out of scope.

---

## 2. MVP Scope

- Keep architecture/storage local only; no backend changes and no external storage.
- Add task field dueDate as optional ISO date in YYYY-MM-DD format.
- Add task field priority as enum P1, P2, P3.
- Set default priority to P3 when not provided.
- Keep title required.
- Add filters/tabs: All, Today, Overdue.
- In filter behavior:
  - All view includes completed tasks.
  - Today view shows incomplete tasks only.
  - Overdue view shows incomplete tasks only.
- Validate dueDate input so invalid values are ignored and treated as absent.
- Keep MVP lean, simple, and teachable.

---

## 3. Post-MVP Scope

- Visually highlight overdue tasks.
- Add sorting with this order:
  - Overdue tasks first.
  - Then by priority in order P1 to P3.
  - Then by due date ascending.
  - Tasks without due dates last.

---

## 4. Out of Scope

- Notifications.
- Recurring tasks.
- Multi-user functionality.
- Keyboard navigation and special accessibility features.
- External storage.
