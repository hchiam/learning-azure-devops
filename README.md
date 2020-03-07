# Learning Azure DevOps

Just one of the things I'm learning. <https://github.com/hchiam/learning>

Just like Travis CI on GitHub, you can set up automated tests in Azure DevOps to run whenever you commit to master: use Pipelines, select a template, and it'll run automatically. `azure-pipelines.yml` can be automagically generated or manually created to set up your tests.

Current favourites: [Selenium WebDriver](https://dev.azure.com/hchiam/test-cross-browser-testing/_git/test-cross-browser-testing-selenium?path=%2Fazure-pipelines.yml) example and [Cypress](https://dev.azure.com/hchiam/test-cypress/_git/test-cypress?path=%2Fazure-pipelines.yml) example.

## [My first Azure DevOps git repo](https://dev.azure.com/hchiam/_git/test-azure-devops-project)

<https://dev.azure.com/hchiam/_git/test-azure-devops-project>

## [Selenium IDE test example](https://dev.azure.com/hchiam/code-inspiration)

<https://dev.azure.com/hchiam/code-inspiration>

Selenium IDE (as opposed to Selenium WebDriver) is very easy to set up locally: just install a Chrome Extension or Firefox Addon with a few clicks, and record actions directly in the browser. However, certain actions will not replay correctly when you use the CLI command, or require workarounds/tricks to work (in which case, you might want to use Cypress - see the other example).

This is an `azure-pipelines.yml` configuration file that runs the app while running a Selenium .side test: <https://dev.azure.com/hchiam/_git/code-inspiration?path=%2Fazure-pipelines.yml>

<details>

<summary>YAML: (Click to expand)</summary>

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

</details>

Results:

<https://dev.azure.com/hchiam/code-inspiration/_build/results?buildId=42&view=logs&j=bf812b03-26a5-57bb-2723-1df9c646b646&t=8be40cd7-2387-56cf-0dc5-8e64b7786d0a>

<https://dev.azure.com/hchiam/code-inspiration/_build>

## [Cypress test example (+Cucumber/Gherkin)](https://dev.azure.com/hchiam/_git/test-cypress?path=README.md)

<https://dev.azure.com/hchiam/_git/test-cypress?path=README.md>

The interface part of Cypress is very developer-friendly. Currently supports Chrome, Firefox, Edge, and Electron, but not Internet Explorer yet as of February 2020 (in which case, you might want to use Selenium WebDriver - see the other example).

Here's an example test configuration for Azure DevOps:

<details>

<summary>YAML: (Click to expand)</summary>

```yml
trigger:
- master

pool:
  vmImage: 'ubuntu-latest'

steps:
- task: NodeTool@0
  inputs:
    versionSpec: '10.x'
  displayName: 'Install Node.js'

- script: npm install
  displayName: 'Install Dependencies'

- script: npx cypress run
  displayName: 'Run Cypress Test'
```

</details>

Results:

<https://dev.azure.com/hchiam/test-cypress/_build/results?buildId=48&view=logs&j=12f1170f-54f2-53f3-20dd-22fc7dff55f9&t=5caf77c8-9b10-50ef-b5c7-ca89c63e1c86>

## [Selenium WebDriver test example (cross-browser testing)](https://dev.azure.com/hchiam/test-cross-browser-testing/_git/test-cross-browser-testing-selenium?path=README.md)

<https://dev.azure.com/hchiam/test-cross-browser-testing/_git/test-cross-browser-testing-selenium?path=README.md>

Selenium WebDriver can run on Firefox, Chrome, Internet Explorer, and more. It has APIs for different programming languages, which includes JavaScript via [`selenium-webdriver`](https://www.npmjs.com/package/selenium-webdriver#installation).

Here's an example test configuration for Azure DevOps:

<details>

<summary>YAML: (Click to expand)</summary>

```yml
trigger:
- master

pool:
  vmImage: 'ubuntu-latest'

steps:
- task: NodeTool@0
  inputs:
    versionSpec: '10.x'
  displayName: 'Install Node.js'

- script: npm install
  displayName: 'Install Dependencies'

- script: node index
  displayName: 'Run Selenium WebDriver Test'
```

</details>

Results: <https://dev.azure.com/hchiam/test-cross-browser-testing/_build/results?buildId=51&view=logs&j=12f1170f-54f2-53f3-20dd-22fc7dff55f9&t=5caf77c8-9b10-50ef-b5c7-ca89c63e1c86>

## [Another example](https://dev.azure.com/hchiam/react-app/_releaseProgress?_a=release-pipeline-progress&releaseId=1)

- Release CD pipeline: <https://dev.azure.com/hchiam/react-app/_releaseProgress?_a=release-pipeline-progress&releaseId=1>
- <https://github.com/hchiam/react-app>
- <https://dev.azure.com/hchiam/react-app/_build/results?buildId=11&view=logs&j=275f1d19-1bd8-5591-b06b-07d489ea915a>

## Further learning

<https://www.youtube.com/watch?v=H-R2bCXfz8I>
