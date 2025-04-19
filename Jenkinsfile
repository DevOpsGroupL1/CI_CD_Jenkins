def repoName = ''
def branchName = ''

pipeline {

    agent any

    stages {

        stage('Initialize variables') {
            steps {
                script {
                    repoName = env.GIT_URL?.tokenize('/').last()?.replace('.git', '')
                    branchName = env.GIT_BRANCH?.replaceFirst(/^origin\//, '')
                }
            }
        }

        stage('Checkout Repositories') {
            when {
                expression {
                    return branchName == 'staging'
                }
            }
            steps {
                script {
                    if (repoName == 'Iac_Terraform') {
                        echo "Checking out the source code from the repository: ${repoName} - branch: ${branchName}"
                        dir('Iac_Terraform') {
                            checkout scm
                        }
                    } else if (repoName == 'Front-end') {
                        echo "Checking out the source code from the repository: ${repoName} - branch: ${branchName}"
                        dir('Front-end') {
                            checkout scm
                        }  
                    } else if (repoName == 'Devop7303') {
                        echo "Checking out the source code from the repository: ${repoName} - branch: ${branchName}"
                        dir('Devop7303') {
                            checkout scm
                        }
                    } else if (repoName == 'CI_CD_Jenkins') {
                        echo "Checking out the source code from the repository: ${repoName} - branch: ${branchName}"
                        dir('CI_CD_Jenkins') {
                            checkout scm
                        }
                    }
                }
            }
        }

        stage('Install dependencies') {
            steps {
                script {
                    if (repoName == 'Iac_Terraform') {
                        dir('Iac_Terraform') {
                            echo 'Installing dependencies for Iac_Terraform'
                            // sh 'terraform init'
                        }
                    } else if (repoName == 'Front-end') {
                        dir('Front-end') {
                            echo 'Installing dependencies for Frontend'
                            sh 'yarn install'
                        }
                    } else if (repoName == 'Devop7303') {
                        dir('Devop7303') {
                            echo 'Installing dependencies for Java springboot Devop7303'
                        }
                    }
                }              
            }
        }

        stage('Test') {
            steps {
                script {
                    if (repoName == 'Front-end') {
                        dir('Front-end') {
                            echo 'Running tests for Frontend'
                        }
                    } else if (repoName == 'Devop7303') {
                        dir('Devop7303') {
                            echo 'Running tests for Java springboot Devop7303'
                        }
                    }
                }
            }
        }

        // stage('Quality Assurance gate') {
        //     steps {
        //         echo "Running SonarQube analysis for ${params.REPO_NAME}"

        //         script {
        //             if (params.REPO_NAME == 'Front-end') {
        //                 dir('Front-end') {
        //                     echo 'Running SonarQube analysis for Frontend'
        //                 }
        //             } else if (params.REPO_NAME == 'Devop7303') {
        //                 dir('Devop7303') {
        //                     echo 'Running SonarQube analysis for Java springboot Devop7303'
        //                 }
        //             }
        //         }
        //     }
        // }

        // stage('Provison Terraform') {
        //     steps {
        //         script {
        //             if (repoName == 'Iac_Terraform') {
        //                 dir('Iac_Terraform') {
        //                     echo 'Provisioning Terraform'
        //                 }
        //             }
        //         }
        //     }
        // }

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
