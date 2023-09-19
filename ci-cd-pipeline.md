

trigger:
  branches:
    include:
    - main
    - develop
  paths:
    include:
    - pipelines/azure_multi_stage_pipeline.yml 

stages:
# *****************  Build Stage starts here ******************** #
- stage: buildStage
  jobs:
  - job: buildJob
    pool:
      vmImage: ubuntu-latest
    steps:
    - task: NodeTool@0
      displayName: 'Install Node.js'
      inputs:
        versionSpec: '10.x'
    - task: Npm@1
      displayName: npm install
      inputs:
        command: 'install'
        workingDir: 'code/.'
    - task: Npm@1
      displayName: npm run build
      inputs:
        command: 'custom'
        workingDir: 'code/.'
        customCommand: 'run build'
    - task: ArchiveFiles@2
      displayName: "Archiving Artifacts"
      inputs:
        rootFolderOrFile: 'code/'
        includeRootFolder: false
        archiveType: 'zip'
        archiveFile: 'react_stopwatch'
        replaceExistingArchive: true
    - task: PublishBuildArtifacts@1
      displayName: 'Publish Artifacts'
      inputs:
        PathtoPublish: 'react_stopwatch.zip'
        ArtifactName: 'react_stopwatch'
        publishLocation: Container

# *****************  Deployment Stage starts here ******************** #

** Can you add code for the deployment stage hereto deploy to Azure App Service ?. Do not worry about the syntax of yaml and it's attributes
