pipeline {

    agent {
     kubernetes {
            label 'maven-slave'
        }
    }
  

    options {
        skipDefaultCheckout(true)
    }

    stages {
        stage('Checkout') {
            steps {
                  deleteDir()
                  checkout scm
            }
        }

        stage('Compile') {
            steps {
        	container('maven') {	
                  sh "mvn clean compile"
                }
            }
        }

	stage('Test') {
	   steps {
		container('maven') {
		  sh "mvn verify"
                }
	    }		
	}
     }
}
