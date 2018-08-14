pipeline {
  agent {
    label 'android'
  }
  stages {

    stage('Lint') {
      steps {
script {
	if (isUnix()) {
        sh '''
	export LANG=en_US.UTF-8
	source ~/.bash_profile
	bundle exec fastlane lint
	'''
        // publish Android Lint results
        androidLint canComputeNew: false, defaultEncoding: '', healthy: '', pattern: 'app/build/reports/**/lint-results.xml', unHealthy: ''
      }
	else{
	    echo 'Linting on Windows started '
	    bat 'gradle lint'
    }
}
}    
}
    
    stage('Unit tests') {
      steps {
	script{
		if (isUnix()) {
        	sh './gradlew clean test'
		}
		else
		{
			echo 'Running unit tests on Windows..'
			bat 'gradlew clean test'
		}
	}
      }
    }
}

  // https://github.com/jenkinsci/pipeline-model-definition-plugin/wiki/Reporting-test-results-and-storing-artifacts
  post {
    always {
      //archive "build/**/*"
    }
  }
}