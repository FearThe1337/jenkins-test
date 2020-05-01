def addBasicFunctionality(Closure body) {
    timestamps {
        ansiColor {
            body()
        }
    }
}

def runBuild() {
    dir ('jenkins-test-code') {
        withMaven(jdk: 'jdk-14', maven: 'maven-3.6', options: [
                junitPublisher(healthScaleFactor: 1.0),
                jacocoPublisher(),
                artifactsPublisher(),
                findbugsPublisher()
                ]) {
            sh 'mvn clean package'
        }
    }
}

addBasicFunctionality {
    node {
        def mvn
        stage('Build') {
            runBuild()
        }
        stage ('OWASP Dependency-Check Vulnerabilities') {
            dependencyCheck();
            dependencyCheckPublisher();
        }
    }
}
// slackSend channel: "#calgary-dev", message: