# 🏠 Dwell

### Home repairs are hard enough. You shouldn’t have to navigate them alone.

**Your multilingual AI tenant agent—from the first repair request to checking the outcome.**

Dwell helps renters document evidence, communicate with landlords, and manage follow-ups. As new evidence and replies come in, your case stays organized and your next step stays clear.

Built for first-time renters and anyone navigating an unfamiliar housing system. Starting in New York City.

**Powered by NVIDIA Nemotron on Nebius Token Factory.**  
Built for the **Nebius × NVIDIA Global AI Hackathon**.

---

## 🏆 Hackathon Submission at a Glance

| | |
| --- | --- |
| 🏁 **Track** | Best Apps and Agents |
| 👥 **Target Users** | Non-native English-speaking tenants in New York City |
| 📱 **Platforms** | Android & Web |
| 🌐 **Live Demo** | **https://dwell-omega.vercel.app** (tap **"Try a demo account"**) |
| 🎬 **Demo Video (≤ 3 min)** | **https://youtu.be/R3j6sy3RzPQ** |
| 🟩 **NVIDIA Model** | NVIDIA Nemotron 3 Nano (`nvidia/NVIDIA-Nemotron-3-Nano-30B-A3B`), powering 7 features |
| ⚡ **Nebius** | Nebius Token Factory: every live Nemotron call is a runtime request to `api.tokenfactory.nebius.com/v1` |
| 💻 **Code** | [Dwell-FE](https://github.com/NebiusXNVIDIA-Global-AI-Hackathon/Dwell-FE) · [Dwell-BE](https://github.com/NebiusXNVIDIA-Global-AI-Hackathon/Dwell-BE) |
| 📜 **License** | Dwell is open source under the **[MIT License](https://github.com/NebiusXNVIDIA-Global-AI-Hackathon/Dwell-BE/blob/develop/LICENSE)**. © 2026 Dwell Team.<br/>Demo video evidence photo: "Ceiling water damage", Wikimedia Commons, [CC BY 3.0](https://creativecommons.org/licenses/by/3.0/). |
| 🗓 **Built** | From scratch during the Submission Period |

---

## 🧑‍⚖️ For Judges — Try Dwell in 3 Minutes

No installation or sign-up needed.

1. Open **https://dwell-omega.vercel.app** (best viewed in mobile view, e.g. 390 × 844, or on a phone).
2. On the login screen, tap **"Try a demo account"**.
3. Follow the path below. Each step is explained in [How it works](#-our-solution).

| Step | Tap | You'll see |
| --- | --- | --- |
| 1 | **Cases → + New Case** | Guided issue → room → spot selection |
| 2 | **Add Evidence → Check** | AI evidence check (3 items) |
| 3 | **Add a description → Submit** | Severity analysis, case created |
| 4 | **Home → View Case → View Case Analysis** | Severity reasons + NYC housing-code rights |
| 5 | **Send a notice → Open in Messages → Yes, I sent it** | Nemotron-drafted notice, response countdown (**Skip 24h** simulates time) |
| 6 | **Got a Reply? Update Status** | Deaver interprets the landlord's reply |
| 7 | **Upload an "after" photo** | Repair verification: Resolved / Disputed / Inconclusive |
| 8 | **Export** | PDF case report |
| 9 | **My Place** · **My Page → Manage Profile → Language** | Building signals, landlord record, community · English / 中文 / Español |

> The demo account is shared. Data you create there may be visible to other judges.
> Dwell's AI output helps tenants document and decide. It does **not** replace professional legal advice or an official inspection.

---

## 🟩 How We Use NVIDIA Nemotron & Nebius

> **A model that sees. A model that decides. A server that governs.**

```
Photo / video ──► Tuned Gemini (Vertex AI) ──► structured observation (JSON)
                                                        │
Renter's words + earlier photos + dates + case law ─────┤
                                                        ▼
                         NVIDIA Nemotron 3 Nano (Nebius Token Factory)
                                                        │  assessment + reasons (JSON)
                                                        ▼
                                  SeverityPolicy (rules enforced in code)
                                                        ▼
                                  Renter: severity, why, and the next step
```

### 🧠 NVIDIA Nemotron 3 Nano: the model that decides

We use **NVIDIA Nemotron 3 Nano** (`nvidia/NVIDIA-Nemotron-3-Nano-30B-A3B`) on **Nebius Token Factory** as Dwell's case agent. It powers **seven features**:

| Feature | What Nemotron does |
| --- | --- |
| ⚖️ **Severity judgment** | Weighs the Inspector's observations against the tenant's own words, earlier photos of the same spot, and the case history. Then it makes the final call. |
| 💬 **Deaver chat** | Multilingual assistant, streamed over SSE (`token → card → action → quick_replies → done`). |
| 🔔 **Case-event detection** | Recognizes commitments in landlord replies (e.g. *"I'll come by Friday"*) and moves the case forward. |
| 🔧 **Repair-verification explanations** | Explains before/after verdicts: **Resolved**, **Disputed**, or **Inconclusive**. |
| ✉️ **Landlord messages** | Formal English drafts with a translation in the tenant's language. |
| ✅ **Personalized checklists** | Next steps tailored to the case. |
| 📄 **Report narratives** | First-person summary for the exportable PDF case report. |

**Why Nano:** a tenant case is not a single prompt. Every new photo, chat message, and landlord reply triggers another call. The 30B-A3B MoE activates only about 3B parameters per token, so we could **call Nemotron on every case event instead of rationing it**, and stream to a phone. It followed our JSON schemas and case rules reliably. As an open model with inspectable reasoning, it also fits a tool whose decisions a tenant may show to a landlord or a housing agency.

**How we adapted it:** prompt and context engineering with code-enforced guardrails. **We did not fine-tune Nemotron.** For every call, the server builds a structured JSON context: vision observations, the tenant's description in their own language, earlier observations of the same spot, case stage and history, today's date, heating-season status, and the relevant legal entries. Each of the seven tasks has its own system prompt and output schema.

### ⚡ Where Nebius Token Factory accelerated our workflow

Every Nemotron feature is a **live runtime call** to `https://api.tokenfactory.nebius.com/v1`.

- **OpenAI-compatible API.** A small Java `HttpClient` in our Spring Boot backend calls `/v1/chat/completions` directly. No vendor SDK, no GPUs to operate.
- **Per-request reasoning control.** Thinking stays on for severity and case updates. It is turned off for writing via `chat_template_kwargs: {"enable_thinking": false}`, which cut report-narrative generation from **about 15–30 s to 2–5 s**. `reasoning_content` and `<think>` blocks are stripped, so users see only the final answer.
- **Streaming end to end.** The token stream feeds our SSE chat protocol, so tenants watch the answer form and then get structured cards and next actions.
- **Config-driven model routing.** `NEBIUS_MODEL` (chat) and `NEBIUS_JUDGE_MODEL` (severity judge) are environment variables, so we tested Nemotron variants per role without code changes. The deployed app uses Nano for both.
- **Pay-per-token pricing.** Tenant demand is bursty (heating complaints spike in winter), and we pay nothing for idle GPUs.

We also tried an **L40S GPU VM on Nebius AI Cloud** while exploring vision fine-tuning and self-hosted serving. We then chose hosted inference to avoid always-on GPU cost. Our Spring backend runs on AWS EC2 with evidence in S3. **Nebius provides all live Nemotron inference.**

### ⚖️ The server: rules a model cannot override

- **SeverityPolicy.** Nemotron may raise severity freely. It may lower it by **at most one level**, and only with a stated reason.
- **What cameras can't see.** Heat and hot-water outages in heating season are always High. Unclear photos return Inconclusive and trigger a retake, unless the renter describes danger.
- **Suggestions, not orders.** Response windows (High 24h / Medium 72h / Low 7 days) are proposed, and the renter confirms.
- **Law the model cannot invent.** The server selects relevant entries from **26 curated NYC/NYS housing-law provisions**. Citation labels and links are rendered **from our database, never from model output**.
- **Every decision has a receipt.** Each assessment is stored as JSON with its reason.
- **Designed to fail gracefully.** Every Nemotron call has a fallback (template text, default checklist, or Inconclusive).

### 👁️ Other models & tools

| Model / tool | Role |
| --- | --- |
| **Gemini 3.1 Flash-Lite**, fine-tuned on Google Vertex AI | The Inspector: visual observations, evidence quality checks, before/after repair comparison. Fine-tuned on **831 indoor ceiling/wall images** (706 train / 125 validation). |
| **GPT** | Dataset labeling support for the vision Inspector. |
| **Claude Code** (Anthropic) | Coding assistant for frontend development, plus demo video production and README documentation. |

Why two providers: Nemotron 3 Nano is a text model, and NVIDIA's vision models on Token Factory were available only as dedicated GPU deployments. We paired Nemotron with a per-token vision model and let the server pass structured data between them. **Nemotron never sees pixels.** It judges structured observations in the context of the whole case.

---

## ▶️ How to Run

### Prerequisites

| Tool | Version |
| --- | --- |
| Flutter | 3.47.x (team standard: 3.47.6) |
| Dart | ≥ 3.13.5 < 4.0.0 |
| Chrome | Latest (for Web) |
| Android SDK + Emulator or device | For Android |

```bash
flutter --version
flutter doctor
```

### 1. Clone & Install

```bash
git clone https://github.com/NebiusXNVIDIA-Global-AI-Hackathon/Dwell-FE.git
cd Dwell-FE
git switch develop
flutter pub get
```

### 2. Environment Setup

```bash
cp env/example.json env/dev.json
```

```json
{
  "APP_ENV": "dev",
  "API_BASE_URL": "https://api.mynokim.cloud",
  "DWELL_ENABLE_MOCK_EVIDENCE_CHECK": "true"
}
```

| Key | Description |
| --- | --- |
| `APP_ENV` | `dev` or `prod` |
| `API_BASE_URL` | Dwell API server URL |
| `DWELL_ENABLE_MOCK_EVIDENCE_CHECK` | `true` enables the demo evidence-check flow |

### 3. Run

**Web**

```bash
flutter run -d chrome --web-port=3000 --dart-define-from-file=env/dev.json
```

> ⚠️ The API server (CORS) only allows `localhost:3000` and `localhost:5173`. Always pass `--web-port=3000`.

**Android**

```bash
flutter devices
flutter run -d <device-id> --dart-define-from-file=env/dev.json
```

### 4. Production Build (Web)

```bash
flutter build web --release \
  --dart-define=APP_ENV=prod \
  --dart-define=API_BASE_URL=https://api.mynokim.cloud \
  --dart-define=DWELL_ENABLE_MOCK_EVIDENCE_CHECK=true
```

Output: `build/web` (deployed on Vercel. See `vercel.json`).

### Backend

See the [Dwell-BE README](https://github.com/NebiusXNVIDIA-Global-AI-Hackathon/Dwell-BE) for backend setup. AI features need `NEBIUS_API_KEY` (Nebius Token Factory). Optional settings are `NEBIUS_BASE_URL`, `NEBIUS_MODEL` (default `nvidia/NVIDIA-Nemotron-3-Nano-30B-A3B`), and `GEMINI_ENDPOINT_URL`. Without a key, the app falls back to template responses.

---

## 💬 Feedback on Nebius & NVIDIA

### Nebius Token Factory: 8/10

Compared with the GPU VM + vLLM setup we briefly tried, Token Factory removed all serving work: no CUDA setup, no cold starts, no idle cost. We called hosted inference from our backend and streamed responses directly into the app. That let our small team spend its time on case logic and safety rules instead of infrastructure.

**Friction we hit**

- Matching console display names to exact API model IDs.
- Some older documentation links (e.g., custom model deployment) returned 404.
- The console did not make it clear which models accept image or audio input.

**What we'd like to see**

1. Public per-token NVIDIA vision models (e.g., Nemotron Nano VL, Cosmos Reason). This would let us collapse our two-provider pipeline into one NVIDIA stack.
2. Self-service Nemotron adaptation (e.g., serverless LoRA adapters) that keeps usage-based hosted inference, so we could tune it on housing-case language without moving to a dedicated deployment.
3. A "copy model ID" button and clear input-modality labels in the console.
4. Documented JSON-schema enforcement (`response_format: json_schema`) that works together with reasoning mode, so apps don't need parse-and-fallback logic.
5. Per-request token usage and cost attribution by tag, so we could report cost per tenant case directly.

### NVIDIA Nemotron

We did not run a formal head-to-head benchmark on identical text tasks. After building with three model families, roles settled clearly: GPT supported dataset labeling, a fine-tuned Gemini handles vision, and Nemotron handles everything that requires judgment over case context. Its structured, rule-bound reasoning was reliable enough to sit behind our policy layer, and Nano-scale cost and latency let us call it on every case event. Where we would still reach for a frontier proprietary model is natural-sounding Korean.

**What we'd like to see from NVIDIA**

1. **A compact multimodal Nemotron on usage-based hosted inference.** One model that reads housing evidence alongside the tenant's words and case history would simplify our architecture. We would especially value its ability to tell visible improvement apart from evidence that actually supports a repair conclusion, and to say clearly when it cannot tell.
2. **Stronger multilingual fidelity, especially in Korean and Spanish.** A translation must preserve the difference between an acknowledgment, a tentative plan, and a firm repair commitment. That difference decides what a renter does next.
3. **Production guidance for combining reasoning controls with schema-constrained output,** including streaming examples and evaluation recipes.

### Nebius AI Cloud

We briefly ran an L40S GPU VM with vLLM while exploring vision fine-tuning and self-hosted serving. For a small team with bursty demand, hosted per-token inference on Token Factory was the better fit, so all live inference moved there.

---

## 🗓 Project Timeline

Dwell was **created from scratch during the Submission Period** (August 26 – October 30, 2026).
The Dwell-FE repository was created on **September 17, 2026**, and Dwell-BE on **October 8, 2026**. No part of the project existed before the hackathon.

---

## ❗ The Problem

The ceiling drips on Tuesday. You text the landlord. On Thursday: *"We'll look into it."*

Is that a promise? A date? A polite no? You read it three times in a language you're still learning, and you still don't know what to do next.

- **835,011** housing problems were reported to NYC HPD in FY2025.
- **7,500** of 20,000+ violations certified as "corrected" were found **false** on reinspection.
- **901** buildings stayed underheated for **seven winters** in a row.
- **23%** of New Yorkers (1.87M) speak English less than "very well".

For a first-time renter, the leak is never the hard part. **The case is.**

- **"Is this serious?"** Is a brown stain an emergency or cosmetic? Which photos will actually count?
- **"What do I say?"** Writing a formal repair request in English is hard. Decoding *"We'll look into it"* is harder.
- **"I asked. Now what?"** Nobody tells you how long to wait, or what to do when the landlord goes silent.
- **"Where's that photo?"** Evidence is in the camera roll, the promise is in a text thread, the 311 number is in a screenshot.
- **"Is it actually fixed?"** The landlord paints over the mold and calls it done. The leak is still there.

---

## 💡 Our Solution

Dwell turns a leak into **one living case**: every photo, every message, every deadline in one place, with **Deaver**, our multilingual AI assistant, telling you what to do next.

### How it works

1. **Report it in a few taps.** *Water & Flooding → Water Leak → Bathroom → Ceiling.* Dwell's guided flow captures exactly what's wrong and where.
2. **Capture evidence that holds up.** Dwell shows what good evidence looks like (overall view, close-up, video, surrounding area). Then AI checks every upload: **damage visible ✓ clear and steady ✓ surroundings included ✓**. Photos, video, voice notes, and documents are all accepted.
3. **Get a severity call, with reasons.** The Inspector reads the photo, and Nemotron weighs it against your own words. Example: *High: ceiling sagging and cracking, stain spreading, water dripping near a light.* Originals are saved, the AI analysis is attached, and the record is **protected from tampering**.
4. **Know your rights, with citations.** Case Analysis lists the NYC housing-code sections that apply (e.g. *§ 27-2005 Duties of owner*, *§ 27-2017.1 Mold remediation*), pulled from our legal database. Never invented by the model.
5. **Send a notice in seconds.** Nemotron drafts a polite, formal English message with your address, the problem, how long it's been going on, and a request for a repair date, plus a translation you can check. Review it, send it from your phone, and tap **"Yes, I sent it."**
6. **Watch the clock.** The case moves to **Waiting for landlord's response** with a countdown (e.g. *23 hours left*) and a fresh checklist for while you wait.
7. **Decode the reply.** Paste *"We will look into it."* Deaver flags it as **vague, not a commitment**, cites the owner's duty to repair, and offers one-tap next steps: *Ask for a written repair schedule · File with 311*.
8. **Prove the fix.** Upload an "after" photo. Dwell compares it with the "before" photo and returns **Resolved**, **Disputed**, or **Inconclusive**. A fresh coat of paint doesn't get a free pass.
9. **Export the whole story.** One tap creates a PDF with the timeline, evidence, correspondence, and the housing-law provisions that apply.

**Plus, beyond your unit:** **My Place** shows building-wide patterns (*4 water-leak cases in 30 days*), your landlord's track record (*53 days average to fix vs. 30 citywide · 1 open Class C violation*), and a **Neighbor Community** organized by floor. The whole app switches between **English, 中文, and Español** in one tap.

**One case. Every piece of evidence. Always a clear next step.**

---

## 🖼️ Service Overview

<img width="1920" height="1080" alt="표지" src="https://github.com/user-attachments/assets/a8590495-7fb3-4c07-8c53-f3458c0dc197" />
<img width="7680" height="4320" alt="persona" src="https://github.com/user-attachments/assets/07d8a16c-057e-4b37-9b10-eec580c4c512" />
<img width="7680" height="4320" alt="problem" src="https://github.com/user-attachments/assets/0d1f1df2-4de9-4568-952f-be7e1efdd312" />
<img width="7680" height="4320" alt="userflow" src="https://github.com/user-attachments/assets/885dcc13-6fcf-4ef7-85da-3417363d289e" />






### 📝 MVP 1 — Case Creation & Evidence Collection

<img width="7680" height="4320" alt="mvp1 - 케이스등록" src="https://github.com/user-attachments/assets/13f4a550-06c8-47ea-b236-e573bed1dee4" />


### 🤖 MVP 2 — AI Evidence Analysis
<img width="7680" height="4320" alt="mvp1- 케이스 디테일" src="https://github.com/user-attachments/assets/6dcf0586-d6b4-49ed-a917-9577dcbdb795" />

### 💬 MVP3  AI Assistant
<img width="7680" height="4320" alt="mvp 3- 채팅" src="https://github.com/user-attachments/assets/3160ec32-d3b6-431f-9429-a13d4a6db8a9" />

### 📊 MVP 4 — My Place
<img width="7680" height="4320" alt="mvp2 - my place" src="https://github.com/user-attachments/assets/e43337a6-f05f-4950-a72b-e7f15bfcff5a" />

---

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
    ASSIST --> VISION["Inspector · Fine-tuned Gemini (Vertex AI)"]
    API --> FILES["Object Storage · AWS S3 SDK"]
```

---

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

---

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
