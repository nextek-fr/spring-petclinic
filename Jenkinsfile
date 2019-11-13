pipeline {

    agent {
     kubernetes {
            label 'petclinic-app'
            defaultContainer 'jnlp'
            yaml """
apiVersion: v1
kind: Pod
metadata:
  labels:
    pipeline: jenkinsfile
spec:
  containers:
    - name: 'maven'
      image: maven:3.3.9
      command:
        - cat
      tty: true
      volumeMounts:
        - mountPath: '/root/.m2'
          name: maven-repo
          readOnly: false
  volumes:
    - name: maven-repo
      persistentVolumeClaim:
        claimName: maven-repo-pvc
"""
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
