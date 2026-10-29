# 🏠 Dwell

### Your home. Your rights. Your next step.

**An AI-powered housing issue companion for non-native English-speaking tenants in New York City.**

Built for the **Nebius × NVIDIA Global AI Hackathon**.

---

## ✍️ Introduction & Overview

- **Service Name:** Dwell
- **Project:** Nebius × NVIDIA Global AI Hackathon
- **Target Users:** Non-native English-speaking tenants in New York City
- **Platforms:** Android & Web
- **Demo:** To be added

### 🔗 Repository

| Part | Repository |
| --- | --- |
| Frontend | [Dwell-FE](https://github.com/NebiusXNVIDIA-Global-AI-Hackathon/Dwell-FE) |
| Backend | [Dwell-BE](https://github.com/NebiusXNVIDIA-Global-AI-Hackathon/Dwell-BE) |

---


## 📌 Project Introduction

**Dwell** helps tenants turn a confusing housing problem into a documented, manageable case. From collecting evidence to understanding the next step, the platform brings housing issue reporting, AI-assisted guidance, and progress tracking into one experience.

The product focuses on tenants in **New York City**, particularly those navigating housing issues in a language that is not their first.


---

## 🖼️ Service Overview

<img width="3200" height="1800" alt="Dwell Service Overview" src="https://github.com/user-attachments/assets/31b4d46c-25d2-4118-84d9-5bd8d9b0ba83" />
<img width="3200" height="1800" alt="image" src="https://github.com/user-attachments/assets/28e11e98-178d-4b38-b810-4ab84387b722" />


## 🧭 User Journey

<img width="3200" height="1800" alt="Dwell User Journey" src="https://github.com/user-attachments/assets/b1cb04e0-71ab-4a71-9612-c2092585dac6" />

### 📝 MVP 1 — Case Creation & Evidence Collection
<img width="3200" height="1800" alt="image" src="https://github.com/user-attachments/assets/a16135a0-88ee-43ae-9e2a-13b616749fd4" />

### 🤖 MVP 2 — AI Evidence Analysis
<img width="3200" height="1800" alt="image" src="https://github.com/user-attachments/assets/a5ce15f2-49ce-46db-a911-7abb737e15b6" />
### 📊 MVP 3 — Case Management & Tracking
<img width="3200" height="1800" alt="image" src="https://github.com/user-attachments/assets/8d41b888-6372-4f2e-b8a7-9fe0ec0c1900" />

### 💬 AI Assistant
<img width="3200" height="1800" alt="image" src="https://github.com/user-attachments/assets/1a12b720-84fb-4bf6-947b-150ab098c6f1" />



---

## ❗ The Problem

When a tenant discovers mold, a leak, broken heating, or another housing issue, taking action is rarely as simple as submitting a complaint.

- **Documentation is difficult.** Photos, messages, and incident details become scattered across devices and conversations.
- **The process is unclear.** Tenants may not know what evidence matters or what to do next.
- **Language adds friction.** Understanding housing terminology and communicating with a landlord can be intimidating.
- **Follow-up is easy to lose.** Deadlines, responses, inspections, and repair outcomes need to be tracked over time.

## 💡 Our Solution

Dwell combines **structured case creation**, **AI-assisted evidence analysis**, and **guided follow-up** in a single tenant-centered workflow.

```text
Housing issue detected
        ↓
Create a case and describe the problem
        ↓
Add supporting evidence
        ↓
AI-assisted analysis and case summary
        ↓
Review suggested actions and checklists
        ↓
Track updates, landlord communication, and repair progress
```

## ✨ Key Features

| Feature | What it helps tenants do |
| --- | --- |
| 📝 **Guided Case Creation** | Record the issue type, location, affected area, description, and evidence through a step-by-step flow. |
| 📷 **Evidence Collection** | Attach supporting materials, including images, video, audio, and documents, to a case. |
| 🧠 **AI-Assisted Analysis** | Turn submitted case information and evidence into structured observations and assessments for review. |
| 📂 **Reports & Case History** | Browse cases and inspect case details, statuses, timelines, and supporting evidence. |
| ✅ **Action Checklists** | Organize recommended next steps and monitor progress as a case evolves. |
| 💬 **AI Assistant** | Access case-related conversations, contextual guidance, and suggested actions. |
| 🏢 **My Place** | View place-related information and building signals in a dedicated workspace. |
| ✉️ **Landlord Communication** | Support notice preparation and track communications related to an issue. |
| 🔧 **Repair Verification** | Document and review the outcome of a reported repair. |
| 🤝 **Community** | Explore tenant discussions and shared experiences. |

> Features represent workflows and modules present in the project repositories. Availability and end-to-end integration may vary by build.

## 🤖 AI Workflow

Dwell uses AI as an **assistance layer**, while keeping the case record and user actions structured within the application.

1. **Collect context** — the tenant describes the issue and supplies relevant evidence.
2. **Analyze evidence** — backend services process evidence-related observations, quality checks, and severity assessment.
3. **Structure the case** — the application organizes findings into case information and summaries.
4. **Suggest next steps** — assistant conversations and checklist services help users understand possible follow-up actions.
5. **Keep the record** — case events, notices, and verification information support ongoing tracking.

**AI infrastructure and components identified in the backend:**

- **NVIDIA Nemotron via Nebius Token Factory** for language-model integration.
- **Nebius AI Cloud** as part of the project's infrastructure stack.
- A dedicated **Gemini inspector client** for vision-oriented inspection functionality.
- A legal-document domain with vector-compatible persistence for contextual legal information.

AI output is intended to assist documentation and decision-making, **not replace professional legal advice or an official inspection**.

## 🏗 Architecture

```mermaid
flowchart TD
    U["Tenant · Android / Web"] --> FE["Flutter / Dart Frontend"]
    FE --> API["Spring Boot REST API"]
    API --> AUTH["JWT Authentication"]
    API --> CASE["Cases / Evidence / Follow-up"]
    API --> ASSIST["AI Assistant / Analysis"]
    API --> PLACE["Building / Community"]
    CASE --> DB[("PostgreSQL")]
    PLACE --> DB
    ASSIST --> DB
    ASSIST --> LLM["Nebius Token Factory · NVIDIA Nemotron"]
    ASSIST --> VISION["Gemini Inspector Client"]
    API --> FILES["Object Storage · AWS S3 SDK"]
```

*High-level architecture based on the repository structure and declared dependencies; it does not guarantee that every integration is active in every environment.*

## 🎬 Demo

The project targets **Android APK and Web** experiences.

- **Live Demo:** Link to be added
- **Demo Video:** Link to be added
- **Android APK:** Link to be added

## 👥 Team Members


### Design & Frontend

<table>
  <tr>
    <td width="160">
      <a href="https://github.com/SoWho-J">
        <img src="https://github.com/SoWho-J.png" width="100" alt="SoWho-J GitHub profile"/>
        <br/><b>SoWho-J</b>
      </a>
      <br/><sub>Design &amp; Frontend</sub>
    </td>
  </tr>
</table>

### Frontend

<table>
  <tr>
    <td width="160">
      <a href="https://github.com/hxx-dev">
        <img src="https://github.com/hxx-dev.png" width="100" alt="hxx-dev GitHub profile"/>
        <br/><b>hxx-dev</b>
      </a>
      <br/><sub>Frontend</sub>
    </td>
    <td width="160">
      <a href="https://github.com/seungminng123">
        <img src="https://github.com/seungminng123.png" width="100" alt="seungminng123 GitHub profile"/>
        <br/><b>seungminng123</b>
      </a>
      <br/><sub>Frontend</sub>
    </td>
  </tr>
</table>

### Backend

<table>
  <tr>
    <td width="160">
      <a href="https://github.com/wjdah1028">
        <img src="https://github.com/wjdah1028.png" width="100" alt="wjdah1028 GitHub profile"/>
        <br/><b>wjdah1028</b>
      </a>
      <br/><sub>Backend</sub>
    </td>
    <td width="160">
      <a href="https://github.com/minho0805">
        <img src="https://github.com/minho0805.png" width="100" alt="minho0805 GitHub profile"/>
        <br/><b>minho0805</b>
      </a>
      <br/><sub>Backend</sub>
    </td>
    <td width="160">
      <a href="https://github.com/eunhasu03">
        <img src="https://github.com/eunhasu03.png" width="100" alt="eunhasu03 GitHub profile"/>
        <br/><b>eunhasu03</b>
      </a>
      <br/><sub>Backend</sub>
    </td>
  </tr>
</table>


## 🛠 Tech Stack

### Frontend

![Flutter](https://img.shields.io/badge/Flutter-02569B?style=for-the-badge&logoColor=white&logo=flutter)
![Dart](https://img.shields.io/badge/Dart-0175C2?style=for-the-badge&logoColor=white&logo=dart)
![Material UI](https://img.shields.io/badge/Material_UI-243B53?style=for-the-badge&logoColor=white)

### Navigation & State

![go router](https://img.shields.io/badge/go_router-02569B?style=for-the-badge&logoColor=white)
![Riverpod](https://img.shields.io/badge/Riverpod-0553B1?style=for-the-badge&logoColor=white)
![fquery](https://img.shields.io/badge/fquery-243B53?style=for-the-badge&logoColor=white)
![Dio](https://img.shields.io/badge/Dio-0A66C2?style=for-the-badge&logoColor=white)

### Backend

![Java 21](https://img.shields.io/badge/Java_21-ED8B00?style=for-the-badge&logoColor=white&logo=openjdk)
![Spring Boot 4](https://img.shields.io/badge/Spring_Boot_4-6DB33F?style=for-the-badge&logoColor=white&logo=springboot)
![Spring Security](https://img.shields.io/badge/Spring_Security-6DB33F?style=for-the-badge&logoColor=white&logo=springsecurity)
![JPA](https://img.shields.io/badge/JPA-59666C?style=for-the-badge&logoColor=white)

### Database

![PostgreSQL](https://img.shields.io/badge/PostgreSQL-4169E1?style=for-the-badge&logoColor=white&logo=postgresql)
![Flyway](https://img.shields.io/badge/Flyway-CC0200?style=for-the-badge&logoColor=white&logo=flyway)
![Hibernate Vector](https://img.shields.io/badge/Hibernate_Vector-59666C?style=for-the-badge&logoColor=white&logo=hibernate)

### AI

![NVIDIA Nemotron](https://img.shields.io/badge/NVIDIA_Nemotron-76B900?style=for-the-badge&logoColor=white&logo=nvidia)
![Nebius Token Factory](https://img.shields.io/badge/Nebius_Token_Factory-243B53?style=for-the-badge&logoColor=white)
![Gemini](https://img.shields.io/badge/Gemini-8E75B2?style=for-the-badge&logoColor=white&logo=googlegemini)

### Infrastructure & Tools

![Docker](https://img.shields.io/badge/Docker-2496ED?style=for-the-badge&logoColor=white&logo=docker)
![GitHub Actions](https://img.shields.io/badge/GitHub_Actions-2088FF?style=for-the-badge&logoColor=white&logo=githubactions)
![Nebius AI Cloud](https://img.shields.io/badge/Nebius_AI_Cloud-243B53?style=for-the-badge&logoColor=white)
![AWS S3](https://img.shields.io/badge/AWS_S3-569A31?style=for-the-badge&logoColor=white&logo=amazons3)
![Swagger](https://img.shields.io/badge/Swagger-85EA2D?style=for-the-badge&logoColor=white&logo=swagger)

---
