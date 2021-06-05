pipeline{
  agent any

  stages{
    stage('Maven Build'){
      steps{
        sh "mvn clean package"
      }
    }

    stage('Upload To Nexus'){
      steps{
        script{
          def pom = readMavenPom file: 'pom.xml'
          def repository = pom.version.endsWith("SNAPSHOT") ? 'shaikmoula-devops-snapshot' : 'shaikmoula-devops'
          nexusArtifactUploader artifacts: 
          [[artifactId: 'myweb', classifier: '', file: "target/myweb-${pom.version}.war", type: 'war']], 
          credentialsId: 'nexus3', 
          groupId: 'in.shaikmoula123', 
          nexusUrl: '172.31.20.251', 
          nexusVersion: 'nexus3', protocol: 'http', 
          repository: repository, 
          version: pom.version
        }
      }
    }
    
    stage('dev-deploy'){
      steps{
        echo "deploy to dev environment"
      }
    }

    stage('uat-deploy'){
      steps{
        echo "deploy to uat environment"
      }
    }

    stage('prd-deploy'){
      steps{
        // How do you get latest artifact from nexus?
        echo "deploy to prod environment"
      }
    }
  }
}
