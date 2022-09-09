pipeline {
	agent any
	stages {
	    stage("STAGE 2") {
		 steps {
			echo "first step"
			echo "second step"
		 }
		 post {
			always {
				echo "fin stage 1"
			}
		 }
		}
		stage("STAGE 2") {
		 steps {
			echo "first step"
			echo "second step"
		 }
		}
}