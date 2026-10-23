# Requirements specification

Task: MED-8. Word version: `docs/06-requirements-specification.docx`. This file is the readable GitHub version of the same tables.

Priorities follow MoSCoW: **Must** is needed for the diploma prototype, **Should** is planned and valuable, **Could** is done if time allows. Use cases (UC) are defined in `docs/07-use-case-catalogue.md`. P1-Qn refers to question n of the physician interview in `docs/interviews/P1-physician-interview.md`.

## Roles

| Role | Can | Never |
|---|---|---|
| Doctor | Publish free slots, open the history of patients of the own clinic, record the visit, run the safety check, decide on alerts, approve the schedule | Open patients of another clinic, change the journals |
| Patient | Create a profile, write the own history, book a free slot, fill the questionnaire, see the own schedule, receive reminders | See other patients, see the doctor's alerts |
| Administrator | See the number of clinics, doctors per clinic, login and event journals; activate or deactivate a doctor account | See personal or clinical data, import data, edit the database or rules |

## Functional requirements

### Access and roles

| ID | Requirement | Priority | Acceptance criterion | UC | Basis |
|---|---|---|---|---|---|
| FR-01 | The system has exactly three roles: Doctor, Patient, Administrator. Users sign in with a login and password; the role decides which screens and API calls are available. | Must | Automated test: every endpoint is called with each role and with no session; only the calls listed in the permission matrix (Table 2) succeed, all others return 401/403. | UC-01 | Product logic; NFR-07 |
| FR-02 | The Administrator account can never read personal or clinical data: no patient names, contacts, history, diagnoses, medicines, visit notes or schedules. Logs show only pseudonymous user IDs and roles. | Must | Test: all Administrator-visible endpoints and screens are scanned against a list of personal and clinical fields; none appears. Direct calls to patient endpoints with an Administrator token return 403. | UC-22 to UC-25 | P1-Q15 (data must not leave the clinic); privacy by design |
| FR-03 | Every Doctor account is linked to one clinic and one specialty (therapist, cardiologist or any other). A doctor works only with patients of the own clinic. | Must | Seed data contain at least 3 clinics with at least 3 specialties; a doctor of clinic A cannot open a record or a slot of clinic B (403). | UC-01 | P1-Q1; product logic |

### Patient profile and medical history

| ID | Requirement | Priority | Acceptance criterion | UC | Basis |
|---|---|---|---|---|---|
| FR-04 | A person who is not yet in the database can create a patient profile on their own: name, date of birth, sex, contact, and optional first entries of the medical history. A profile is required before the first booking. | Must | A new user completes registration in at most 3 minutes; booking is blocked with a clear message until the profile exists; duplicate profile (same identifier) is rejected. | UC-02 | P1-Q5, Q7, Q8 (history is incomplete and scattered) |
| FR-05 | The Patient enters and edits the own medical history: past illnesses and operations, chronic conditions, allergies with reaction, current medicines including over-the-counter drugs and supplements, free-text remarks. Every entry is labelled "patient-reported" with a date. | Must | Patient adds one entry of each type; entries appear in the doctor's view of the same patient within 5 seconds with the label and date; the patient cannot see or edit other patients. | UC-03 | P1-Q5, Q7, Q8 |
| FR-06 | When a patient with a profile comes to the appointment, the Doctor opens the full history on one screen: conditions, allergies, current medicines, previous visits, patient-reported remarks, each with its source label (patient-reported, doctor-confirmed, visit record). | Must | For 10 random synthetic patients, all stored entities are visible and carry the correct source label; opening a record creates an audit event. | UC-11 | P1-Q2, Q8 |
| FR-07 | The Doctor can confirm, correct or reject a patient-reported entry. Confirmed entries get the label "doctor-confirmed"; rejected entries stay in the log but are not used in the safety check. | Should | Rejected entry does not trigger any alert; confirmation changes the label and is audited. | UC-12 | P1-Q7 (patients do not name everything; history must be verified) |
| FR-08 | Diagnoses and chronic conditions are stored with ICD-10 codes and a Russian display name. | Should | 100 % of conditions in the synthetic database have a valid ICD-10 code; the doctor can search a condition by code or by name. | UC-03, UC-13 | Project decision; P1-Q8 (structured fields not always filled) |

### Appointment booking

| ID | Requirement | Priority | Acceptance criterion | UC | Basis |
|---|---|---|---|---|---|
| FR-09 | A Doctor of any specialty publishes availability slots: date, start time, duration and clinic. Slots that are not booked can be edited or removed. | Must | Doctor creates 10 slots in under 2 minutes; overlapping slots for the same doctor are rejected; a booked slot cannot be deleted without cancelling the booking. | UC-09 | Product logic (booking by free time) |
| FR-10 | The Patient sees the free slots of doctors, filtered by clinic, specialty, doctor and date. | Must | Only unbooked future slots are listed; filters combine; the list updates within 5 seconds after another patient books a slot. | UC-04 | Product logic |
| FR-11 | The Patient books one free slot; the slot immediately becomes unavailable to others. The patient can cancel the booking, which releases the slot (reschedule is cancel plus new booking). | Must | Two parallel booking attempts on the same slot: exactly one succeeds. Cancel returns the slot to the free list. Both actions are audited. | UC-05 | Product logic |
| FR-12 | The Doctor sees the own appointments for a day or week and opens the patient record from an appointment. | Must | The list shows exactly the booked slots of this doctor, sorted by time; one click opens the history of the booked patient. | UC-10 | P1-Q4 (25 to 30 visits a day); prototype Home and Patients |
| FR-13 | The Doctor has a patient list with search by name and a filter by status (risk, to check, normal). | Must | Search returns a patient in under 1 second for 10,000 records; the filter shows only patients with the chosen status. | UC-10 | Prototype Patients screen |
| FR-14 | The Patient receives a confirmation and a reminder of the appointment in the chosen channel (Telegram). | Could | A reminder is sent 24 hours and 2 hours before the slot; a cancelled booking sends a cancellation notice. | UC-05, UC-07 | P1-Q14 |
| FR-15 | Before the appointment the Patient can answer a short questionnaire about complaints (in the application or through the Telegram bot). The Doctor sees the answers in the visit record, labelled "patient-reported". | Should | Answers saved before the slot time appear in the visit record with the label and time; the doctor can edit or discard them. | UC-27 | Prototype (pre-visit questionnaire, bot dialogue); P1-Q8 |

### Doctor workspace and clinical record

| ID | Requirement | Priority | Acceptance criterion | UC | Basis |
|---|---|---|---|---|---|
| FR-16 | The Doctor records the visit as free text (complaints, history, findings) next to the structured fields. | Must | Free text up to 5,000 characters is saved with the visit and shown in the history; edits are versioned. | UC-13 | P1-Q8 (visit notes are free text) |
| FR-17 | The system extracts conditions, allergies, medicines (with dose and frequency) and key observations from the free text into a fixed structure and shows them as suggestions. | Must | On the held-out synthetic notes set, entity-level F1 is at least 0.80 for medicines and allergies; output always validates against the schema. | UC-13, UC-14 | P1-Q13 (paste the list or the discharge summary); literature (n2c2) |
| FR-18 | Extracted entities are never used automatically. The Doctor confirms, edits or rejects each one first. | Must | With no confirmation the entities are not part of the patient's active list and do not enter any check; every confirmation is audited. | UC-14 | P1-Q9; human in the loop |
| FR-19 | Drug names (Russian brand names used in Kazakhstan, generic names, misspellings) are normalised to the active ingredient. Names that cannot be mapped are flagged, never dropped. | Must | At least 95 % of medicines in the test set map to the correct ingredient; every unmapped name is shown to the doctor as "not recognised". | UC-14, UC-15 | P1-Q15 (drugs sold in Kazakhstan, Russian brand names) |
| FR-20 | The Doctor searches a drug by brand or generic name and sees the active substance, group, form and the label sections used by the checks. | Must | The top-3 results contain the intended drug for at least 90 % of 50 test queries; search time is below 1 second. | UC-15 | P1-Q15; prototype Result screen |
| FR-21 | The Doctor enters a proposed medicine: drug, dose, frequency, duration and intake conditions. | Must | All fields are stored with the visit; saving a proposal starts the safety check automatically. | UC-16 | P1-Q2, Q11 |

### Medication safety check

| ID | Requirement | Priority | Acceptance criterion | UC | Basis |
|---|---|---|---|---|---|
| FR-22 | Check of the proposed medicine against the patient's active medicines for dangerous interactions. | Must | Unit tests with at least 20 curated positive and 20 negative pairs pass; recall on critical test scenarios is at least 0.95. | UC-16 | P1-Q3, Q5, Q6 |
| FR-23 | Check against the patient's allergies, including cross-reactivity within the drug class (for example penicillin and amoxicillin). | Must | At least 20 positive and 20 negative cases pass; the penicillin and amoxicillin case from the interview is raised as critical. | UC-16 | P1-Q5, Q6, Q10 |
| FR-24 | Check against the patient's conditions (contraindication by diagnosis), for example NSAIDs in gastritis or decongestants in hypertension. Pregnancy-specific rules are not part of this version. | Must | At least 20 positive and 20 negative cases pass; NSAID with gastritis raises an alert. | UC-16 | P1-Q5, Q6, Q10 |
| FR-25 | Detection of duplicate therapy: the same active substance under different brand names, or two drugs of the same class (for example two NSAIDs). | Must | At least 20 positive and 20 negative cases pass; a combined cold powder plus paracetamol is flagged. | UC-16 | P1-Q6 (duplication is the most common error) |
| FR-26 | Dose check: single dose and daily dose of the proposed medicine are compared with the label range for the patient's age and shown as within range or exceeded. | Should | For 30 test cases the flag matches the label range in 100 % of cases; a missing range gives "range not available". | UC-16 | P1-Q6, Q10 (dose exceedance) |
| FR-27 | Every result has one of three levels: critical (do not prescribe), review (use with caution), informational (can be prescribed). Informational findings are collapsed by default. | Must | Each alert carries exactly one level; critical alerts cannot be hidden; in a test run informational items are collapsed on opening. | UC-16 | P1-Q10 (red cannot be skipped, yellow optional); alert fatigue literature |
| FR-28 | Each alert shows on one line the level, the two conflicting items, the mechanism, the patient factor that caused it, the recommended action (stop, replace, monitor) and the source with its version and date. | Must | 100 % of alerts in a test run contain all six elements; the source link opens the cited passage; up to 5 alerts fit on one screen without scrolling at 1440 x 900. | UC-16, UC-17 | P1-Q9, Q12 |
| FR-29 | The Doctor can accept a risk by entering a short mandatory comment. The decision is stored with the user, time and comment. | Must | Acceptance without a comment is rejected; accepted risk stays visible on the patient's card and in the audit log. | UC-18 | P1-Q12 (accept-risk button with comment) |
| FR-30 | When an alert is critical or review, the system offers one or two safer alternatives with a short justification. The Doctor decides; nothing is applied automatically. | Should | For 20 critical test cases at least one alternative is offered, each with a justification and a source; choosing it re-runs the check. | UC-19 | P1-Q11 |
| FR-31 | Any change of the medicine list, allergies or conditions triggers a repeat check of the full regimen. | Should | Changing a condition produces a new result within 5 seconds; the previous result stays in the history. | UC-16 | MedSafe FR-19; literature (final regimen re-check) |
| FR-32 | A natural-language explanation is generated from the rule result and the retrieved label passage. The language model can only explain; it cannot add, remove or change an alert. If no supporting passage is found, the explanation is replaced by the plain rule text. | Should | With the model disabled the set of alerts is identical; unsupported statements are at most 5 % of the evaluated sample; the fallback is triggered in 100 % of "no evidence" test cases. | UC-17 | Literature (RAG, hallucination); NFR-03 |

### Schedule and prescription output

| ID | Requirement | Priority | Acceptance criterion | UC | Basis |
|---|---|---|---|---|---|
| FR-33 | From the approved regimen the system builds a daily intake schedule (times, relation to meals, minimum intervals, course length). The Doctor edits and approves it; the final regimen is checked again before approval. | Must | For 30 test regimens all hard constraints are satisfied in 100 % of cases; an unapproved schedule is not visible to the patient. | UC-20 | P1-Q14; literature (adherence) |
| FR-34 | The Doctor exports the prescription and schedule as a PDF for printing or handing over. | Should | The PDF contains patient identifier, drugs, doses, schedule and date; it opens in standard viewers and prints on A4. | UC-21 | P1-Q14 (printout for older staff) |
| FR-35 | The Patient sees the approved schedule and the active prescriptions in the own account. | Must | After approval the schedule appears in the patient account within 5 seconds; the patient sees only own data. | UC-06 | P1-Q14 |

### Patient engagement

| ID | Requirement | Priority | Acceptance criterion | UC | Basis |
|---|---|---|---|---|---|
| FR-36 | Dose reminders are sent to the Patient through a Telegram bot at the scheduled times. The patient marks a dose as taken or skipped. | Should | In a 48-hour simulated run at least 99 % of reminders are sent within 60 seconds; dose events are stored. Detailed design is refined after 24 October. | UC-07 | P1-Q14, Q15; literature (adherence apps) |
| FR-37 | The Patient can talk to the MedGuard bot (in Telegram) about the own schedule and general information on the prescribed medicines. The bot does not diagnose and does not change prescriptions. Detailed design is refined after 24 October. | Could | In a scripted dialogue of 20 questions the bot answers from the stored schedule and label text, refuses diagnosis requests, and shows a disclaimer. | UC-08 | Product logic; to be refined |
| FR-38 | The Doctor sees a simple adherence indicator (share of doses taken) before a follow-up visit, without extra reports. | Could | The indicator equals a hand-computed value for 7 days of dose events. | UC-11 | P1-Q14 |

### Administrator: usage and logs

| ID | Requirement | Priority | Acceptance criterion | UC | Basis |
|---|---|---|---|---|---|
| FR-39 | The Administrator sees how many clinics use the application and the number of doctors and of active users per clinic. Only counts, no personal data. | Must | The numbers equal the database counts for the seed data; the screen contains no names of patients. | UC-22 | Product logic |
| FR-40 | The Administrator sees the list of clinics and, for each clinic, the doctors who work there: doctor name, specialty, account status. | Must | Each clinic shows exactly its doctors; no patient, appointment or clinical field is returned by the endpoint. | UC-23 | Product logic |
| FR-41 | The Administrator sees the login journal: time, pseudonymous user ID, role, result (success or failure). | Must | A scripted session of 10 logins (3 failed) appears in the journal with correct time and result; patient names are not shown. | UC-24 | Product logic |
| FR-42 | The Administrator sees the event journal: time, pseudonymous user ID, role, action type (for example booking, check run, risk accepted) and object type. The journal contains no clinical content. | Must | A scripted session of 20 actions creates 20 entries; no entry contains a diagnosis, drug name or note text. | UC-25 | Product logic |
| FR-43 | The Administrator filters the journals by clinic, role, date and result and exports the filtered view as CSV. | Should | Filter results match a hand-checked sample; the CSV contains the same columns as the screen. | UC-24, UC-25 | Product logic |
| FR-44 | The Administrator activates or deactivates a doctor account. This does not give access to any patient data and does not change the database content. | Should | A deactivated doctor cannot sign in, and the event is journalled; the doctor's past records are unchanged. | UC-26 | Product logic |

### Audit and interface language

| ID | Requirement | Priority | Acceptance criterion | UC | Basis |
|---|---|---|---|---|---|
| FR-45 | The system writes an audit event for every sign-in, record opening by a doctor, safety check, accepted risk, booking, cancellation and profile change. | Must | For a scripted session of 20 actions, 20 events exist with correct user, time and action; events cannot be edited through the application. | UC-01 to UC-27 | Medication-safety practice; P1-Q15 (unclear responsibility) |
| FR-46 | The interface is in Russian. An English interface is available for demonstration and for the committee. | Should | All labels of the main flows exist in both languages; switching does not lose the entered data. | UC-01 | Project context |

## Non-functional requirements

| ID | Category | Requirement and measurable criterion | Priority | Basis |
|---|---|---|---|---|
| NFR-01 | Performance | The safety check of a proposed medicine for a patient with up to 15 medicines returns the rule result in at most 3 seconds (95th percentile), and the model-written explanation in at most 10 seconds. | Must | P1-Q15 (works in a few seconds) |
| NFR-02 | Capacity | The system works for 20 simultaneous users and 10,000 patient records without exceeding the limits above. | Should | Project scale |
| NFR-03 | Safety | The language model never creates or removes an alert. Verified by a test that disables the model and compares the alert sets. | Must | Literature (hallucination) |
| NFR-04 | Safety | Missing or unmapped data give the explicit state "insufficient data", never "no risk". | Must | Fail-safe principle |
| NFR-05 | Decision support boundary | The system does not prescribe, choose doses or diagnose. The interface states that the final decision belongs to the doctor. | Must | P1-Q9, Q11 |
| NFR-06 | Security | Passwords are stored hashed (Argon2id or bcrypt); traffic uses TLS 1.2 or newer; sessions expire after 30 minutes of inactivity; five failed sign-ins lock the account for 15 minutes; secrets are kept in environment variables. | Must | Security baseline |
| NFR-07 | Access control | Authorisation is enforced on the server for every request. A patient reaches only own data; a doctor only patients of the own clinic; the Administrator no personal data. Verified by an automated test over all endpoints and roles. | Must | P1-Q15 |
| NFR-08 | Privacy | Patient data do not leave the deployment of the clinic. The language model runs locally; no patient text is sent to external services. Only synthetic data are used in the project. | Must | P1-Q15 (data must not leave the clinic) |
| NFR-09 | Auditability | The audit log is append-only, keeps entries for at least 12 months and contains no clinical content. Every alert can be reproduced from stored inputs, rule version and source date. | Must | Traceability |
| NFR-10 | Explainability | Every alert stores the rule identifier, the source, and the source version and date, and shows them to the doctor. | Must | P1-Q9 |
| NFR-11 | Usability | The result of a check with up to 5 alerts fits on one screen at 1440 x 900 without scrolling. Risk level is shown by colour plus a text label or icon. Informational items are collapsed. | Must | P1-Q10, Q12 |
| NFR-12 | Usability | System Usability Scale of at least 70 in a test with at least 5 participants; the main doctor flow (open patient, record, check, decide) takes at most 6 clicks from the patient list. | Should | Usability goal |
| NFR-13 | Accessibility | Text contrast meets WCAG 2.1 level AA; the main flows can be completed with the keyboard. | Should | Accessibility |
| NFR-14 | Compatibility | The web application works in the current versions of Chrome, Edge, Firefox and Safari on a desktop or laptop screen of at least 1366 x 768. | Must | P1-Q13 (main work at a computer) |
| NFR-15 | Localisation | Russian interface by default; English interface available; drug names shown with Russian brand names. | Should | P1-Q15 |
| NFR-16 | Reliability | Nightly database backup with a tested restore; availability of at least 99 % during working hours in the demonstration period. | Should | Operations |
| NFR-17 | Maintainability | Modular structure; at least 70 % unit-test coverage of the safety engine and the schedule generator; linting and tests run in CI on every pull request. | Should | Engineering practice |
| NFR-18 | Deployability | The whole system starts with one docker compose command on a laptop with 16 GB RAM. | Must | Reproducibility |
| NFR-19 | Interoperability | REST API described in OpenAPI 3; data model uses names compatible with FHIR R4; ICD-10 and active-ingredient codes are kept, so a later link to a clinic information system is possible. | Should | P1-Q13 (ideally inside the clinic system) |
| NFR-20 | Data licensing | Sources and licences are shown in the interface and the thesis (DDInter 2.0 CC BY-NC-SA 4.0, public FDA labels); the project is non-commercial. | Must | Legal |
| NFR-21 | Synthetic data | The demonstration database is generated by the team's own scripts from a fixed random seed and is documented. No real personal data are used at any stage. | Must | Project decision |
| NFR-22 | Reminder timing | Telegram reminders are delivered within 60 seconds of the scheduled time in a simulated run. | Should | P1-Q14 |

## Out of scope

- Import of data through the product; the team generates the synthetic database with its own scripts.
- Administrator access to personal or clinical data, database management, rule editing in the interface.
- Researcher role.
- Real patient data, link to a production clinic information system or national registries.
- Prescribing, diagnosis or treatment choice by the system; the decision belongs to the doctor.
- Dose calculation, pharmacokinetics, pregnancy-specific and paediatric rules.
- Payments, insurance, e-prescription with legal force, video consultation, laboratory or imaging analysis, voice dictation.
- Clinical-outcome study; the evaluation is technical.
