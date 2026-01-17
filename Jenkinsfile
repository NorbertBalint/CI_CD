pipeline {
	 environment {
        GIT_REPO = 'http://github.com/NorbertBalint/MyApp.git'
		BRANCH="main"
    }
	
    agent any
        stages {
			stage('Clone') {
				steps {
					echo "Cleanup on ${WORKSPACE}..."
					cleanWs()
					
					echo "GIT checkout branch ${env.BRANCH} into ${WORKSPACE}..."
					git url: "${env.GIT_REPO}", branch: "${env.BRANCH}"
				}
			}
            stage('Build APK') {
				steps {
					sh 'chmod +x ./gradlew'
					sh './gradlew clean assembleDebug'
				}
			}
			stage('Archive APK') {
				steps {
					archiveArtifacts artifacts: '**/*.apk', fingerprint: true
				}
			}
	}
}