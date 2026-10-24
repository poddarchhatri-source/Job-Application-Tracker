<div align="center">

# 📌 Job-Application-Tracker

**Track every application. Never miss an interview. Keep all your documents in one place.**

<p>
  <img src="https://img.shields.io/badge/Next.js-000000?style=for-the-badge&logo=nextdotjs&logoColor=white" alt="Next.js" />
  <img src="https://img.shields.io/badge/React-20232A?style=for-the-badge&logo=react&logoColor=61DAFB" alt="React" />
  <img src="https://img.shields.io/badge/Tailwind_CSS-38B2AC?style=for-the-badge&logo=tailwind-css&logoColor=white" alt="Tailwind CSS" />
  <img src="https://img.shields.io/badge/Prisma-2D3748?style=for-the-badge&logo=prisma&logoColor=white" alt="Prisma" />
  <img src="https://img.shields.io/badge/PostgreSQL-316192?style=for-the-badge&logo=postgresql&logoColor=white" alt="PostgreSQL" />
  <img src="https://img.shields.io/badge/Vercel-000000?style=for-the-badge&logo=vercel&logoColor=white" alt="Vercel" />
</p>

<p>
  <img src="https://img.shields.io/github/license/your-username/Job-Application-Tracker?style=flat-square" alt="License" />
  <img src="https://img.shields.io/github/stars/your-username/Job-Application-Tracker?style=flat-square" alt="Stars" />
  <img src="https://img.shields.io/github/forks/your-username/Job-Application-Tracker?style=flat-square" alt="Forks" />
  <img src="https://img.shields.io/github/issues/your-username/Job-Application-Tracker?style=flat-square" alt="Issues" />
  <img src="https://img.shields.io/badge/PRs-welcome-brightgreen?style=flat-square" alt="PRs Welcome" />
</p>

<p>
  <a href="#-features">Features</a> •
  <a href="#-tech-stack">Tech Stack</a> •
  <a href="#-architecture">Architecture</a> •
  <a href="#-getting-started">Getting Started</a> •
  <a href="#-contributing">Contributing</a> •
  <a href="#-author">Author</a>
</p>

### DashBoard
![Screenshot](docs/screenshots/jobtracker.png)

</div>

---

## 📖 About

**Job-Application-Tracker** is a web application designed to help users manage and organize their job search. It provides features for tracking application status, scheduling interviews, managing documents, and receiving notifications — all in one clean dashboard.

---

## ✨ Features

### 🗂️ Job Application Tracking
| Stage | Description |
|---|---|
| 🔖 **Bookmarked** | Jobs you're interested in but haven't applied to yet |
| 📨 **Applied** | Applications you've submitted |
| 📅 **Interview Scheduled** | Jobs where you've secured an interview |
| 🎉 **Got Offer** | Offers you've received |

### 🎤 Interview Management
- **Scheduled Interviews:** Keep track of interviews you've scheduled.
- **Notifications:** Get alerts about upcoming interview dates.
- **Conflicts:** Detect and resolve overlapping interview schedules.

### 📄 Document Management
- **Uploaded Documents:** Store and manage resumes, cover letters, portfolios, and other relevant files.

### 🔐 Authentication
- Email sign-in and OAuth (GitHub & Google) powered by NextAuth.

---

## 🛠️ Tech Stack

<table>
  <tr>
    <th>Category</th>
    <th>Technology</th>
  </tr>
  <tr>
    <td><b>Frontend</b></td>
    <td>
      <img src="https://skillicons.dev/icons?i=nextjs,react,tailwind" alt="Next.js, React, Tailwind" /><br/>
      <img src="https://img.shields.io/badge/Lucide_Icons-F56040?style=flat-square&logo=lucide&logoColor=white" alt="Lucide" />
    </td>
  </tr>
  <tr>
    <td><b>Backend</b></td>
    <td>
      <img src="https://skillicons.dev/icons?i=nextjs,prisma" alt="Next.js, Prisma" /><br/>
      <img src="https://img.shields.io/badge/NextAuth.js-purple?style=flat-square&logo=nextdotjs&logoColor=white" alt="NextAuth" />
    </td>
  </tr>
  <tr>
    <td><b>Database</b></td>
    <td><img src="https://skillicons.dev/icons?i=postgres" alt="PostgreSQL" /></td>
  </tr>
  <tr>
    <td><b>Document Management</b></td>
    <td><img src="https://img.shields.io/badge/UploadThing-E11D48?style=flat-square&logo=icloud&logoColor=white" alt="UploadThing" /></td>
  </tr>
  <tr>
    <td><b>State Management</b></td>
    <td><img src="https://img.shields.io/badge/Zustand-443E38?style=flat-square&logo=react&logoColor=white" alt="Zustand" /></td>
  </tr>
  <tr>
    <td><b>Editor</b></td>
    <td><img src="https://img.shields.io/badge/Novel-000000?style=flat-square&logo=markdown&logoColor=white" alt="Novel" /></td>
  </tr>
  <tr>
    <td><b>Authentication</b></td>
    <td>
      <img src="https://skillicons.dev/icons?i=github,google" alt="GitHub, Google OAuth" /><br/>
      Email + OAuth
    </td>
  </tr>
  <tr>
    <td><b>Deployment</b></td>
    <td><img src="https://skillicons.dev/icons?i=vercel" alt="Vercel" /></td>
  </tr>
</table>

---

## 🏗️ Architecture

### System Overview

```mermaid
flowchart TB
    User([👤 User])

    subgraph Client["🖥️ Frontend (Next.js + React)"]
        UI["UI Components<br/>Tailwind CSS + Lucide"]
        Store["Zustand Store<br/>(client state)"]
        Editor["Novel Editor<br/>(notes)"]
    end

    subgraph Server["⚙️ Backend (Next.js API / Server Actions)"]
        Auth["NextAuth<br/>(Email + OAuth)"]
        API["API Routes /<br/>Server Actions"]
        ORM["Prisma ORM"]
    end

    subgraph External["☁️ External Services"]
        DB[("🐘 PostgreSQL")]
        UT["📁 UploadThing<br/>(file storage)"]
        GH["GitHub OAuth"]
        GG["Google OAuth"]
    end

    User --> UI
    UI <--> Store
    UI --> Editor
    UI -->|requests| API
    UI -->|sign in| Auth
    Auth --> GH
    Auth --> GG
    Auth --> ORM
    API --> ORM
    ORM <--> DB
    API -->|upload / delete files| UT

    Vercel{{"▲ Deployed on Vercel"}}
    Client -.-> Vercel
    Server -.-> Vercel
```

### Application Status Flow

```mermaid
stateDiagram-v2
    [*] --> Bookmarked: Save a job
    Bookmarked --> Applied: Submit application
    Applied --> InterviewScheduled: Interview secured
    InterviewScheduled --> GotOffer: Offer received
    Applied --> Rejected: No response / rejected
    InterviewScheduled --> Rejected: Not selected
    GotOffer --> [*]
    Rejected --> [*]

    state "Interview Scheduled" as InterviewScheduled
    state "Got Offer" as GotOffer
```

### Authentication Flow

```mermaid
sequenceDiagram
    actor U as User
    participant App as Next.js App
    participant NA as NextAuth
    participant P as OAuth Provider<br/>(GitHub / Google)
    participant DB as PostgreSQL (Prisma)

    U->>App: Click "Sign in"
    App->>NA: Start auth flow
    NA->>P: Redirect for authorization
    P-->>NA: Return auth code / profile
    NA->>DB: Create or fetch user + session
    DB-->>NA: User record
    NA-->>App: Session established
    App-->>U: Redirect to dashboard
```

### Document Upload Flow

```mermaid
sequenceDiagram
    actor U as User
    participant UI as React UI
    participant UT as UploadThing
    participant API as Next.js API
    participant DB as PostgreSQL

    U->>UI: Select resume / cover letter
    UI->>UT: Upload file
    UT-->>UI: File URL + key
    UI->>API: Save document metadata
    API->>DB: Store URL, name, owner
    DB-->>API: Saved
    API-->>UI: Document listed in dashboard
```

---

## 🚀 Getting Started

### Prerequisites

- [Node.js](https://nodejs.org/) 18+
- A PostgreSQL database (local or hosted)
- GitHub / Google OAuth credentials (optional, for social login)
- An [UploadThing](https://uploadthing.com/) account

### Installation

1. **Clone the repository:**
    ```bash
    git clone https://github.com/your-username/Job-Application-Tracker
    ```

2. **Install dependencies:**
    ```bash
    cd Job-Application-Tracker
    npm install
    ```

3. **Set up environment variables:** Create a `.env` file in the project root and add the following:

    ```ini
    # Next Auth
    AUTH_SECRET=your_next_auth_secret_here
    AUTH_URL=https://your-auth-url.com

    # GitHub OAuth
    AUTH_GITHUB_ID=your_github_client_id_here
    AUTH_GITHUB_SECRET=your_github_client_secret_here

    # Google OAuth
    AUTH_GOOGLE_ID=your_google_client_id_here
    AUTH_GOOGLE_SECRET=your_google_client_secret_here

    # UploadThing
    UPLOADTHING_SECRET=your_uploadthing_secret_here
    UPLOADTHING_APP_ID=your_uploadthing_app_id_here

    # Database URL
    POSTGRES_PRISMA_URL=postgresql://user:password@localhost:5432/db
    POSTGRES_URL_NON_POOLING=postgresql://user:password@localhost:5432/db_non_pooling
    ```

4. **Set up the database:**
    ```bash
    npx prisma generate
    npx prisma db push
    ```

5. **Run the development server:**
    ```bash
    npm run dev
    ```

---

## 📘 Usage

1. Open the app at [http://localhost:3000](http://localhost:3000).
2. Create a new account or log in using OAuth.
3. Start adding job applications and moving them across stages.
4. Upload your resumes and cover letters in the Documents section.
5. Schedule interviews and watch for notifications and conflict alerts.

---

## 🗺️ Roadmap

- [ ] Email reminders for upcoming interviews
- [ ] Calendar sync (Google Calendar)
- [ ] Analytics dashboard (response rate, offer rate)
- [ ] Dark mode
- [ ] Browser extension to bookmark jobs in one click

---

## 🤝 Contributing

Contributions are welcome! Please follow these guidelines:

1. **Fork** the repository.
2. **Create** a new branch for your feature or bug fix:
    ```bash
    git checkout -b feature/your-feature-name
    ```
3. **Make** your changes and commit them:
    ```bash
    git commit -m "Add: your feature description"
    ```
4. **Push** your changes to your fork:
    ```bash
    git push origin feature/your-feature-name
    ```
5. **Open** a pull request to the `main` branch.

---

## 📄 License

This project is licensed under the [MIT License](LICENSE).

---

## 👨‍💻 Author

<div align="center">

**PRINCE KUMAR**

*Full-Stack Developer*

<a href="https://github.com/poddarchhatri-source"><img src="https://img.shields.io/badge/GitHub-181717?style=for-the-badge&logo=github&logoColor=white" alt="GitHub" /></a>
<a href="https://www.linkedin.com/in/prince-poddar-873327375/"><img src="https://img.shields.io/badge/LinkedIn-0A66C2?style=for-the-badge&logo=linkedin&logoColor=white" alt="LinkedIn" /></a>
<a href="mailto:poddarchhatri@gmail.com"><img src="https://img.shields.io/badge/Email-D14836?style=for-the-badge&logo=gmail&logoColor=white" alt="Email" /></a>

⭐ If you found this project helpful, please consider giving it a star!

</div>