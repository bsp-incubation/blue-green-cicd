pipeline {
  agent any
  stages {
    stage('Traffic Check') {
      steps {
        sh '''cd /var/lib/jenkins/workspace
cat ids.sh router > tmpScript
chmod 777 tmpScript
bash ./tmpScript
rm ./tmpScript'''
      }
    }

    stage('Deploy Phase') {
      steps {
        sh '''cd /var/lib/jenkins/workspace
targetDir="$(cat ./targetDir)p1"
echo $targetDir
cat ids.sh $targetDir > p1Script
chmod 777 p1Script
bash ./p1Script
'''
      }
    }

    stage('Sleep') {
      steps {
        sh '''cd /var/lib/jenkins/workspace
targetDir="$(cat ./targetDir)interval"
cat ids.sh $targetDir > intervalScript
chmod 777 intervalScript
bash ./intervalScript'''
      }
    }

    stage('Routing Phase') {
      steps {
        sh '''cd /var/lib/jenkins/workspace
targetDir="$(cat ./targetDir)p2"
cat ids.sh $targetDir > p2Script
chmod 777 p2Script
bash ./p2Script'''
      }
    }

    stage('Clean Up') {
      steps {
        sh '''cd /var/lib/jenkins/workspace
rm ./targetDir
rm ./p1Script
rm ./intervalScript
rm ./p2Script'''
      }
    }

  }
}