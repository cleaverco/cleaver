# **Project Charter: Cleaver**

* **Name:** Cleaver
* **Tagline:** Map and manage your personal relationships.
* **Vision:** To create a simple, private, and powerful tool to visualize and nurture one's personal and familial network. It begins as a superior alternative to a standard contacts app and evolves into a meaningful, interactive map of your life's connections.
* **Core Principles:**
  * **Start Small, Deliver Value:** Every phase must result in a more useful application. We prioritize shipping a working feature over planning a perfect one.
  * **Simplicity is Paramount:** The user interface, the codebase, and the deployment process will be kept as simple as possible to respect limited development time and encourage future contribution.
  * **You Own Your Data:** Getting data in and out is a fundamental right. The application will use open standards and make exporting your entire dataset trivial.
  * **Pragmatic, Not Perfect:** This is a personal project. We will favor practical solutions that work now over complex solutions that might be theoretically better later.

## **Technology Foundation**

* **Backend:** Python with the Django framework.
* **Frontend:** HTMX for dynamic user interfaces, styled with Tailwind CSS.
* **Database:** SQLite for simplicity and ease of deployment, with the ability to switch to PostgreSQL for future scaling.
* **Deployment:** A single Docker container for a simple, one-command launch.

---

## **Project Roadmap: From Contacts to Connections**

This roadmap is broken into phases, each with a clear goal and distinct milestones.

### **Phase 0: The Foundation (Setup & CI)**

*Goal: Create a stable, deployable skeleton of the application.*

* **Milestone 1: Project Initialization.**
  * Set up the Django project structure.
  * Initialize a Git repository.
  * Create the basic `User` model.
* **Milestone 2: Authentication.**
  * Integrate a third-party authentication library (`django-allauth` is recommended).
  * Implement a single sign-on method to start (e.g., "Sign in with Google" or "GitHub"). This completely bypasses the need to build and secure a password system.
* **Milestone 3: "Hello, Docker!".**
  * Create a `Dockerfile` that builds and runs the application.
  * Successfully run the empty project via `docker-compose up`. This confirms the deployment strategy works from day one.

### **Phase 1: The Core PRM (The MVP)**

*Goal: Build a functional contacts application that is immediately useful by prioritizing data import.*

* **Milestone 1: The `Contact` Model.**
  * Design and create the database model for a `Contact`.
  * Include essential fields: `first_name`, `last_name`, `birthday`, `email`, `phone_number`, and a flexible `notes` field.
* **Milestone 2: Basic UI & Data Management.**
  * Create a simple, read-only list view to display all contacts.
  * Create a read-only detail view for a single contact.
  * **Leverage the Django Admin Panel** for all initial Create, Update, and Delete (CRUD) operations. This provides a secure, functional data management UI for free.
* **Milestone 3: CSV Import.**
  * Build a simple page where a user can upload a CSV file (from Google Contacts, etc.).
  * Implement the logic to parse the file and create `Contact` objects in the database. This is the single most important feature for initial user adoption.
* **Milestone 4: vCard Import.**
  * Add the ability to import standard `.vcf` (vCard) files, a common format for sharing single contacts.

### **Phase 2: The Connected Network**

*Goal: Introduce the core differentiating feature: relationships.*

* **Milestone 1: The `Relationship` Model.**
  * Create a database model to link two `Contact` records.
  * It will include the `from_contact`, the `to_contact`, and a `type` field (e.g., "Friend", "Parent of", "Spouse of").
* **Milestone 2: Viewing Relationships.**
  * On the `Contact` detail page, add a new section that lists all relationships associated with that person.
* **Milestone 3: Creating Relationships.**
  * Using HTMX, add a simple form to the contact detail page that allows the user to select another contact and define the relationship between them without a full page reload.

### **Phase 3: The Genealogical Bridge**

*Goal: Achieve compatibility with the GEDCOM standard for data portability.*

* **Milestone 1: GEDCOM Export.**
  * Create a function that generates a valid GEDCOM file from the contacts and relationships in the database. This provides a powerful "data out" feature and aligns with the principle of data ownership.
* **Milestone 2: Basic GEDCOM Import.**
  * Implement a parser for GEDCOM files that focuses only on the most critical tags: `INDI` (for individuals/contacts) and `FAM` (for family units/relationships).
  * Any unrecognized data from the import can be stored in the `notes` field of the relevant contact to prevent data loss.

### **Phase 4: Enhancing the Experience**

*Goal: Add quality-of-life features that make the application more proactive and enjoyable to use.*

* **Milestone 1: Interaction Logging.**
  * Create a simple model to log an `Interaction` linked to a contact (e.g., a date and a text description like "Had lunch").
  * Display a reverse-chronological list of these interactions on the contact detail page.
* **Milestone 2: Event Reminders.**
  * Build a simple system to scan for upcoming birthdays from your contacts.
  * Display a "Upcoming Birthdays" section on the main dashboard.
* **Milestone 3: Inline Editing.**
  * Enhance the UI by using HTMX to allow editing of contact fields directly on the detail page, reducing reliance on the Django Admin for everyday use.

---

### **Beyond the Roadmap: Future Stretch Goals**

These are ideas to consider only after the core roadmap is complete. They are not part of the initial plan.

* **Visual Graph View:** A dedicated page to visualize the entire network of contacts and relationships as an interactive graph.
* **Advanced PWA:** Improve the mobile experience by making the app a full-fledged Progressive Web App (PWA) that can be "installed" on a phone's home screen.
* **REST API:** Expose the data via a secure, read-only API to enable other applications or scripts to interact with the data.
* **Optional AI Module:** A separate, opt-in service that could analyze the network to suggest potential duplicate contacts or missing relationships.
