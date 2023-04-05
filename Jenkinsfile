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
	stage('Checkout') {
		steps{
			//sh 'mvn --version'
			sh 'docker version'
			echo "Build"
			echo "Printing enviornmnet varibales"
			echo "Build_number - $env.BUILD_ID"
			echo "Job name - $env.JOB_NAME"
		}
	}
	stage('Compile') {
		steps{
			sh "mvn clean compile"
		}
	}
	stage('Test') {
		steps{
			sh "mvn test"
		}
	}
	stage('IntegrationTest') {
		steps{
			sh "mvn failsafe:integration-test failsafe:verify"
		}
	}

	stage('Package') {
		steps{
			sh "mvn package -DskipTests"
		}
	}

	stage('Build Docker Image') {
		steps{
			//"docker build -t ericharutyunyan1996/currency-exchange-devops:$env.BUILD_TAG"
			script{
				dockerImage = docker.build("docker build -t ericharutyunyan1996/currency-exchange-devops:${env.BUILD_TAG}")
			}
		}
	}

	stage('Push Docker Iamge') {
			steps{
				script{
				docker.withRegistery('','dockerhub'){
				dockerImage.Push();
				dockerImage.push('latest')
				}
			}
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