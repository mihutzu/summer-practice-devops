**GitHub Workflow Cheatsheet**

1. **Creating a Workflow File:**
   - Navigate to the repository where you want to create the workflow file.
   - Go to the `.github/workflows` directory.
   - Create a new file with a `.yml` extension (e.g., `my_workflow.yml`).

2. **Defining a Workflow:**
   - Use the `name` key to give your workflow a descriptive name.
   - Use the `on` key to specify the events that trigger the workflow.
   - Use the `jobs` key to define the jobs that run in parallel.

3. **Defining Jobs:**
   - Use the `name` key to give your job a descriptive name.
   - Use the `runs-on` key to specify the type of runner environment (e.g., `ubuntu-latest`, `macos-latest`, `windows-latest`).
   - Use the `steps` key to define the sequence of steps in your job.

4. **Defining Steps:**
   - Each step is an individual task within a job.
   - Use the `name` key to give your step a descriptive name.
   - Use the `run` key to specify the shell commands or script to execute.

5. **Using Actions:**
   - Actions are reusable tasks defined in separate repositories.
   - Use the `uses` key to reference an action's repository and version.
   - Specify the action's inputs and outputs as needed.

6. **Example Workflow File:**

```yaml
name: My Workflow

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  build:
    name: Build and Test
    runs-on: ubuntu-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Build
        run: |
          npm install
          npm run build

      - name: Test
        run: npm run test
```
