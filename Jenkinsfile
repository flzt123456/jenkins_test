pipeline {
  agent any
  stages {
    stage('Download file') {
      steps {
        rtDownload(serverId: swpa_test, spec: '''{
                            "files": [
                                    {
                                        "pattern": "swpa/swpa/VD4224B/VD4224B-1.5.302.0.pkgtb",
                                        "target": "files"
                                    }
                                ]
                            }''')
        }
      }

    }
  }