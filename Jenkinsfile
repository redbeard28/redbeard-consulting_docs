/* Created by Jeremie CUADRADO
 Under GNU AFFERO GENERAL PUBLIC LICENSE
*/

pipeline {
    agent { label 'node2' }


    environment {
        branchName = 'master'
        docker_mkdocs_image = 'redbeard28/docset:0.1'
        DOCSET_NAME = 'redbeard28'
        DOCKER_TCPIP = '10.10.1.212:2376'
    }

    stages{

        stage('Clone the GitHub repo'){

            steps{
                git url: "https://github.com/redbeard28/docset.git", branch: "${branchName}", credentialsId: "jenkins_github_pat"
            }
            post{
                success{
                    echo 'Successfuly clone your repo...'
                }
            }
        }
        stage('Serve HTML doc'){
            /*steps{
                timeout(time:5, unit:'MINUTES'){
                    input message:'Approuve Image Building'
                }
            }*/

            steps{
                script {
                    withDockerServer([uri: "tcp://${DOCKER_TCPIP}"]) {
                        sh "docker run -it --rm -p 8001:8000 ${docker_mkdocs_image}"
                        }
                    }
            }
        }


    }
}