pipeline {

    agent any
  
    libraries {
        lib('jsl')
    }

    environment {
        VERSION = ""
    }

    options {
        skipDefaultCheckout(true)
    }

    stages {
        stage('Checkout') {
            steps {
                script {
                    deleteDir()
                    checkout scm
                    def pom = readMavenPom()
                    def current_version = pom.getVersion()
                    VERSION = nextVersion(current_version)
                }
            }
        }

        stage('Compile') {
            steps {
                script {
                    sh """
                       mvn versions:set -DnewVersion=${VERSION}
                       mvn clean compile
                    """
               }
            }
        }
	// other stages
     }
}
