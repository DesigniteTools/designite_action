# Designite action for C# projects

## What it does?
This action analyzes your C# code using [Designite](https://www.designite-tools.com/products-cs), detects a comprehensive set of architecture, design, and implementation smells, computes a large set of object-oriented code quality metrics, and uploads the results as an artifact.

## How to configure it?
Configuration for CI pipeline is a one-time process.

### Step 1. Obtain Personal access token and add it to GitHub secrets

- Create a new personal access token for your GitHub repository by navigating to your account’s user menu (top right) → Settings → Developer settings → Personal access tokens. Create a new token, and if using a fine-grained token, ensure read access to Actions, Code, and Metadata.
- Add the token to your repository’s secrets by going to the repository’s Settings → Secrets and variables → Actions. Create a new secret, paste the token into the Value field, and assign a meaningful name (e.g., PAT).

### Step 2 (Optional): Add your Designite license key to secrets
If you have a Designite **Professional** or **Academic** license key, add it to your repository’s GitHub secrets as `D_KEY`. This key enables the analysis of large projects.

### Step 3: Add a GitHub Actions workflow file

This is the last and very crucial step. Create a folder `.github` on your root directory of the project and create `workflows` folder inside the `.github` folder. Create a workflow file (say `actions.yml`) in the newly created `workflows` folder. The contents of the `action.yml` file depend upon your project language and tasks.

A sample action file is provided below.

```yaml
name: CI

on:
   push:
      branches: [ main ]
   pull_request:
      branches: [ main ]

jobs:
   analyze:
      runs-on: windows-latest
      steps:
      - name: DesigniteAction
        uses: DesigniteTools/designite_action@v1.0.0
        with:
            PAT: ${{ secrets.PAT }}
```

Change the version number of action.

## What you'll get
Once configured, your repository will be analyzed on each event defined in your workflow file (in the example above, the analysis runs on every push or pull request to the main branch). The resulting report will be stored as a GitHub Actions artifact, which you can download later to review detected code quality smells and metrics for deeper analysis.
