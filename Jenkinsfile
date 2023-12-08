pipeline
{

agent any
environment{
SONARQUBE_SCANNER_HOME=tool 'sonar-scanner'
}
stages

{ 
    stage ('scm checkout')
    {
        steps { git branch: 'master', url: 'https://github.com/deepakraut247/Ant-WebProject' }
    }

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

}


}
