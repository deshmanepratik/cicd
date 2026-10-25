
pipeline {
    agent any

    options {
        timestamps()
        disableConcurrentBuilds()
    }

    stages {
        stage('Validate Branch') {
            steps {
                script {
                    def branch = env.BRANCH_NAME ?: ''

                    if (!(branch == 'main' ||
                          branch ==~ /^feature\/.+$/ ||
                          branch ==~ /^release\/.+$/)) {
                        error("Build not allowed for branch: ${branch}")
                    }

                    echo "Building allowed branch: ${branch}"
                }
            }
        }

        stage('Checkout') {
            steps {
                checkout scm
                echo "Build URL is ${env.BUILD_URL}"
                echo "Build Number is ${env.BUILD_NUMBER}"
                echo "testing."
            }
        }

        stage('Build') {
            steps {
                echo 'Starting build...'
                sh 'echo "Replace with your build command"'
            }
        }

        stage('Test') {
            steps {
                echo 'Running tests...'
                sh 'echo "Replace with your test command"'
            }
        }

        stage('Package') {
            steps {
                echo 'Packaging application...'
                sh 'echo "Replace with your packaging command"'
            }
        }

        stage('Deploy') {
            when {
                anyOf {
                    branch 'main'
                    branch pattern: 'release/.+', comparator: 'REGEXP'
                }
            }
            steps {
                echo 'Run your authorized deployment steps here.'
            }
        }
    }

    post {
        success {
            echo 'Pipeline completed successfully.'
        }
        failure {
            echo 'Pipeline failed. Check the stage logs.'
        }
        always {
            echo "Finished processing branch: ${env.BRANCH_NAME}"
        }
    }
}