
# MedGuard

### Intelligent Medication Safety Assessment System

**Project Title:** Development of an Intelligent System for Medication Safety Assessment Based on Patient Medical History

**University:** Astana IT University  
**Programme:** Software Engineering  
**Project Type:** Diploma Project  
**Status:** Analysis and Design

---

## Overview

**MedGuard** is an intelligent web-based clinical decision-support system designed to assess medication-safety risks based on structured and unstructured patient medical history.

The system combines:

- Natural Language Processing (NLP)
- Rule-based medication safety checks
- Evidence-grounded AI explanations
- Patient medical history management
- Appointment scheduling and booking
- Medication intake schedules
- Telegram-based reminders and chatbot functionality

MedGuard helps physicians identify potential medication-related risks while keeping final clinical decisions under the physician's control.

> **Important:** MedGuard is a clinical decision-support tool. It does not autonomously diagnose patients or prescribe medications.

---

## Problem Statement

Medication safety assessment requires physicians to consider multiple factors:

- Current medications
- Drug allergies
- Chronic conditions
- Previous medical history
- Potential drug interactions
- Duplicate therapies

Medical information may be incomplete, distributed across different records, or stored as unstructured text.

**MedGuard aims to solve this problem** by integrating medical history analysis, medication safety rules, and evidence-linked explanations into one web application.

---

## Target Users

MedGuard supports **three user roles**.

### 1. Doctor

Doctors can:

- View patient medical histories within their clinic
- Publish available appointment slots
- View scheduled appointments
- Record patient visits
- Review and confirm extracted medical information
- Check medications for potential safety risks
- View evidence-based alerts and explanations
- Accept risks with justification
- Generate and approve medication schedules

### 2. Patient

Patients can:

- Create and manage their profiles
- Enter and update their medical histories
- Browse available appointment slots
- Book or cancel appointments
- Complete pre-visit questionnaires
- View physician-approved medication schedules
- Receive Telegram reminders
- Interact with the Telegram chatbot

### 3. Administrator

Administrators can:

- View the number of clinics using MedGuard
- View doctors associated with each clinic
- View aggregated usage statistics
- Access login and event journals
- Activate or deactivate doctor accounts

**Access restrictions:**

Administrators cannot:

- Access patient medical histories
- View personal or clinical patient data
- Modify medical records
- Edit medication safety rules
- Import patient records

---

## Core Features

### 1. Patient Medical History Management

Patients enter their medical information, including:

- Chronic conditions
- Allergies
- Current medications
- Previous illnesses and operations
- Additional medical remarks

Doctors can review, confirm, correct, or reject patient-reported information.

### 2. Appointment Booking

- Doctors publish available appointment slots.
- Patients filter slots by clinic, specialty, doctor, and date.
- Patients book or cancel appointments.
- Booked slots become unavailable to other patients.

### 3. Medication Safety Assessment

MedGuard checks proposed medications for:

| Check Type | Description |
|---|---|
| Drug–Drug Interactions | Detects potentially dangerous medication combinations |
| Drug–Allergy Conflicts | Identifies conflicts with recorded allergies |
| Drug–Disease Contraindications | Checks medications against existing conditions |
| Duplicate Therapy | Detects duplicate active ingredients or drug classes |
| Dose Range Check | Compares prescribed doses with available reference ranges |

### 4. Explainable Safety Alerts

Medication safety results are classified into three levels:

| Risk Level | Description |
|---|---|
| Critical | Potentially dangerous medication-related risk |
| Review | Requires additional physician attention |
| Informational | No significant risk identified by the applicable checks |

Each alert includes:

- Risk level
- Conflicting medications or patient factors
- Explanation of the potential risk
- Recommended action
- Supporting evidence and source references

The final decision always belongs to the physician.

### 5. Medication Schedule Generation

MedGuard generates medication intake schedules based on physician-approved prescriptions.

Schedules may include:

- Medication name
- Dosage
- Intake time
- Frequency
- Course duration
- Instructions related to meals

Doctors review and approve schedules before patients can access them.

### 6. Telegram Integration

Telegram functionality includes:

- Medication reminders
- Appointment notifications
- Pre-visit questionnaires
- Medication intake confirmation
- Chatbot assistance with medication schedules

The chatbot does not diagnose patients or independently modify prescriptions.

---

## AI and NLP

MedGuard uses AI-assisted processing to extract structured medical information from clinical notes.

The NLP module identifies:

- Medical conditions
- Allergies
- Medications
- Dosages and frequencies
- Relevant medical observations

Extracted information must be confirmed by the doctor before it is used in medication safety checks.

### Evidence-Grounded Explanations

The system uses Retrieval-Augmented Generation (RAG) to produce explanations supported by medical references.

**Safety principle:** The language model cannot independently create, modify, or remove medication safety alerts.

---

## Planned Technology Stack

| Component | Technology |
|---|---|
| Frontend | React, Next.js, TypeScript |
| Backend | Python, FastAPI |
| Database | PostgreSQL |
| Vector Search | pgvector |
| AI/NLP | Locally hosted open-weight LLM |
| Evidence Retrieval | RAG |
| Drug Information | RxNorm/RxNav, DDInter 2.0, openFDA, DailyMed |
| Background Jobs | Celery, Redis |
| Notifications | Telegram Bot API |
| Deployment | Docker Compose |
| Version Control | Git, GitHub |
| Project Management | YouTrack |

---

## Security and Privacy

MedGuard follows privacy-focused design principles.

- Only synthetic patient data are used during development and evaluation.
- Synthetic records are generated using the team's own scripts.
- Role-based access control restricts access to information.
- Patients can access only their own medical information.
- Doctors can access only patients associated with their clinic.
- Administrators cannot access personal or clinical patient data.
- Login and event journals use pseudonymous identifiers.
- The language model is planned to run locally.
- Medical decisions remain under physician supervision.

---

## Project Scope

### In Scope

- Web application with three user roles
- Patient profiles and medical histories
- Appointment booking
- Medication safety assessment
- NLP-based medical information extraction
- Evidence-based safety explanations
- Medication schedule generation
- Telegram reminders and chatbot
- Audit logging
- Synthetic patient database
- Technical evaluation

### Out of Scope

- Real patient data
- Production hospital system integration
- Autonomous diagnosis
- Autonomous prescribing
- Native mobile applications
- Progressive Web App (PWA)
- Administrator access to clinical records
- Medication rule editing through the administrator interface
- Synthea import as an application feature
- Clinical-outcome studies

---

## Expected Outcomes

The project aims to deliver:

1. A working web-based MedGuard prototype.
2. Role-based interfaces for Doctor, Patient, and Administrator.
3. A medication safety rule engine.
4. NLP-based medical information extraction.
5. Evidence-grounded safety alerts.
6. Physician-approved medication schedules.
7. Telegram-based reminders and chatbot.
8. A reproducible synthetic patient database.
9. Technical evaluation results.
10. Complete project documentation.

---

## Development Team

| Team Member | Responsibilities |
|---|---|
| **Yertay Altynay Talgatkyzy** | ML Engineer (Lead), Research Head, Backend Developer, Frontend Developer |
| **Salemkan Aknur Seitkankyzy** | Head of Backend, DevOps, Business Analyst, UI/UX Designer, ML Developer |
| **Nuraly Nuray Bakytzhankyzy** | Project Manager, Head of Frontend, QA Engineer, ML Developer |

### Academic Supervisor

**Orazova Arailym Zhanbolatkyzy**

Astana IT University

---

## Project Documentation

Project documentation is maintained in the `docs/` directory.

| Section | Document |
|---|---|
| 1 | Project Proposal |
| 2 | Evidence of Relevance |
| 3 | Literature Review |
| 4 | Existing System Comparison |
| 5 | Technology Comparison |
| 6 | Requirements Specification |
| 7 | System Architecture and Use Cases |
| 8 | UX/UI Design |
| 9 | Verification and Evaluation |
| 10 | Project Management and Risks |
| 11 | Supervisor Feedback |

Additional project materials include:

- `diagrams/` — System architecture and use case diagrams
- `prototype/` — UI prototype and design materials
- `docs/` — Academic and technical documentation

---

## Project Management

Project planning and task tracking are managed through **YouTrack**.

 **[MedGuard YouTrack Project](https://medguard.youtrack.cloud/projects/MED)**

Development workflow:

1. Create a task in YouTrack.
2. Assign an owner and acceptance criteria.
3. Create a Git branch for the task.
4. Implement the required changes.
5. Open a Pull Request.
6. Request a review from another team member.
7. Merge approved changes.

---

## Setup and Installation

> **Current status:** The project is in the analysis and design phase.

The application is not yet available as a fully runnable system.

Installation and configuration instructions will be added after implementation.

Planned deployment will use **Docker Compose**.

---

## Testing and Evaluation

The planned evaluation includes:

- Unit testing
- Integration testing
- Medication safety rule validation
- NLP extraction evaluation
- AI explanation quality assessment
- Security and access control testing
- Usability testing
- Performance testing

Only synthetic patient data will be used for development, demonstration, and evaluation.

---

## Current Project Status

**Phase:** Analysis and Design

Current activities include:

- Requirements specification
- Use case modelling
- Architecture design
- UI/UX prototyping
- Technology selection
- Project documentation
- Planning of implementation and testing

---

## License

License information will be added after the team confirms the project's distribution terms.

Third-party drug information sources are subject to their respective licenses and attribution requirements.

---

**MedGuard — Supporting safer medication decisions through explainable AI.**
