![logo_ironhack_blue 7](https://user-images.githubusercontent.com/23629340/40541063-a07a0a8a-601a-11e8-91b5-2f13e4e6b441.png)

# LAB | Setting Up a Complete CI/CD Pipeline Using GitHub Actions 🌐🚀

## Introduction

In this lab, you’ll create a fully automated **CI/CD pipeline** for a **Next.js** application using **GitHub Actions**. You’ll implement key stages such as building, testing, and deploying the application to a production environment.

<br>

## Requirements 📝

1. Clone this repo => [link](https://github.com/BH-webdev-devops/Lab-day13.git)
2. Create a new branch => lab/your_name
3. Complete the tasks below.

## Submission 📬

Once you finish the assignment, submit a URL link to your repository or your pull request in the field on Student Portal.

<br>

## Instructions

## Tasks 🛠️

### **Task 1: Initialize Your Project and GitHub Repository** 🌟

1. Clone the forked repository to your local machine.
2. Ensure you have a working **Next.js** application:
   - Run `npm install` to install dependencies.
   - Run `npm run dev` to start the development server.
3. Push your local code to the GitHub repository using the following commands:

```bash
git add .
git commit -m "Initial commit"
git push origin main
```
<br>

### Task 2: Set Up GitHub Actions Workflow 🤖
1. Create a `.github/workflows/ci-cd.yml` file in your repository.
2. Write a GitHub Actions workflow to:
- Install dependencies.
- Run unit tests using Jest.
- Deploy the application to Vercel or Netlify after successful tests.

**Example Workflow**:

```yaml
name: CI/CD Workflow

on:
  push:
    branches:
      - main
  pull_request:
    branches:
      - main

jobs:
  build-test:
    runs-on: ubuntu-latest
    steps:
      - name: Checkout code
        uses: actions/checkout@v2

      - name: Set up Node.js
        uses: actions/setup-node@v3
        with:
          node-version: '16'

      - name: Install dependencies
        run: npm install

      - name: Run tests
        run: npm test

  deploy:
    runs-on: ubuntu-latest
    needs: build-test
    steps:
      - name: Deploy to Vercel
        run: vercel --prod
        env:
          VERCEL_TOKEN: ${{ secrets.VERCEL_TOKEN }}
```

3. Add a Vercel deployment token or similar secret in GitHub:
Go to **Settings > Secrets and variables > Actions**.
Add a new secret named `VERCEL_TOKEN`.

<br>

### Task 3: Add Unit Tests ✅
1. Install Jest and React Testing Library:
```bash
npm install --save-dev jest @testing-library/react @testing-library/jest-dom
```
2. Add a __tests__ folder and create a test file for your Home page:
```typescript
// __tests__/index.test.tsx
import { render, screen } from '@testing-library/react';
import Home from '../pages/index';

test('renders the welcome message', () => {
  render(<Home />);
  expect(screen.getByText('Welcome to Next.js!')).toBeInTheDocument();
});
```

Ensure your tests pass by running:
`npm test`


4. Verify that the tests are triggered by your GitHub Actions workflow.


### Task 4: Deploy the Application 🌍
1. Push your changes to the main branch.
2. Confirm the application is deployed by visiting the URL provided by Vercel or Netlify.

<br>

## Bonus Tasks 🎁
1. **Add Linting**:
- Install ESLint: npm install eslint --save-dev
- Add linting to your workflow:
```yaml
- name: Run Lint
  run: npm run lint
```

2. **Add Staging Environment**:
Set up a `staging` branch with a separate deployment environment.

### Expected Outcome ✅
By the end of this lab, you should have:

- A fully functional CI/CD pipeline for your Next.js application.
- Automated tests that run on every push or pull request.
- A deployed application accessible via a public URL.


### Hints :bulb:
<details style="font-size: 14px; cursor: pointer; outline: none;">

- **Workflow Triggers**: Remember to specify the correct branches in your GitHub Actions workflow for triggering the pipeline. For example, use `main` for production and `staging` for testing.

- **Environment Variables**: Use GitHub secrets to securely store sensitive information like deployment tokens (e.g., `VERCEL_TOKEN`). Access these in your workflows using `${{ secrets.VERCEL_TOKEN }}`.

- **Testing**: Start with a basic test for your Next.js app, such as checking if a component renders correctly. Use Jest and React Testing Library for this purpose.

- **Linting and Formatting**: Include an ESLint configuration in your project to ensure consistent coding standards and integrate it into your CI/CD pipeline.

- **Deployment**: If deploying to Vercel or Netlify, ensure your build commands (`npm run build`) and environment variables are correctly set in the respective platform.

- **Debugging**: Use the logs in the GitHub Actions dashboard to identify issues in your workflow. Look for failed steps and analyze their output.

- **Secrets Configuration**: Check that all required secrets (e.g., `VERCEL_TOKEN`) are added to the GitHub repository’s settings under **Settings > Secrets and Variables > Actions**.

- **Error Handling**: If a workflow step fails, review the logs to see if it's due to missing dependencies, environment variables, or incorrect configuration.

- **Testing Deployments**: Once deployed to staging or production, test the application manually to ensure it behaves as expected.

- **Iterative Development**: Start small—test one part of the workflow, like building and testing, before adding deployment.

</details>

<br>

<br>


