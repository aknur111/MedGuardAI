# Interview P1: physician, Mediker clinic at Astana IT University

Task: MED-16. Section 2 of the project documentation (Evidence of relevance).

- **Participant:** P1, a practising physician of the Mediker clinic located at Astana IT University. Anonymous; the name is not recorded in this repository.
- **Method:** semi-structured interview, 15 open questions, about 30 to 40 minutes. Answers were written down by the interviewer and then read and confirmed by the physician.
- **Consent:** the physician signed an informed-consent form that allows anonymous use of the answers for academic purposes. The signed form is kept by the team and is not stored in the repository.
- **Date:** October 2026.

## Questions and answers (English)

### Q1. Where do you work and which patients do you see most often: age, chronic conditions, number of medications taken at the same time?

I work as a physician at the Mediker clinic based at Astana IT University. The main flow is students aged 17–25 and university staff. Students most often come with acute respiratory infections, gastritis, headaches, allergies, anxiety and sleep problems during exams, and sports injuries. Some have chronic conditions: bronchial asthma, atopic dermatitis, type 1 diabetes, epilepsy. Staff over 40 come with hypertension, type 2 diabetes and thyroid disorders. Students usually take 1–3 drugs; staff sometimes take 4–6.

### Q2. How do you prescribe treatment for a patient who is already taking several medications? Describe your steps from collecting the medical history to writing the prescription.

First I open the record in our clinic's information system and look at previous visits. Then I ask the patient what they take now, what was prescribed at the polyclinic where they are registered, and whether they have allergies or chronic conditions. With students I ask separately about antidepressants, acne medications, contraceptives and sports supplements, because they do not mention them on their own. Then I choose the drug according to the clinical protocol and check contraindications and compatibility with what is already being taken. I write the prescription and explain how and how much to take.

### Q3. Where do you get information about interactions and contraindications: Vidal, RLS, package inserts, Drugs.com, experience, colleagues, something in the medical information system?

Mostly package inserts and the Vidal reference book; for interactions more often Drugs.com or Medscape, because they have a convenient checker. Our clinic's information system has no automatic interaction check; it is mainly for recording visits and prescriptions. In complex cases I consult colleagues at the clinic or call a clinical pharmacologist at the main Mediker clinic.

### Q4. How much time does checking drug compatibility for one patient usually take? Do you do it every time or only in complex cases?

If there are two or three drugs, the check takes 3–5 minutes. For staff on 5–6 drugs it takes up to 10–15 minutes if every pair is checked. During the respiratory-infection season, with 25–30 visits a day, it is not possible to check everyone. I always check with chronic conditions, antidepressants and anticonvulsants, antibiotics, and when the patient already takes something from another doctor. In simple cases like a cold in a healthy student I rely on experience.

### Q5. Recall a case where a patient had a problem due to a drug combination, allergy, or comorbidity. How was it detected, and what could have helped earlier?

A student with chronic gastritis regularly took ibuprofen for headaches, which was not in the record. Elsewhere he was prescribed diclofenac for a knee injury, and a few days later he came in with abdominal pain and black stool; he had to be referred to hospital with suspected bleeding. There was also a case where a student with a penicillin allergy received amoxicillin, because the allergy was recorded only at the polyclinic where she is registered and was not in our record. Both cases were found only from complaints. It would help if a system could see all current drugs and allergies and warn at the time of prescribing.

### Q6. Which prescribing errors occur most often: interaction, allergy, contraindication by diagnosis, duplication of the active substance, wrong dosage?

Among students the most common is duplication: they take combined cold powders and paracetamol separately, or two NSAIDs under different names. Second are contraindications by diagnosis, for example NSAIDs with gastritis or some nasal decongestants with hypertension in staff. Allergy is rarer but more dangerous, especially to antibiotics. Dosing errors happen because of self-medication: the patient takes more than prescribed. Clinically significant interactions are rare in young people, but they do occur with antidepressants and anticonvulsants.

### Q7. How completely do you know what the patient actually takes, including drugs from other doctors, supplements and over-the-counter medicines?

Less than half. Students are registered at polyclinics at their place of residence or in another city, and I cannot see prescriptions from there. They buy a lot on their own at the pharmacy on the advice of friends or the internet: painkillers, sleeping pills, concentration aids during exams, protein and sports supplements, high-dose vitamins. They do not mention this unless asked directly. Staff usually know their drugs better, but do not always remember the names.

### Q8. In what form is the patient's medical history stored: paper, DamuMed or another system, free text, structured fields? How complete and up to date is it?

We have our own clinic information system, not DamuMed. Visit notes are mostly free text; there are fields for diagnosis and allergies, but they are not always filled in. The record contains only visits to our clinic, while the student's state polyclinic keeps its own record in DamuMed, and these data are not linked. Students bring certificates and discharge summaries on paper or as photos on their phone. So the history is incomplete, and I ask again at every visit.

### Q9. If a system warned you about a dangerous combination with the reason and source, would you trust it? What would it take for you to trust it?

Yes, if the warning comes with a clear reason and a link to the source: the package insert, a clinical protocol or a recognised interaction database. Without a source I would double-check myself, and then the system has no point. It is important that the system does not make basic mistakes and does not raise false alarms for every drug. Trust will come after I compare its warnings with the reference books several times and see that they match. The final decision must still remain with the physician.

### Q10. Which warnings would you want to see, and which would only get in the way? Have you experienced “alert fatigue” in existing systems?

I want to see dangerous interactions, allergies, contraindications by diagnosis and pregnancy, duplication of the active substance and dose exceedance. Warnings about minor interactions and pop-ups that must be closed for every drug get in the way. Our information system has no drug warnings, but it has mandatory fields and reminders that everyone closes without reading, so the effect is familiar. It needs to be split by risk level: red cannot be skipped, yellow can be reviewed if desired.

### Q11. What matters more to you: the system suggesting treatment options or only checking what you prescribed yourself?

Checking what I prescribed is more important. Treatment options are useful as a hint, especially with allergy or intolerance when a substitute is needed, but the prescribing must be done by me and according to the protocol. If the system imposes a treatment scheme, doctors will see it as control rather than help. A good option: I enter the prescription, the system checks it and, if there is a problem, suggests one or two safe alternatives with justification.

### Q12. What should the explanation of a warning look like so that you can decide quickly: risk level, link to the source, replacement recommendation?

One line: risk level in colour, which two drugs conflict and what the mechanism is, for example “increases the risk of gastric bleeding”. Below it a link to the source. Then what to do: stop, replace with a specific drug, or monitor a parameter. Everything should fit on one screen without scrolling. And there must be an “accept risk” button with a short comment, because sometimes the combination is deliberately justified.

### Q13. Where would it be convenient for you to work with such a system: inside the medical information system, a separate web application, a mobile application?

Ideally inside our clinic's information system, so the patient does not have to be entered a second time. I understand that integration is difficult, so at the first stage a web application where I can quickly paste the drug list, diagnoses and allergies or upload a discharge summary would be fine. A mobile version is convenient for a quick check of a pair of drugs, for example when a student asks in the corridor whether two medicines can be combined. For the main work at the appointment a computer is needed.

### Q14. How often do patients break the dosing schedule, and would a dosing schedule with reminders help? Would you want to see whether the patient follows the schedule?

Students break the schedule all the time: they stop an antibiotic on the third day when they feel better, miss doses because of classes and deadlines, take everything at once in the evening. A phone schedule with reminders would suit them perfectly, since they already live in apps. For older staff a printout is better. Seeing adherence would be useful, at least as a simple indicator before a follow-up visit, but without extra reporting for the doctor.

### Q15. What must such a system have for you to start using it, and what would stop you?

Must have: a database of drugs actually available in Kazakhstan's pharmacies with brand names in Russian, quick entry without retyping the history, an explanation of every warning with a source, fast performance within a few seconds, and account of allergies and chronic conditions. What would stop me: having to re-enter all patient data, many false warnings, unclear responsibility for a system error, and patient data leaving the clinic. For our students a dosing schedule with reminders would be a separate plus.
