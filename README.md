# Learning Azure DevOps

Just one of the things I'm learning. <https://github.com/hchiam/learning>

My first Azure DevOps git repo: <https://dev.azure.com/hchiam/_git/test-azure-devops-project>

You can set up automated tests, just like Travis CI on GitHub: use Pipelines, select a template, and it'll run automatically. For example:

- <https://dev.azure.com/hchiam/_git/code-inspiration?path=%2Fazure-pipelines.yml>
- <https://dev.azure.com/hchiam/code-inspiration/_build/results?buildId=42&view=logs&j=bf812b03-26a5-57bb-2723-1df9c646b646>
- <https://dev.azure.com/hchiam/code-inspiration/_build>

Example `azure-pipelines.yml` that can run the app while running a Selenium .side test:

```yaml
trigger:
- master

pool:
  vmImage: 'ubuntu-latest'
  name: Azure Pipelines
  demands: npm

stages:
- stage: Test
  jobs:
  - job: TestJob
    displayName: Agent Job 1
    steps:
    - task: Npm@1
      displayName: install
      inputs:
        verbose: false

    - task: Npm@1
      displayName: 'install chromedriver'
      inputs:
        command: custom
        verbose: false
        customCommand: 'install chromedriver'

    - task: Npm@1
      displayName: 'install selenium-side-runner'
      inputs:
        command: custom
        verbose: false
        customCommand: 'install selenium-side-runner'

    - task: Npm@1
      displayName: 'install react-scripts'
      inputs:
        command: custom
        verbose: false
        customCommand: 'install react-scripts'

    - script: 'npx react-scripts build'
      displayName: 'build (npx)'

    - script: 'npx react-scripts start & npm run side-test'
      displayName: 'start (npx) & side-test'
```

Another example:

- Release CD pipeline: <https://dev.azure.com/hchiam/react-app/_releaseProgress?_a=release-pipeline-progress&releaseId=1>
- <https://github.com/hchiam/react-app>
- <https://dev.azure.com/hchiam/react-app/_build/results?buildId=11&view=logs&j=275f1d19-1bd8-5591-b06b-07d489ea915a>

## More learning

<https://www.youtube.com/watch?v=H-R2bCXfz8I>
