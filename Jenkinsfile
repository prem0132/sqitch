pipeline {
    options {
      timeout(time: 2, unit: 'HOURS') 
  }
  agent {
    docker {
      image 'premhashmap/sqitch'
      args '-u root -v /var/run/docker.sock:/var/run/docker.sock'
    }
  }
  stages {
    stage('Build') {
        steps {
            echo 'Building..'
        }
    }
    stage('docker build'){
        sh 'cd ./dev'
        sh 'docker build -t premhashmap/sqitch:snowflake ../ -f Dockerfile'
    }
    stage('docker push'){
        withCredentials([string(credentialsId: 'dockerhubPWD', variable: 'dockerpwd')]) {
            sh 'docker login -u premhashmap -p ${dockerpwd}'
        }
        sh 'docker push premhashmap/sqitch:snowflake'
    }
  }     
}
