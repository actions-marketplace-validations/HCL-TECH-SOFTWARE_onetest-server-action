## HCL OneTest Server GitHub Action
HCL OneTest provides software testing tools to support a DevOps approach: API testing, functional testing, UI testing, performance testing and service virtualization. It helps you automate and run tests earlier and more frequently to discover errors sooner - when they are less costly to fix.

This action enables the ability to run various tests from a HCL OneTest Server project.

## Usage

## Prerequisites to run this action

Configure a self hosted runner on a suitable machine
1. The host machine will need to be able to access the OneTest Server that will be used to run tests.
2. [Add a self-hosted runner](https://docs.github.com/en/actions/hosting-your-own-runners/adding-self-hosted-runners) at an appropriate level, ensure you have configured network access.
3. If you are using more than one runner [assign it a suitable label](https://docs.github.com/en/actions/hosting-your-own-runners/using-labels-with-self-hosted-runners) and note this for later.
**OR**
1. An instance of OneTest Server that can be accessed from the GitHub's hosted runners

### Setup
In the repository you want to apply the action to
1. Create a folder named ".github/workflows" in the root.
2. Create a .yml file with any name, inside the ".github/workflows" folder based on the following example content:

```yaml
name: HCL OneTest Server

on: workflow_dispatch

jobs:
    OTS-Action:
        runs-on: self-hosted
        name: HCL OneTest Server
        steps:
         - name: Execute Test
           uses: HCL-TECH-SOFTWARE/onetest-server-action@main
           with:
            serverUrl: 
            offlineToken: 
            teamspace: 
            project: 
            branch: 
            assetId: 
            environment: 
            datasets:
            labels: 
            secretsCollection:
            variables:

```

3. Update the parameterized items to refer to your server, project and tests (see parameter details below).
4. Depending on connectivity, 
  - If you have more than one hosted runner configured, then use its label as the argument for **runs-on**.
  - If the OneTest Server is accessible from GitHub then use **runs-on: ubuntu-latest** 
5. Push your updated yml file to the repository.
6. Go to the Actions section in the repository and select the workflow.
7. Click the Run workflow dropdown and the list of input boxes get displayed.

### Required Parameters

- **serverUrl ** URL of the HCL OneTest Server where the tests are located. URL should be of the format - https://hostname
- **offlineToken** The offline user token for the corresponding HCL OneTest Server
- **teamspace** Team Space name of the project.
- **project** Project name of the test.
- **branch** Project name of the test.
- **assetId** AssetId of the test file in HCL OneTest Server.

### Optional Parameters

- **environment** Test environment corresponding to the test. Mandatory to input the value if you want to run API test.
- **datasets** Semicolon (;) delimited list of source:replacement datasets for the job to run. For example, dataset1:dataset2;dataset3:dataset4
- **labels** Labels to add to test results when the test run is complete. You can add multiple labels to a test result separated by a comma. For example, label1, label2.
- **secretsCollection** Secrets collection name for the job to run.
- **variables** Variables corresponding to the test. The format is name_of_the_variable=value_of_the_variable. You can add multiple variables to the test run separated by a semicolon.

## Troubleshooting
- **No runner available:** If you are using a self-hosted runnter, check that the runner still exists in GitHub, if the local agent has not connected to GitHub for a period of 14 days then it will be automatically removed.