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
targetDir="$(cat ./targetDir)"
targetDir+="p1"
echo $targetDir
cat ids.sh $targetDir > tmpScript
chmod 777 tmpScript
bash ./tmpScript
rm ./tmpScript'''
      }
    }

    stage('Sleep') {
      steps {
        sh '''cd /var/lib/jenkins/workspace
targetDir="$(cat ./targetDir)"
targetDir+="interval"
cat ids.sh $targetDir > tmpScript
chmod 777 tmpScript
bash ./tmpScript
rm ./tmpScript'''
      }
    }

    stage('Routing Phase') {
      steps {
        sh '''cd /var/lib/jenkins/workspace
targetDir="$(cat ./targetDir)"
targetDir+="p2"
cat ids.sh $targetDir > tmpScript
chmod 777 tmpScript
bash ./tmpScript
rm ./tmpScript'''
      }
    }

    stage('Clean Up') {
      steps {
        sh '''cd /var/lib/jenkins/workspace
rm ./targetDir'''
      }
    }

  }
}