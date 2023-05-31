pipeline {
    agent any

    tools {
	maven "jenkinsmaven"
    }

    stages {
	stage('Build') {
            steps {
                sh 'mvn clean package'
            }
	}
	stage('Archivar artefacto') {
            steps {
                archiveArtifacts 'target/ControlInventario-0.0.1-SNAPSHOT.jar'
            }
	}
	stage('Ejecutar Tests') {
            steps {
                sh 'mvn test'
            }
	}
    stage('Sonar Scanner') {
    steps {
        script {
            def sonarqubeScannerHome = tool name: 'sonar', type: 'hudson.plugins.sonar.SonarRunnerInstallation'
            withCredentials([string(credentialsId: 'sonar', variable: 'sonarLogin')]) {
                sh "${sonarqubeScannerHome}/bin/sonar-scanner -e \
                    -Dsonar.host.url=http://SonarQube:9000 \
                    -Dsonar.login=${sonarLogin} \
                    -Dsonar.projectName=gs-gradle \
                    -Dsonar.projectVersion=${env.BUILD_NUMBER} \
                    -Dsonar.projectKey=GS \
                    -Dsonar.sources=src/main/java/com/kibernumacademy/miapp \
                    -Dsonar.tests=src/test/java/com/kibernumacademy/miapp \
                    -Dsonar.language=java \
                    -Dsonar.java.binaries=."
            }
        }
    }
}





    }
}
