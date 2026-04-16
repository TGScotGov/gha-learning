# Github actions

First Github actions demo

## method

Stage 1 — Understand GitHub Actions (10 minutes)
Takeaway: GitHub Actions is automation that runs in the cloud whenever something happens in your repo.

What you need to know right now
A workflow = the automation file

A job = a set of steps

A step = a command or action

Workflows live in:
.github/workflows/yourfile.yml

Your task
Create a new GitHub repo named gha-learning.

Add a simple file like README.md.

Click the Actions tab and look around.

That’s it. No coding yet.

⭐ Stage 2 — Create your first workflow (15 minutes)
This will run every time you push code.

Your task
In your repo, create this folder structure:

Code
.github/
  workflows/
    first.yml
Put this inside first.yml:

yaml
name: First Windows Workflow

on:
  push:
    branches: [ main ]

jobs:
  hello:
    runs-on: windows-latest

    steps:
      - name: Say hello
        run: echo "Hello from GitHub Actions on Windows!"
Commit and push.

What to do next
Go to Actions → click the run → open the logs

You should see the message printed

You’ve now run your first GitHub Action.

⭐ Stage 3 — Run a script from your Windows Server repo (20 minutes)
Now you’ll run a script stored in your repo—this is where it starts feeling real.

Your task
Create a file in your repo called test.ps1:

powershell
Write-Host "Running PowerShell script..."
Write-Host "Everything works!"
Update your workflow:

yaml
name: Run PowerShell Script

on:
  push:
    branches: [ main ]

jobs:
  run-script:
    runs-on: windows-latest

    steps:
      - name: Checkout code
        uses: actions/checkout@v4

      - name: Run PowerShell script
        run: ./test.ps1
        shell: pwsh
Commit and push.

What to look for
The workflow should run on a Windows runner

You should see your PowerShell output in the logs

⭐ Stage 4 — Add something useful (30 minutes)
Now you’ll make GitHub Actions do something practical.

Choose one of these (your choice):

Option A — Run a PowerShell test script
Add a script like:

powershell
# test.ps1
$number = 5
if ($number -eq 5) {
    Write-Host "Test passed"
} else {
    Write-Host "Test failed"
}
Your workflow already runs it.

Option B — Run a build command (if you use .NET)
Add:

yaml
- name: Setup .NET
  uses: actions/setup-dotnet@v4
  with:
    dotnet-version: 8.0.x

- name: Build project
  run: dotnet build
Option C — Run a Windows command
For example:

yaml
- name: List directory
  run: dir
This helps you understand how the runner behaves.

⭐ Stage 5 — Add triggers (10 minutes)
Right now your workflow runs only on pushes.
Let’s add pull requests too.

Your task
Modify the top of your workflow:

yaml
on:
  push:
    branches: [ main ]
  pull_request:
    branches: [ main ]
Now GitHub Actions will run when:

You push code

You open a pull request

This is how teams automate testing before merging.

⭐ Stage 6 — Explore and copy real examples (20 minutes)
This is where GitHub Actions starts to “click.”

Your task
Go to your repo → Actions

Look at the suggested templates

Pick one that matches your language or environment

Compare it to your workflow:

Where is on:?

Where are jobs:?

What steps are used?

Copying and tweaking is the fastest way to learn.

⭐ Stage 7 — Your “I understand GitHub Actions” checklist
You’re good once you can:

Create a workflow from scratch

Run commands on a Windows runner

Trigger workflows on push and PR

Read someone else’s workflow and explain what it does

Add steps and see them run

If you can do those, you’ve got the fundamentals.