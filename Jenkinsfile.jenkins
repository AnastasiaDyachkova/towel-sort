pipeline {
  agent any

  tools {nodejs "node"}

  stages {
    stage('Clonning Git') {
        steps {
            git 'https://github.com/AnastasiaDyachkova/towel-sort'
        }
    } 
            
    stage('Build') {
      steps {
        bat 'npm install'
      }
    }

    stage('Test') {
      steps {
        bat 'npm test'
      }
    }

    stage('Archive'){
                steps{
			dir('C:\\'){
				echo "Current build: ${BUILD_NUMBER}"
				zip zipFile: "${BUILD_NUMBER}.zip", archive:false, dir: 'ProgramData\\Jenkins\\.jenkins\\workspace\\job'
				archiveArtifacts artifacts: "${BUILD_NUMBER}.zip"
			}
		  }
    }

    stage('Deploy'){
		  steps{
			  dir('C:\\'){
				  script{
					  try
					  {
						  bat("md C:\\Deploy\\")
					  }catch(Exception e){}
				  }
				  unzip zipFile: "${BUILD_NUMBER}.zip", dir: 'C:\\Deploy'
			  }
		  }
	  }
  }
}
