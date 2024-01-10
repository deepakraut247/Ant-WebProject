pipeline
{

agent any
    /*
environment{
SONARQUBE_SCANNER_HOME=tool 'sonar-scanner'
}  */
stages

{ 
    stage ('scm checkout')
    {
        steps { git branch: 'master', url: 'https://github.com/deepakraut247/Ant-WebProject' }
    }
/*
    stage('Run Sonar')
    {
    steps{
        script{
            withSonarQubeEnv('sonar-api'){
                sh "${SONARQUBE_SCANNER_HOME}/bin/sonar-scanner -X"
            }
        }
    }
}
*/
    stage ('ant-prepare-target')
    {
        steps { withAnt(installation: 'ANT_HOME') 
        {
          sh 'ant prepare'
        }     }
    }

    stage ('ant-init-target')
    {
        steps 
         { withAnt(installation: 'ANT_HOME') 
           {
               sh 'ant init'
           }  }
    }
    
stage('Package') {
            steps {
                rtServer (
                    id: "artifactory",
                    url: "http://10.10.2.72:8082/artifactory",
                    username: 'admin',
                    password: 'Amazon@123',
                    bypassProxy: true,
                    timeout: 300
                )
            }
        }
        stage('Upload') {
            steps {
                rtUpload (
                    serverId: "artifactory",
                    spec: '''{
                        "files": [
                            {
                                "pattern": "*.war",
                                "target": "generic_local/"
                            }
                        ]
                    }'''
                )
            }
        }
        stage('Publish Build Info') {
            steps {
                rtPublishBuildInfo (
                    serverId: "artifactory"
                )
            }
        }

}
}
