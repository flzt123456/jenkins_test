pipeline {
  agent any
  stages {
    stage('Clone') {
      steps {
        git(branch: 'master', url: 'https://github.com/jfrog/project-examples.git')
        input(message: 'Please Input Model Name', id: 'Model')
      }
    }

    stage('Upload file') {
      steps {
        rtUpload(serverId: SERVER_ID, spec: '''{
                            "files": [
                                    {
                                        "pattern": "jenkins-examples/pipeline-examples/resources/ArtifactoryPipeline.zip",
                                        "target": "libs-snapshot-local"
                                    }
                                ]
                            }''')
        }
      }

      stage('Publish build info') {
        steps {
          rtPublishBuildInfo SERVER_ID
        }
      }

      stage('Set output resources') {
        steps {
          jfPipelines(outputResources: """[
                                    {
                                          "name": "pipelinesBuildInfo",
                                          "content": {
                                                "buildName": "${env.JOB_NAME}",
                                                "buildNumber": "${env.BUILD_NUMBER}"
                                            }
                                        }
                                    ]""")
              }
            }

          }
        }