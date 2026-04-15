# Repo Viability Scanner Frontend PRD

## Purpose
Enable developers to quickly assess the runnability of GitHub repositories by providing a user interface for submitting repository URLs and displaying execution results.

## Responsibilities
- Collect repository URL and metadata from the user.
- Display the execution status and explanations.
- Provide a runnable preview if the execution is successful.

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


## Views / Screens
- **Home Screen:** Input form for repository URL and metadata.
- **Result Screen:** Displays execution status, explanations, and runnable preview if available.

## User Flow
1. User enters a GitHub repository URL and optional metadata on the Home Screen.
2. User submits the form to initiate the evaluation process.
3. The Result Screen displays the success or failure status, explanations, and a runnable preview if successful.

## Components
- **RepositoryInputForm:** Collects repository URL and metadata.
- **ResultDisplay:** Shows execution status, explanations, and runnable preview.

## State Model
- **Input State:** Stores the repository URL and metadata entered by the user.
- **Result State:** Holds the execution status, explanations, and preview data received from the API.

## API Usage (Must match API Contract)
| Method | Path | Purpose | Input (high-level) | Output (high-level) |
|--------|------|---------|--------------------|---------------------|
| POST   | /api/evaluate | Evaluate repository viability | Repository URL, metadata | JSON with success/failure status, explanations |


## UX / Loading / Error Handling
- Show a loading indicator while waiting for the API response.
- Display error messages for invalid inputs or failed executions.
- Provide a retry option on error.

## Out of Scope
- Detailed analysis of execution logs.
- Manual configuration of sandbox environments.
- Persistent storage of user inputs or results.

## Implementation Phases

### Phase 1 — App shell and primary flow
- Implement the basic structure of the app with routing between Home and Result screens.
- Develop the RepositoryInputForm component to capture user input.
- Acceptance: User can navigate between screens; form captures input.

### Phase 2 — API wiring and state handling
- Connect the form submission to the API endpoint to evaluate repositories.
- Implement state management for input and result data.
- Acceptance: Form submission triggers API call; results are stored and accessible.

### Phase 3 — Output rendering and UX polish
- Develop the ResultDisplay component to show execution status and explanations.
- Integrate loading indicators and basic error handling.
- Acceptance: Loading shows during API call; results and errors display correctly.

### Phase 4 — Edge handling and cleanup
- Enhance error messages and add retry functionality.
- Implement conditional rendering for runnable previews.
- Acceptance: Errors are informative; previews display when available; retry works.
