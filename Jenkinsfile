def app

pipeline {
  agent{
    label 'ansible'
  }
  stages{
    stage('Clone repository'){
      checkout scm
    }
    stage('Build image'){
      app = docker.build('.')
    }
    stage('Test image'){
      app.inside{
        sh 'echo "Tests passes"'
      }
    }
    stage('Push image'){
       docker.withRegistry('https://hub.docker.com/r/khanabid20/hello-world', 'khanabid20-git-repo-creds'){
          app.push("$(env.BUILD_NUMBER)")
          app.push("latest")
       }
    }
  }

}
