# NPCstorage

[![License: MIT](https://img.shields.io/badge/License-MIT-yellow.svg)](https://opensource.org/licenses/MIT) <!-- Placeholder -->

A web-based application designed for Game Masters (GMs) of the 2nd edition of Warhammer Fantasy Roleplay (WHFRP) to streamline the process of creating and managing Non-Player Characters (NPCs). The primary language for the UI and core data is Polish.

## Table of Contents

- [Project Description](#project-description)
- [Tech Stack](#tech-stack)
- [Getting Started Locally](#getting-started-locally)
- [Available Scripts](#available-scripts)
- [Project Scope](#project-scope)
- [Project Status](#project-status)
- [License](#license)

## Project Description

NPCstorage aims to solve the time-consuming process of manually creating and managing NPC stats for Warhammer Fantasy Roleplay 2nd Edition. It allows GMs to:

- Manually create NPCs with full control over details.
- Randomly generate NPCs based on a specified Experience Point (XP) budget and WHFRP 2e rules.
- Automatically generate character descriptions using AI (Polish language).
- Edit any detail of existing NPCs.
- Store and persist NPCs linked to user accounts.
- View, sort, filter, and search their NPC list.
- Manage temporary statistical changes during gameplay.
- Import game data (Careers, Skills, Talents) from predefined CSV files.

The project focuses on providing a Minimum Viable Product (MVP) to address the core needs of WHFRP 2e GMs for NPC management during game preparation and sessions.

## Tech Stack

-   **Frontend:**
    -   [Astro 5](https://astro.build/)
    -   [React 19](https://react.dev/)
    -   [TypeScript 5](https://www.typescriptlang.org/)
    -   [Tailwind CSS 4](https://tailwindcss.com/)
    -   [shadcn/ui](https://ui.shadcn.com/)
-   **Backend:**
    -   [FastAPI](https://fastapi.tiangolo.com/) (Python)
    -   [PostgreSQL](https://www.postgresql.org/)
    -   [SQLAlchemy](https://www.sqlalchemy.org/)
    -   [Pydantic](https://docs.pydantic.dev/)
    -   Authentication: `python-jose`, `passlib`
    -   [Uvicorn](https://www.uvicorn.org/)
-   **AI Integration:**
    -   [OpenAI API](https://platform.openai.com/) (Utilizing models like GPT-4o-mini)
    -   [Langfuse](https://langfuse.com/) (LLM Observability)
-   **CI/CD & Hosting:**
    -   [GitHub Actions](https://github.com/features/actions)
    -   [Docker](https://www.docker.com/)
    -   [DigitalOcean](https://www.digitalocean.com/)

## Getting Started Locally

### Prerequisites

-   [Node.js](https://nodejs.org/) (LTS version recommended)
-   [npm](https://www.npmjs.com/) or [yarn](https://yarnpkg.com/)
-   [Python](https://www.python.org/) (3.8+ recommended)
-   [pip](https://pip.pypa.io/en/stable/)
-   [PostgreSQL](https://www.postgresql.org/download/) Server
-   [Docker](https://docs.docker.com/get-docker/) (Optional, can be used for PostgreSQL)
-   OpenAI API Key (Required for description generation)
-   Langfuse Credentials (Optional, for LLM observability)

### Backend Setup (`/backend`)

1.  **Clone the repository:**
    ```bash
    git clone <repository-url>
    cd <repository-folder>/backend
    ```
2.  **Create and activate a virtual environment:**
    ```bash
    python -m venv venv
    source venv/bin/activate  # On Windows use `venv\Scripts\activate`
    ```
3.  **Install dependencies:**
    ```bash
    pip install -r dependencies.txt
    ```
4.  **Set up PostgreSQL:**
    -   Ensure PostgreSQL server is running.
    -   Create a database for the application.
    -   Configure database connection details (see Environment Variables).
5.  **Configure Environment Variables:**
    -   Create a `.env` file in the `/backend` directory.
    -   Add necessary variables (exact names TBD, examples below):
        ```env
        DATABASE_URL=postgresql://user:password@host:port/database_name
        OPENAI_API_KEY=your_openai_api_key
        # LANGFUSE_SECRET_KEY=your_langfuse_secret
        # LANGFUSE_PUBLIC_KEY=your_langfuse_public
        # JWT_SECRET_KEY=your_strong_secret_key
        # ALGORITHM=HS256
        # ACCESS_TOKEN_EXPIRE_MINUTES=30
        ```
6.  **Run database migrations (if applicable):**
    *(Command depends on migration tool used, e.g., Alembic)*
    ```bash
    # alembic upgrade head  (Example)
    ```
7.  **Run the backend server:**
    ```bash
    uvicorn main:app --reload --host 0.0.0.0 --port 8000
    ```
    *(Assuming the entry point is `main.py` containing a FastAPI `app` instance)*

### Frontend Setup (`/frontend`)

1.  **Navigate to the frontend directory:**
    ```bash
    cd ../frontend
    ```
2.  **Install dependencies:**
    ```bash
    npm install
    # or
    # yarn install
    ```
3.  **Configure Environment Variables:**
    -   Create a `.env` file in the `/frontend` directory (if needed).
    -   Set the backend API URL (exact variable name TBD by Astro config):
        ```env
        # Example: Check Astro's environment variable handling
        PUBLIC_API_BASE_URL=http://localhost:8000
        ```
4.  **Run the frontend development server:**
    ```bash
    npm run dev
    # or
    # yarn dev
    ```
    The application should now be accessible, typically at `http://localhost:4321`.

## Available Scripts

### Backend (`/backend`)

-   `pip install -r dependencies.txt`: Installs Python dependencies.
-   `uvicorn main:app --reload`: Starts the FastAPI development server with auto-reload.

### Frontend (`/frontend`)

-   `npm run dev` or `yarn dev`: Starts the Astro development server.
-   `npm run build` or `yarn build`: Builds the application for production.
-   `npm run preview` or `yarn preview`: Serves the production build locally for preview.
-   `npm run astro` or `yarn astro`: Accesses the Astro CLI.

## Project Scope

### In Scope (MVP)

-   Full support for **Warhammer Fantasy Roleplay 2nd Edition** ruleset.
-   Manual and Random (XP-based) NPC creation.
-   Editing of all NPC attributes.
-   User account management (registration, login, password change, account deletion).
-   Persistent storage of NPCs per user.
-   NPC List View with sorting, filtering, and free-text search (Name, Race, Profession).
-   Temporary statistic modifier management.
-   Importing Career, Skill, and Talent data from CSV files (Polish).
-   LLM-based generation of NPC descriptions (Polish).
-   Error handling for CSV imports.

### Out of Scope (MVP)

-   Support for other RPG systems (e.g., WHFRP 4e, D&D).
-   Advanced NPC organization features (e.g., tags, folders).
-   NPC sharing between users.
-   Direct integration of game mechanics (e.g., automatic test calculations).
-   Automatic tracking of temporary effect durations.
-   Explicit NPC balancing tools (manual editing is possible).
-   Mobile application.

## Project Status

**Actively Developed**

The project is currently focused on delivering the Minimum Viable Product (MVP) features outlined in the scope.

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details (assuming MIT, link needs verification if a LICENSE file exists or is added). 