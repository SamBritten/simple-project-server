pipeline {
    agent any
	environment {
    		VERSION = readMavenPom().getVersion()
	}
    stages {
	    stage('Version') {
		    steps {
		    	echo "$(version)"
		    }
	    }
        stage('Test') {
            steps {
                    sh 'mvn test -Dtest=ControllerAndServiceSuite'
		    sh 'mvn test -Dtest=IntegrationSuite'
                }
            }
        stage('Build') {
            steps {
                    sh 'mvn package -DskipTests'
		    sh 'docker build -t="sam315/simple-project-server:latest" .'
                }
            }
        stage('Deploy') {
            steps {
                    sh 'docker push sam315/simple-project-server:latest'
                }
            }
	 stage('Testing Environment') {
            steps {
                echo "hello"
                }
            }
         stage('Staging') {
		 when {
			 expression {
				 env.BRANCH_NAME=='developer'
			 }
		 }
            steps {
                echo "hello"
                 }
            }
          stage('Production') {
	     when  {
		expression {  
			env.BRANCH_NAME=='master'
		}
	     }
             steps {
                echo "hello"
                  }
             }
    }
}
