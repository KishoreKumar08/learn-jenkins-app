pipeline {
    agent any
    environment {
        FILE_NAME = 'sheeby.txt'
    }

    stages {
        stage('Build') {
            steps {
                cleanWs()
                sh 'echo "hello from my first pipeline in jenkins"'
                sh 'whoami'
		        sh "echo $FILE_NAME"
                sh '''
                    mkdir -p build
                    echo Mainboard >> build/$FILE_NAME
                    cat build/$FILE_NAME
                    echo Display >> build/$FILE_NAME
                    cat build/$FILE_NAME
                    echo Keyboard >> build/$FILE_NAME
                    cat build/$FILE_NAME
                '''
            }
        }
        stage('Test') {
            steps('test') {
                sh '''
                    test -f build/$FILE_NAME
                    grep "Mainboard" build/$FILE_NAME
                    grep "Display" build/$FILE_NAME
                    grep "Keyboard" build/$FILE_NAME
                '''
            }
        }
    }
    post {
        success {
            archiveArtifacts artifacts: 'build/**'
        }
    }
}
