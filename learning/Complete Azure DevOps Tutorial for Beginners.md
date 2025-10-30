# Complete Azure DevOps Tutorial for Beginners (Updated for 2025)

Welcome to this comprehensive, step-by-step tutorial on Azure DevOps! Azure DevOps is a cloud-based platform from Microsoft that helps teams plan, develop, test, and deploy software applications efficiently. It's designed to support DevOps practices, which emphasize collaboration between development (Dev) and operations (Ops) teams for faster, more reliable software delivery. Whether you're a beginner developer, project manager, or IT professional, this guide will walk you through everything from setup to advanced features.

This tutorial assumes basic knowledge of software development concepts but no prior Azure DevOps experience. We'll cover the core services: **Azure Boards**, **Repos**, **Pipelines**, **Test Plans**, **Artifacts**, and **Extensions**. By the end, you'll have hands-on experience building a simple CI/CD pipeline.

**Note:** All instructions are in English (as "US language" typically refers to American English). Screenshots or visuals aren't included here, but I'll reference where to find them in the official docs.

## What is Azure DevOps?

Azure DevOps is a SaaS (Software as a Service) platform that integrates tools for the entire software development lifecycle (SDLC). It evolved from Visual Studio Team Services (VSTS) in 2018 and now supports agile planning, version control, automated builds, testing, and deployments. Key benefits include:
- **Collaboration:** Real-time tracking and shared visibility.
- **Automation:** CI/CD pipelines reduce manual errors.
- **Scalability:** Works with any language, platform, or cloud (e.g., Azure, AWS, GitHub).
- **Integration:** Connects with tools like GitHub, Slack, or Jira.

**Pricing (as of 2025):** Free for up to 5 users with basic features; paid plans start at $6/user/month for advanced usage. Check [Azure DevOps Pricing](https://azure.microsoft.com/en-us/pricing/details/devops/) for details.

**Prerequisites:**
- A Microsoft account (free at [outlook.com](https://outlook.com)).
- Basic command-line knowledge (e.g., Git).
- Optional: Visual Studio Code (free IDE) for coding.

## Step 1: Setting Up Your Azure DevOps Account and Organization

1. **Sign Up:**
   - Go to [dev.azure.com](https://dev.azure.com).
   - Click **Start free** and sign in with your Microsoft account. If you're new, select "Create a Microsoft account" (no credit card needed).
   - Accept the terms and create your organization (e.g., "MyDevOpsOrg"). This is your top-level workspace.

2. **Create Your First Project:**
   - In the organization dashboard, click **New Project**.
   - Enter a name (e.g., "MyFirstApp"), description, and visibility (Private for teams; Public for open-source).
   - Choose **Git** for version control (recommended over TFVC for beginners).
   - Click **Create**. You'll land in the project overview.

**Tip:** Organizations can host multiple projects. For tutorials, start with one.

Your project dashboard shows all services. Let's explore them one by one.

## Step 2: Azure Boards – Planning and Tracking Work

Azure Boards is for agile project management: backlogs, Kanban boards, sprints, and reporting.

### Key Features:
- **Work Items:** Track tasks, bugs, features, or epics.
- **Backlogs:** Prioritize work.
- **Boards:** Visualize progress with Kanban or Scrum views.
- **Dashboards:** Custom widgets for metrics.

### Hands-On: Create a Backlog
1. In your project, select **Boards > Backlogs**.
2. Click **+ New Work Item** > **User Story** (e.g., Title: "As a user, I want to log in securely").
3. Add details: Description, Acceptance Criteria, Tags.
4. Drag items to prioritize in the backlog.
5. Switch to **Boards > Kanban** to see a visual flow (To Do > Doing > Done).

**Pro Tip:** Link work items to code commits for traceability (e.g., use #WorkItemID in commit messages).

For more: [Azure Boards Documentation](https://learn.microsoft.com/en-us/azure/devops/boards/?view=azure-devops).

## Step 3: Azure Repos – Version Control with Git

Azure Repos provides unlimited private Git repositories for code storage and collaboration.

### Key Features:
- **Git Repos:** Branching, pull requests (PRs), and merge policies.
- **TFVC:** Centralized version control (less common now).
- **Branch Policies:** Require reviews before merging.

### Hands-On: Set Up a Repo and Make Changes
1. In your project, go to **Repos > Files**.
2. If empty, click **Initialize** to create a README.md.
3. Clone the repo locally:
   - Copy the HTTPS clone URL.
   - In VS Code terminal: `git clone <URL>`.
   - Navigate: `cd MyFirstApp`.
4. Make a change: Edit README.md, then commit:
   ```
   git add .
   git commit -m "Update README #1"  # Links to work item #1
   git push origin main
   ```
5. Create a branch and PR:
   - `git checkout -b feature/login`.
   - Make changes, commit, push.
   - In Azure Repos > Pull Requests, click **New Pull Request**.
   - Add reviewers, description, and complete after approval.

**Security Note:** Enable branch policies for main branch to require PRs.

For more: [Azure Repos Tutorial](https://learn.microsoft.com/en-us/azure/devops/repos/git/?view=azure-devops).

## Step 4: Azure Pipelines – CI/CD Automation

Pipelines automate building, testing, and deploying code (CI/CD: Continuous Integration/Continuous Delivery).

### Key Features:
- **YAML Pipelines:** Code-as-config for builds.
- **Hosted Agents:** Free Microsoft-hosted VMs (Linux, Windows, macOS).
- **Multi-Stage:** Build > Test > Deploy.

### Hands-On: Build Your First Pipeline
We'll create a simple Node.js app pipeline (adapt for your language).

1. **Prepare Code:** In your repo, create a simple app:
   - Add `index.js`: `console.log("Hello Azure DevOps!");`
   - Add `package.json` with `"start": "node index.js"`.
   - Commit and push.

2. **Create Pipeline:**
   - Go to **Pipelines > New Pipeline**.
   - Select **Azure Repos Git** > Your repo.
   - Choose **Starter pipeline** (YAML).
   - Replace with this basic YAML (save as `azure-pipelines.yml` in repo root):
     ```
     trigger:
     - main

     pool:
       vmImage: 'ubuntu-latest'

     steps:
     - task: NodeTool@0
       inputs:
         versionSpec: '18.x'
     - script: npm install
       displayName: 'Install dependencies'
     - script: npm test || echo "No tests"
       displayName: 'Run tests'
     - task: PublishTestResults@2
       condition: succeededOrFailed()
       inputs:
         testResultsFormat: 'JUnit'
         testResultsFiles: '**/test-results.xml'
     ```
   - Click **Run**. Watch it build!

3. **Add Deployment Stage:** Edit YAML to add a deploy stage (e.g., to Azure App Service):
     ```
     stages:
     - stage: Build
       jobs:
       - job: BuildJob
         steps:
         - script: echo "Building..."
     - stage: Deploy
       dependsOn: Build
       jobs:
       - deployment: DeployJob
         environment: 'production'
         strategy:
           runOnce:
             deploy:
             steps:
             - task: AzureWebApp@1
               inputs:
                 azureSubscription: 'YourSubscription'
                 appName: 'myapp'
                 package: '$(Pipeline.Workspace)/**/*.zip'
     ```
   - Connect to Azure: In **Project Settings > Service Connections**, add an Azure Resource Manager connection.

**Best Practice:** Use variables for secrets (e.g., API keys) in **Pipelines > Library**.

For more: [Azure Pipelines Guide](https://learn.microsoft.com/en-us/azure/devops/pipelines/?view=azure-devops).

## Step 5: Azure Test Plans – Testing and Quality Assurance

Test Plans manage manual/automated tests, track defects, and ensure quality.

### Key Features:
- **Test Suites:** Organize tests into plans and cases.
- **Exploratory Testing:** Ad-hoc bug hunting.
- **Integration:** Link tests to Pipelines for automated runs.

### Hands-On: Create a Test Case
1. Go to **Test Plans > + New Test Plan**.
2. Add a **Test Suite** > **Requirements-based** (link to a work item).
3. Click **+ New Test Case**: Title: "Verify Login", Steps: "Enter credentials > Click Submit > Check redirect".
4. Run the test: Mark as Passed/Failed, attach screenshots.

**Automation Tip:** Use the `@webtest` task in Pipelines for integration.

For more: [Test Plans Overview](https://learn.microsoft.com/en-us/azure/devops/test/?view=azure-devops).

## Step 6: Azure Artifacts – Package Management

Artifacts hosts packages (NuGet, npm, Maven) for sharing across teams.

### Key Features:
- **Feeds:** Private repositories for binaries.
- **Upstream Sources:** Proxy public registries like npmjs.com.

### Hands-On: Publish a Package
1. Go to **Artifacts > Create Feed** (e.g., "MyFeed").
2. In your pipeline YAML, add:
   ```
   - task: Npm@1
     inputs:
       command: 'publish'
       publishRegistry: 'myFeed'
   ```
3. Run the pipeline; view packages in Artifacts.

For more: [Artifacts Tutorial](https://learn.microsoft.com/en-us/azure/devops/artifacts/?view=azure-devops).

## Step 7: Extensions and Integrations

Enhance Azure DevOps with the Marketplace:
1. Go to **Extensions > Browse Marketplace**.
2. Install popular ones: Slack notifications, SonarQube for code analysis.
3. Integrate with GitHub: **Project Settings > GitHub Connections**.

**Advanced:** Enable AI assistance (e.g., GitHub Copilot integration) for code suggestions.

## Best Practices and Monitoring
- **Security:** Use multi-stage approvals and role-based access.
- **Monitoring:** Add Azure Monitor for logs; dashboards for pipeline metrics.
- **Scaling:** For large teams, use multi-repo pipelines.
- **Common Pitfalls:** Avoid over-customizing YAML initially; start simple.

## Real-World Project: Deploy a Simple Web App
1. Create a Node.js/Flask app in Repos.
2. Track features in Boards.
3. Set up a Pipeline for build/test/deploy to Azure App Service.
4. Run tests in Test Plans.
5. Publish npm packages via Artifacts.

Test it: Push code and watch the pipeline deploy live!

## Next Steps and Resources
- **Official Docs:** [Azure DevOps Get Started](https://learn.microsoft.com/en-us/azure/devops/get-started/?view=azure-devops).
- **Video Series:** [Azure DevOps Zero to Hero (YouTube Playlist)](https://www.youtube.com/playlist?list=PLl4APkPHzsUXseJO1a03CtfRDzr2hivbD) – 15+ videos with demos.
- **Courses:** [Udemy: Azure DevOps Fundamentals](https://www.udemy.com/course/azure-devops-for-beginners/) or [Microsoft Learn Path](https://learn.microsoft.com/en-us/training/paths/evolve-your-devops-practices/).
- **Community:** Join Reddit's r/AZURE or Azure Discord.

Practice on a free account, and you'll be deploying like a pro in no time. Questions? Drop them in the comments or forums. Happy DevOps-ing! 🚀
