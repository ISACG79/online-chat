pipeline {
    agent any

    parameters {
        booleanParam(name: 'CLEAN_WORKSPACE', defaultValue: false, description: 'Delete Jenkins map')
        booleanParam(name: 'TESTING_FRONTEND', defaultValue: false, description: 'Testing frontend...')
    }


    environment {
        ON_SUCCESS_SEND_EMAIL = true
        ON_FAILURE_SEND_EMAIL = true
    }

    stages {

        stage("Fetch repository") {
            steps {
                git 'https://github.com/ISACG79/online-chat.git'
            }
        }

        stage("Procesul de Build") {
            steps {
                echo "Build number ${BUILD_NUMBER} and ${BUILD_TAG}"
                bat 'npm install'
            }
        }

        stage("Testing backend") {
            steps {
                echo "TESTING_BACKEND"
                script{
                    TESTING_FRONTEND = true
                }
                bat 'npm test'
            }
        }

        stage("Testing frontend") {
            steps {
                script{
                    if(TESTING_FRONTEND == true){
                        echo "TESTING_FRONTEND"
                    }
                }
            }
        }
    }


    post {
        success {
            echo "I am running because the job ran successfully"
            script {
                ON_SUCCESS_SEND_EMAIL = true
            }
        }

        unstable {
            echo "The build is unstable. Try fix it"
        }

        failure {
            echo "Something happened"
            script {
                ON_SUCCESS_SEND_EMAIL = false
            }
        }

        always {
            echo "Build Tag: ${BUILD_TAG}"


            script {
                if (CLEAN_WORKSPACE == true) {
                    echo 'Deleting BUILD_TAG folder'
                    bat 'rm -rf ${BUILD_TAG}'
                } else {
                    echo 'BUILD_TAG not folder deleted'
                }
            }

        }

    }
}
