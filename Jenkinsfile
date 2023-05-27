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

    }
}
