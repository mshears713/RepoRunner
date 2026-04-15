# Repo Viability Scanner PRD

## Overview
The Repo Viability Scanner enables individual developers to rapidly assess the runnability of pre-filtered GitHub repositories in a sandbox environment without manual setup. The core value is to provide a quick and automated way to determine if a repository can be executed successfully, offering developers a runnable preview if viable.

## System Contract (Source of Truth)
- frontend_required: true

### 1. Core Entities
- **Repository:** A GitHub repository URL and associated metadata for evaluation.
- **Sandbox Environment:** An isolated execution space for running repository code.
- **Execution Result:** The outcome of running the repository, including success or failure status and explanations.
- **Runnable Preview:** A generated preview if the repository execution is successful.

### 2. API Contract
| Method | Path | Purpose | Input (high-level) | Output (high-level) |
|--------|------|---------|--------------------|---------------------|
| POST   | /api/evaluate | Evaluate repository viability | Repository URL, metadata | JSON with success/failure status, explanations |

### 3. Data Flow
1. User submits repository URL via React Frontend.
2. Request sent to Node/Express API for validation.
3. Validated request routed to Sandbox Environment Manager.
4. Sandbox Environment Manager spins up an isolated environment.
5. Execution Engine attempts to run the repository.
6. Result Analyzer determines success or failure and generates explanations.
7. If successful, Preview Generator creates a runnable preview.
8. Node/Express API returns JSON response with status and explanations to React Frontend.

### 4. Frontend / Backend Boundary
**Frontend Responsibilities**
- Collect repository URL and metadata from the user.
- Display success/failure status and explanations.
- Provide a runnable preview if available.

**Backend Responsibilities**
- Validate incoming requests.
- Manage sandbox environment setup.
- Execute repository code and analyze results.
- Generate and return JSON responses.

### 5. State Model (lightweight)
**Client State**
- User input data (repository URL, metadata).
- Displayed results (status, explanations, preview).

**Server State**
- Execution status and logs.
- Generated explanations and preview data.

## Architecture
The system is structured as a full-stack application with a React frontend and a Node/Express backend. The frontend collects user input and displays results, while the backend handles request validation, sandbox environment management, and execution logic. The Execution Engine runs repositories in isolated environments, and the Result Analyzer interprets outcomes to provide feedback. The Preview Generator creates runnable previews for successful executions.

## Components

### React Frontend
- **Responsibility:** Provides the user interface for developers to submit repository URLs and view results.
- **Interface:** Interacts with users and sends requests to the Node/Express API.
- **Key logic:** Collects input, displays results, and handles user interactions.

### Node/Express API
- **Responsibility:** Handles incoming requests, validates them, and routes them to the core logic.
- **Interface:** Exposes HTTP endpoints for frontend communication.
- **Key logic:** Validates requests, manages data flow to other components.

### Execution Engine
- **Responsibility:** Performs standardized execution attempts on the repositories within the sandbox.
- **Interface:** Receives execution requests from the Node/Express API.
- **Key logic:** Runs repository code and collects execution data.

### Result Analyzer
- **Responsibility:** Analyzes execution outcomes to determine success or failure and generates explanations.
- **Interface:** Processes data from the Execution Engine.
- **Key logic:** Interprets execution logs and determines viability.

### Preview Generator
- **Responsibility:** Creates a runnable preview if the repository execution is successful.
- **Interface:** Utilizes successful execution data to generate previews.
- **Key logic:** Constructs and returns a runnable preview.

## API Usage
No external APIs required.

## Database Design
No persistent storage required.

## Test Cases
| Test | Input | Expected Output | Type |
|------|-------|-----------------|------|
| Valid repository URL | Valid URL, metadata | Success status, explanations | integration |
| Invalid repository URL | Invalid URL | Error response | unit |
| Complex repository | Complex URL, metadata | Timeout or failure status | e2e |
| Successful execution | Valid URL, metadata | Success status, runnable preview | integration |
| Execution failure | Valid URL, metadata | Failure status, error explanations | unit |
| No metadata provided | URL only | Error response | unit |

## Implementation Notes for Build Agents
- This PRD is a coordination layer that downstream agents will use to generate `backend_prd.md` and `frontend_prd.md`.
- The **System Contract (Source of Truth)**, especially the **API Contract**, must NOT be changed downstream.
- Implementation phases will be defined separately in each downstream PRD.