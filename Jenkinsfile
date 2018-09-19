pipeline {
    agent any
    environment {
    def uploadSpec = """{
     "files": [
      {
          "pattern": "classes/abc/*",
          "target": "generic-local/"
        }
     ]
    }"""
    def downloadSpec = """{
     "files": [
      {
          "pattern": "classes/abc/*",
          "target": "downloads"
        }
     ]
    }"""
    }
    
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
                sh 'mkdir downloads'
                    script
                        {
                        //def server = Artifactory.newServer('http://18.207.229.179:8081/artifactory', 'admin', 'art123')
                        def server = Artifactory.server 'Artifactory_server1'
                        server.bypassProxy = true
                        //def buildInfo = server.upload spec: uploadSpec
                        server.upload(uploadSpec)
                        echo 'Uploaded the file to Jfrog Artifactory successfully"
                        server.download(downloadSpec)
                        echo 'Downloaded the file from Jfrog Artifactory successfully"
                        }
                 /*def uploadSpec = """{
                  "files": [
                    {
                      "pattern": "classes/abc/*",
                      "target": "generic-local/"
                    }
                 ]
                }"""
                server.upload(uploadSpec)*/
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
