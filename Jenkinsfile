pipeline {

    agent any

    parameters {
        string(name: 'REPO_NAME', defaultValue: '', description: 'Name of the repository triggering the pipeline')
    }

    stages {

        stage('Checkout Repositories') {
            steps {
                echo "Checking out the source code from the repository: ${params.REPO_NAME}"

                script {
                    if (params.REPO_NAME == 'Iac_Terraform') {
                        dir('Iac_Terraform') {
                            echo "Triggered by ${params.REPO_NAME} repository - checking out staging branch"
                            git branch: 'staging', url: 'https://github.com/DevOpsGroupL1/Iac_Terraform'
                        }
                    } else if (params.REPO_NAME == 'Front-end') {
                        dir('Front-end') {
                            echo "Source code from ${params.REPO_NAME} repository - staging branch"
                            git branch: 'staging', url: 'https://github.com/DevOpsGroupL1/Front-end'
                        }   
                    } else if (params.REPO_NAME == 'Devop7303') {
                        dir('Devop7303') {
                            echo "Source code from ${params.REPO_NAME} repository -  staging branch"
                            git branch: 'staging', url: 'https://github.com/DevOpsGroupL1/Devop7303'
                        } 
                    }
                }
            }
        }

        stage('Install dependencies') {
            steps {
                echo "Installing dependencies for ${params.REPO_NAME}"

                script {
                    if (params.REPO_NAME == 'Front-end') {
                        dir('Front-end') {
                            echo 'Installing dependencies for Frontend'
                            sh 'yarn install'
                        }
                    } else if (params.REPO_NAME == 'Devop7303') {
                        dir('Devop7303') {
                            echo 'Installing dependencies for Java springboot Devop7303'
                        }
                    }
                }
            }
        }

        stage('Test') {
            steps {
                echo "Running tests for ${params.REPO_NAME}"

                script {
                    if (params.REPO_NAME == 'Front-end') {
                        dir('Front-end') {
                            echo 'Running tests for Frontend'
                        }
                    } else if (params.REPO_NAME == 'Devop7303') {
                        dir('Devop7303') {
                            echo 'Running tests for Java springboot Devop7303'
                        }
                    }
                }
            }
        }

        stage('Quality Assurance gate') {
            steps {
                echo "Running SonarQube analysis for ${params.REPO_NAME}"

                script {
                    if (params.REPO_NAME == 'Front-end') {
                        dir('Front-end') {
                            echo 'Running SonarQube analysis for Frontend'
                        }
                    } else if (params.REPO_NAME == 'Devop7303') {
                        dir('Devop7303') {
                            echo 'Running SonarQube analysis for Java springboot Devop7303'
                        }
                    }
                }
            }
        }

        // stage('Build docker image') {
        //     steps {
        //         echo 'Building docker image'
        //         sh 'docker build -t groupone -f Docker/Dockerfile.prod .'
        //     }
        // }

        // stage('Deploy docker image to docker hub registry') {
        //     steps {
        //         echo 'Deploying docker image to docker hub'
        //         withCredentials([usernamePassword(credentialsId: "${DOCKER_REGISTRY_CREDS}", passwordVariable: 'DOCKER_PASSWORD', usernameVariable: 'DOCKER_USERNAME')]) {

        //             sh 'echo \$DOCKER_PASSWORD | docker login -u \$DOCKER_USERNAME --password-stdin docker.io'

        //             sh 'docker tag groupone hardarmyyy/groupone:latest'
        //             sh 'docker push hardarmyyy/groupone:latest'

        //         }
        //     }
        // }

    }

    post {
        
        always {
            // echo 'logging out of docker hub'
            // sh 'docker logout'
        }

        success {
            echo 'Build successful! Archiving new build artifacts.'
            archiveArtifacts artifacts: '**', allowEmptyArchive: true
            cleanWs()
        }

        failure {
            echo 'Build failed. Check the logs for details.'
            cleanWs()
        }

    }

}
