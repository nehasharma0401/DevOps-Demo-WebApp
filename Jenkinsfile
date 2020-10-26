pipeline {
  agent any
  stages {
    stage('Clone Webapp') {
      steps {
        git(url: 'https://github.com/nehasharma0401/DevOps-Demo-WebApp.git', poll: true)
      }
    }

    stage('Static Code Analysis') {
      steps {
        echo 'Code Analysis using Sonar Qube'
        
      }
    }

    stage('Compile Webapp') {
      steps {
        echo 'Compiling Webapp'
        sh 'mvn compile'
      }
    }

    stage('Deploy to Test') {
      steps {
        echo 'Deploy to Tomcat Server in Test Environment'
      }
    }

    stage('Storing Artifacts') {
      steps {
        echo 'Storing Artifacts'
      }
    }
    
    stage('Perform UI Test') {
      steps {
        echo 'Performing UI Test'
      }
    }

    stage('Performance Test') {
      steps {
        echo 'Performing Performance Test'
      }
    }
    
    stage('Deploy To production') {
      steps {
        echo 'Deploying To production'
      }
    }

    stage('Sanity Test') {
      steps {
        echo 'Performing Sanity Test'
      }
    }
  }
}
