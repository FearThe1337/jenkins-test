node {
    stage('Build') {
        dir ('jenkins-test-code') {
            withMaven(jdk: 'jdk-14', maven: 'maven-3.6', options: [junitPublisher(healthScaleFactor: 1.0), jacocoPublisher(), artifactsPublisher()]) {
                sh 'mvn clean package'
            }
        }
    }
}