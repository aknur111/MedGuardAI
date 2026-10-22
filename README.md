
# MedSafe

## Project Title
Development of an Intelligent System for Medication Safety Assessment Based on Patient Medical History

## Overview
MedSafe is a planned intelligent clinical decision-support system designed to assess potential medication-safety risks based on structured and unstructured patient medical history.

## Problem Statement
Medication-safety assessment requires considering current medications, allergies, chronic conditions, and other relevant patient information. MedSafe aims to support this process by integrating structured medical data, NLP-based extraction, rule-based safety checks, and evidence-linked explanations.

## Target Users
- Physicians
- Patients
- Clinical administrators
- Researchers

## Expected Outcomes
- Web-based clinical decision-support prototype
- Medication safety rule engine
- NLP extraction of medical history
- Evidence-grounded explanations
- Physician-approved medication schedules
- Technical evaluation using synthetic data

## Team
- Yertay Altynay Talgatkyzy — ML Engineer (lead), Research Head, Backend Developer, Frontend Developer
- Salemkan Aknur Seitkankyzy — Head of Backend, DevOps, Business Analyst, UI/UX Designer, ML Developer
- Nuraly Nuray Bakytzhankyzy — Project Manager, Head of Frontend, QA Engineer, ML Developer

## Supervisor
Orazova Arailym Zhanbolatkyzy

## Project Scope
The prototype will use synthetic adult patient data and focus on four selected medication groups. It will not use real patient data, autonomously prescribe medications, or integrate with production hospital systems.

## Planned Technology Stack
- Frontend: React, Next.js, TypeScript
- Backend: Python, FastAPI
- Database: PostgreSQL, pgvector
- AI/NLP: Locally hosted open-weight LLM, RAG
- Drug information: RxNorm, DDInter 2.0, FDA labels
- Background jobs: Celery, Redis
- Deployment: Docker Compose

## Current Status
Analysis and design phase. Technical architecture and implementation plans are under review.

## Documentation
See the `docs/` directory for the project proposal, literature review, system comparison, technology comparison, requirements, and evaluation plan.

## Project Management
YouTrack: https://medguard.youtrack.cloud/projects/MED

## Setup and Testing
The application is not yet runnable. Setup and testing instructions will be added when implementation becomes available.
