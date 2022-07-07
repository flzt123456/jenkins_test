pipeline {
  agent any
  stages {
    stage('VQA Test') {
      parallel {
        stage('Sanity Test') {
          agent {
            label 'RDTD_101'
          }
          post {
            success {
              echo 'VD4224B Sanity Test Pass on fw 2.5.301.3'
            }

            failure {
              echo 'VD4224B Sanity Test Fail on fw 2.5.301.3'
            }

          }
          steps {
            cleanWs()
            rtDownload(serverId: 'swpa_test', spec: '''{
                            "files": [
                                    {
                                        "pattern": "swpa/swpa/VD4224B/*",
                                        "target": "",
                                        "props": "Version=2.5.301.3"
                                    }
                                ]
                            }''')
              sh 'pscp -pw swpa@sdc ./swpa/VD4224B/* swpa@192.168.123.111:/home/swpa/Sharing/ftp/VD4224B/FW'
              sh '/home/nuc/Automation/Jenkins/FW_Upgrade.sh'
              sh '/home/nuc/Automation/Jenkins/runtest.sh'
            }
          }

          stage('Security Test') {
            agent {
              label 'RDTD_MINI'
            }
            post {
              success {
                echo 'VD4224B Security Test Pass on fw 2.5.301.3'
              }

              failure {
                echo 'VD4224B Security Test Fail on fw 2.5.301.3'
              }

            }
            steps {
              cleanWs()
              rtDownload(serverId: 'swpa_test', spec: '''{
                            "files": [
                                    {
                                        "pattern": "swpa/swpa/VD4224B/*",
                                        "target": "",
                                        "props": "Version=2.5.301.3"
                                    }
                                ]
                            }''')
                sh 'pscp -pw 123456 ./swpa/VD4224B/* pi@192.168.123.111:/home/pi/Sharing/ftp/VD4224B/FW'
                sh '/home/pi/Jenkins/FW_Upgrade.sh'
                sh '/home/pi/Jenkins/runtest.sh'
              }
            }

          }
        }

      }
    }