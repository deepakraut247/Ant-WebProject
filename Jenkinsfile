pipeline
{

agent any
stages

{ 
    stage ('scm checkout')
    {
        steps { git branch: 'master', url: 'https://github.com/deepakraut247/Ant-WebProject' }
    }

    stage ('ant-prepare-target')
    {
        steps { withAnt(installation: 'ANT_HOME', jdk: 'JAVA_HOME') 
        {
          sh 'ant prepare'
        }     }
    }

    stage ('ant-init-target')
    {
        steps 
         { withAnt(installation: 'ANT_HOME', jdk: 'JAVA_HOME') 
           {
               sh 'ant init'
           }  }
    }

}


}
