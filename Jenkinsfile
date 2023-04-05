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
	stages{
	stage('Build') {
		steps{
			echo "Build"
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