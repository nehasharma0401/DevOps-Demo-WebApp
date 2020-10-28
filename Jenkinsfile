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
		publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll:    false, reportDir: '\\functionaltest\\target\\surefire-reports', reportFiles: 'index.html', reportName: 'UI Test Report', reportTitles: ''])
	    }
	

	    stage('Performance Test') {
	      steps {
	        echo 'Performing Blazemeter Test'
	      }
	    }
	    
	    stage('Deploy To production') {
	      steps {
		      deploy adapters: [tomcat7(credentialsId: 'AWStomcat', path: '', url: 'http://3.14.10.76:8080/')], contextPath: '/ProdWebapp', war: '**/*.war'
		     jiraSendDeploymentInfo environmentId: 'Staging', environmentName: 'Staging', environmentType: 'staging', serviceIds: ['http://3.14.10.76:8080/ProdWebapp'], site: 'devopsbc.atlassian.net', state: 'successful'
		     jiraSendDeploymentInfo environmentId: 'Prod', environmentName: 'prod', environmentType: 'production', serviceIds: ['http://3.14.10.76:8080/ProdWebapp'], site: 'devopsbc.atlassian.net', state: 'successful'
  }
}
	

	    stage('Sanity Test') {
	      steps {
	        buildInfo = rtMaven.run pom: 'Acceptancetest/pom.xml', goals: 'test'
		publishHTML([allowMissing: false, alwaysLinkToLastBuild: false, keepAll: false, reportDir: '\\Acceptancetest\\target\\surefire-reports', reportFiles: 'index.html', reportName: 'Sanity Test Report', reportTitles: ''])
	    }
		slackSend channel: 'project-dcs', message: "Build Completed ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)", tokenCredentialId: 'slack'
	 }
	 catch (exc) {
	 	echo 'I failed'
		slackSend channel: 'project-dcs', message: "Build Failed ${env.JOB_NAME} ${env.BUILD_NUMBER} (<${env.BUILD_URL}|Open>)", tokenCredentialId: 'slack'
	 }
	 finally {
		if (currentBuild.result == 'failure') {
	            echo 'I am unstable :/'
		     error " failed"
	        } else {
	            echo 'One way or another, I have finished $currentBuild.result'
	      }
	    }
	    stage('Notification') {
	      steps {
	        echo 'Sending alerts'
	      }
	    }
	  }
	}


