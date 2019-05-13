pipeline {
  agent any
  stages {
    stage('Download Feature Files') {
          steps {
            downloadFeatureFiles(serverAddress: 'http://35.235.105.137', projectKey: 'POC', targetPath: 'src/test/java/Feature')
          }
    }

    stage('Clean Work Space') {
      steps {
        bat 'mvn clean install'
      }
    }
    stage('Execute Running') {
      steps {
        bat 'mvn surefire:test -Dtest=Running_Buscar_Google'
      }
    }
  }
  post {
    always {
      archiveArtifacts(artifacts: 'target/', fingerprint: true)
      junit 'target/cucumber.xml'
      publishTestResults(serverAddress: 'http://35.235.105.137', projectKey: 'POC', filePath: 'target/cucumber.json', format: 'Cucumber', autoCreateTestCases: false)

    }
  }
}
