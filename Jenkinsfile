// node {
// 	stage('Build') {
// 		echo "Build"
// 	}
// 	stage('Test') {
// 		echo "Test"
// 	}
// 	stage('IntegrationTest') {
// 		echo "Test"
// 	}
// }
pipeline{
	agent any

	// agent{
	// 	docker{
	// 		image 'maven:3.6.3'
	// 	}
	// }
environment{
	dockerHome = tool 'myDocker'
	mavenHome = tool 'myMaven'
	PATH = "$dockerHome/bin:$mavenHome/bin:$PATH"
}
	stages{
	stage('Build') {
		steps{
			//sh 'mvn --version'
			sh 'docker version'
			echo "Build"
			echo "Printing enviornmnet varibales"
			echo "Build_number - $env.BUILD_ID"
			echo "Job name - $env.JOB_NAME"
		}
	}
	stage('Test') {
		steps{
			echo "Test"
		}
	}
	stage('IntegrationTest') {
		steps{
			echo "Integration Test"
		}
	}
	} 
	post{
		always{
			echo 'I am running always'
		}
		success{
			echo 'I am running when the build successed'
		}
		failure{
			echo 'I am running when the build failed'
		}
	}
}