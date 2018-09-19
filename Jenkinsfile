def server = Artifactory.newServer('artifactory-url', 'username', 'password')

pipeline {
    agent any

    stages {
        stage('Build') {
            steps {
                echo 'Building..'
                sh 'ant -f build.xml run'
            }
        }
        stage('Test') {
            steps {
                echo 'Testing..'
                 def uploadSpec = """{
                  "files": [
                    {
                      "pattern": "classes/abc/*",
                      "target": "classes/abc/"
                    }
                 ]
                }"""
                server.upload(uploadSpec)
            }
        }
        stage('Deploy') {
            steps {
                echo 'Deploying....'
                mail body: 'project build successful for job named testpipeline-1',
                from: 'krk835900@gmail.com',
                subject: 'project build successful',
                to: 'krk835900@gmail.com'
            }
        }
    }
}
