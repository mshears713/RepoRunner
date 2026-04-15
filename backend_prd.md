# Repo Viability Scanner Backend PRD

## Purpose
The purpose of the Repo Viability Scanner backend is to provide a robust system for evaluating the runnability of GitHub repositories in a sandbox environment. This backend will handle request validation, manage sandbox environments, execute repository code, and return execution results to the frontend.

## Responsibilities
- Validate incoming requests from the frontend.
- Manage the setup and teardown of sandbox environments.
- Execute repository code within these environments.
- Analyze execution results and generate explanations.
- Return structured JSON responses to the frontend.

## Integration Contract (From Main PRD — Do Not Change Without Updating Main PRD)
### Core Entities
- **Repository:** A GitHub repository URL and associated metadata for evaluation.
- **Sandbox Environment:** An isolated execution space for running repository code.
- **Execution Result:** The outcome of running the repository, including success or failure status and explanations.
- **Runnable Preview:** A generated preview if the repository execution is successful.

### API Contract
| Method | Path | Purpose | Input (high-level) | Output (high-level) |
|--------|------|---------|--------------------|---------------------|
| POST   | /api/evaluate | Evaluate repository viability | Repository URL, metadata | JSON with success/failure status, explanations |


## Architecture
The backend is built using Node/Express, responsible for handling HTTP requests, validating inputs, and coordinating the execution flow across various components like the Execution Engine and Result Analyzer. It interacts with a sandbox environment to ensure isolated execution of repository code.

## Endpoints (Must match API Contract)
| Method | Path | Purpose | Input (high-level) | Output (high-level) |
|--------|------|---------|--------------------|---------------------|
| POST   | /api/evaluate | Evaluate repository viability | Repository URL, metadata | JSON with success/failure status, explanations |


## Data / Models
- **Repository Model:** Captures the repository URL and metadata for processing.
- **Execution Result Model:** Stores the outcome of the execution, including status and explanations.

## External Integrations
- **Sandbox Environment Manager:** Responsible for creating isolated environments to run repository code.
- **Execution Engine:** Executes the repository code within the sandbox.
- **Result Analyzer:** Analyzes the execution logs and determines the viability of the repository.

## Validation / Error Handling
- Ensure all incoming requests have valid repository URLs and necessary metadata.
- Handle errors from sandbox setup and execution gracefully, providing meaningful feedback to the user.
- Implement timeout mechanisms for execution attempts to prevent indefinite hangs.

## Testing Strategy
- Unit tests for request validation and error handling.
- Integration tests for end-to-end request processing through the sandbox and execution engine.
- Mock external integrations to test backend logic in isolation.

## Out of Scope
- Frontend development and UI/UX design.
- Persistent data storage or database integration.
- Detailed analysis of repository code beyond execution viability.

## Implementation Phases

### Phase 1 — Backend skeleton and contracts
- Set up Node/Express server with the basic structure.
- Implement the `/api/evaluate` endpoint with a placeholder response.
- Acceptance: Server responds to `POST /api/evaluate` with a 200 status and a basic JSON object.

### Phase 2 — Core request flow and business logic
- Implement request validation logic for repository URLs and metadata.
- Integrate with the Sandbox Environment Manager to initiate environments.
- Acceptance: Valid requests trigger sandbox setup, and invalid requests return a 400 error.

### Phase 3 — External integrations and data handling
- Integrate the Execution Engine to run repository code within the sandbox.
- Implement the Result Analyzer to interpret execution outcomes.
- Acceptance: Execution attempts return a JSON response with success/failure status and explanations.

### Phase 4 — Validation, tests, and polish
- Implement comprehensive error handling and logging.
- Develop unit and integration tests to cover all critical paths.
- Acceptance: All tests pass, and the system handles edge cases gracefully, providing clear user feedback.
