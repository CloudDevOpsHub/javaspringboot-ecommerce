pipeline {
  agent {
    docker {
      image 'maven:3.9-eclipse-temurin-17'
      args '-v maven-repo:/root/.m2'
    }
  }
  
  environment {
    MAVEN_OPTS = "-Dmaven.repo.local=/root/.m2"
  }   
  
  stages {
    stage('Check Environment') {
      steps { 
 	echo 'java --version'
	echo 'mvn --version'
      }
    }

    stage('Compile Code') {
      steps {
	echo 'Compiling Java Project....'
	sh 'mvn clean compile'
      }
    }

    stage('Run Steps') {
      steps {
	echo 'Running unit tests....'
	echo 'mvn test'
      }
    }
  }

  post {
    always {
      junit 'target/surefire-reports/*.xml'
    }
    success {
      echo 'Java compile and test stage succeeded!'
    }
    failure {
      echo 'Java compile and test stage failed!'
    }
  }
}
