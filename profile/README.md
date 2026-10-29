<div align="center">

# 🏠 Dwell

### Your home. Your rights. Your next step.

**An AI-powered housing issue companion for non-native English-speaking tenants in New York City.**

Built for the **Nebius × NVIDIA Global AI Hackathon**.

[Frontend Repository](https://github.com/NebiusXNVIDIA-Global-AI-Hackathon/Dwell-FE) · [Backend Repository](https://github.com/NebiusXNVIDIA-Global-AI-Hackathon/Dwell-BE)

</div>

---

## 🌍 Overview

**Dwell** helps tenants turn a confusing housing problem into a documented, manageable case. From collecting evidence to understanding the next step, the platform brings housing issue reporting, AI-assisted guidance, and progress tracking into one experience.

The product focuses on tenants in **New York City**, particularly those navigating housing issues in a language that is not their first.

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

## 🛠 Tech Stack

| Area | Technologies |
| --- | --- |
| **Frontend** | Flutter, Dart, Material UI |
| **Navigation & State** | go_router, Riverpod, fquery |
| **Networking & Storage** | Dio, shared_preferences, flutter_secure_storage |
| **Media & UI** | camera, image_picker, video_player, flutter_svg, Lucide Icons |
| **Backend** | Java 21, Spring Boot 4, Spring Security, Spring Data JPA |
| **Database** | PostgreSQL, Flyway, Hibernate Vector |
| **Authentication** | JWT |
| **AI** | NVIDIA Nemotron, Nebius Token Factory, Gemini inspector integration |
| **Infrastructure & Tooling** | Docker, GitHub Actions, Nebius AI Cloud, AWS S3 SDK |
| **API Documentation** | OpenAPI / Swagger UI |

## 🎬 Demo

The project targets **Android APK and Web** experiences.

- **Live Demo:** Link to be added
- **Demo Video:** Link to be added
- **Android APK:** Link to be added

## 📱 Screenshots

Product screenshots will be added here. Suggested sequence: **Home → Create Case → Add Evidence → AI Analysis → Reports → Case Detail → Assistant**.

## 👥 Team

<div align="center">

### Frontend

<table><tr>
      <td align="center" width="160"><a href="https://github.com/hxx-dev"><img src="https://github.com/hxx-dev.png" width="100" style="border-radius:50%" alt="hxx-dev GitHub profile"/><br/><b>hxx-dev</b></a><br/><sub>Frontend</sub></td>
      <td align="center" width="160"><a href="https://github.com/SoWho-J"><img src="https://github.com/SoWho-J.png" width="100" style="border-radius:50%" alt="SoWho-J GitHub profile"/><br/><b>SoWho-J</b></a><br/><sub>Frontend</sub></td>
      <td align="center" width="160"><a href="https://github.com/seungminng123"><img src="https://github.com/seungminng123.png" width="100" style="border-radius:50%" alt="seungminng123 GitHub profile"/><br/><b>seungminng123</b></a><br/><sub>Frontend</sub></td>
</tr></table>

### Backend

<table><tr>
      <td align="center" width="160"><a href="https://github.com/wjdah1028"><img src="https://github.com/wjdah1028.png" width="100" style="border-radius:50%" alt="wjdah1028 GitHub profile"/><br/><b>wjdah1028</b></a><br/><sub>Backend</sub></td>
      <td align="center" width="160"><a href="https://github.com/minho0805"><img src="https://github.com/minho0805.png" width="100" style="border-radius:50%" alt="minho0805 GitHub profile"/><br/><b>minho0805</b></a><br/><sub>Backend</sub></td>
      <td align="center" width="160"><a href="https://github.com/eunhasu03"><img src="https://github.com/eunhasu03.png" width="100" style="border-radius:50%" alt="eunhasu03 GitHub profile"/><br/><b>eunhasu03</b></a><br/><sub>Backend</sub></td>
</tr></table>

</div>

## 🔗 Repositories

| Repository | Description |
| --- | --- |
| [**Dwell-FE**](https://github.com/NebiusXNVIDIA-Global-AI-Hackathon/Dwell-FE) | Flutter application for Android and Web, including tenant-facing workflows and UI. |
| [**Dwell-BE**](https://github.com/NebiusXNVIDIA-Global-AI-Hackathon/Dwell-BE) | Spring Boot API, case management, AI integration, authentication, and persistence. |

---

<div align="center">

**Dwell — turning housing concerns into clearer, actionable next steps.**

</div>
