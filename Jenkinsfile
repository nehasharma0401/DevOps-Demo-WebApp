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
	        echo 'Code Analysis'
	        
	      }
	    }
	

	    stage('Compile Webapp') {
	      steps {
	        echo 'Compiling Webapp'
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
	                buildInfo = rtMaven.run pom: 'functionaltest/pom.xml', goals: 'test'
	               publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll:false, reportDir: '\\functionaltest\\target\\surefire-reports', 
		       reportFiles: 'index.html', reportName: 'UI Test Report', reportTitles: ''])

	      }
	    }
	

	    stage('Performance Test') {
	      steps {
	        echo 'Performing Blazemeter Test'
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
	    stage('Notification') {
	      steps {
	        echo 'Sending alerts'
	      }
	    }
	  }
	}
