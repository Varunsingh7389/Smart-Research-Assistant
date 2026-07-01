# Smart Research Assistant

An AI-powered research assistant backend built with **Java 21**, **Spring Boot 3**, and the **Gemini API**, designed to accept natural language research questions and return structured answers with summaries, key points, and follow-up questions.

> **Status:** Backend core is complete and functional (layered architecture, Gemini API integration, REST endpoints, database persistence, export). Frontend dashboard is in progress.

## Features

- Ask a research question and get a structured, AI-generated answer
- Auto-generated summary, key points, and follow-up questions per answer
- Conversations organized into research sessions with auto-generated titles and tags
- Search past conversations by keyword
- Mark conversations as favorites
- Export a conversation as PDF or Markdown
- Global exception handling with consistent JSON error responses
- Externalized configuration (API keys and DB credentials via environment variables)

## Tech Stack

| Layer        | Technology                          |
|--------------|--------------------------------------|
| Language     | Java 21                              |
| Framework    | Spring Boot 3 (Web, Data JPA, Validation, WebFlux) |
| AI           | Gemini API (Google AI)               |
| Database     | PostgreSQL / MySQL / H2 (for tests)  |
| Caching      | Redis (optional)                     |
| PDF export   | iText 7                              |
| Frontend     | HTML, CSS, JavaScript                |
| Build tool   | Maven                                |

## Architecture

The backend follows a standard layered architecture:

```
Controller  -> handles HTTP requests/responses
Service     -> business logic, Gemini API orchestration
Repository  -> Spring Data JPA data access
DTO         -> request/response contracts
Entity      -> JPA-mapped database models
Config      -> Gemini, WebClient, CORS, Redis configuration
Exception   -> centralized error handling
```

## Project Structure

```
smart-research-assistant/
├── backend/
│   ├── src/main/java/com/research/assistant/
│   │   ├── controller/      # REST controllers
│   │   ├── service/         # Business logic + Gemini integration
│   │   ├── repository/      # Spring Data JPA repositories
│   │   ├── dto/              # Request/response objects
│   │   ├── entity/           # JPA entities
│   │   ├── config/           # App configuration
│   │   └── exception/        # Global exception handling
│   ├── src/main/resources/
│   │   ├── application.properties
│   │   └── schema.sql
│   └── src/test/             # Unit tests
├── frontend/
│   ├── index.html
│   ├── css/style.css
│   └── js/ (api.js, ui.js, app.js)
└── README.md
```

## Getting Started

### Prerequisites

- Java 21+
- Maven 3.9+
- PostgreSQL (or MySQL) running locally, or use the H2 in-memory profile for quick testing
- A Gemini API key from [Google AI Studio](https://aistudio.google.com/)

### 1. Clone the repository

```bash
git clone https://github.com/Varunsingh7389/smart-research-assistant.git
cd smart-research-assistant
```

### 2. Set environment variables

```bash
export GEMINI_API_KEY=your_gemini_api_key
export DB_URL=jdbc:postgresql://localhost:5432/research_assistant
export DB_USERNAME=postgres
export DB_PASSWORD=your_db_password
```

### 3. Run the backend

```bash
cd backend
mvn spring-boot:run
```

The API will start on `http://localhost:8080`.

### 4. Open the frontend

Open `frontend/index.html` directly in a browser, or serve it with any static file server. It's configured to call the backend at `http://localhost:8080/api`.

## API Endpoints

| Method | Endpoint                              | Description                        |
|--------|-----------------------------------------|-------------------------------------|
| POST   | `/api/research/ask`                     | Ask a new research question         |
| GET    | `/api/conversations`                    | List all conversations              |
| GET    | `/api/conversations/{id}`               | Get a single conversation           |
| GET    | `/api/conversations/favorites`          | List favorite conversations         |
| GET    | `/api/conversations/search?keyword=`    | Search conversations by keyword     |
| PUT    | `/api/conversations/{id}/favorite`      | Toggle favorite status              |
| DELETE | `/api/conversations/{id}`               | Delete a conversation               |
| GET    | `/api/export/{id}/pdf`                  | Export a conversation as PDF        |
| GET    | `/api/export/{id}/markdown`             | Export a conversation as Markdown   |

## Running Tests

```bash
cd backend
mvn test
```

## Roadmap

- [ ] Wire up frontend dashboard to live backend
- [ ] Add user authentication
- [ ] Dockerize backend + database for one-command setup
- [ ] Add citation/source links to answers where available

## License

This project is for educational and portfolio purposes.
