pipeline {
  agent any
  
  environment {
    RELEASE = false
  }
  
  tools {
    maven "Maven3"
    jdk "JDK7"
  }
  
  options {
    // General Jenkins job properties
    buildDiscarder(logRotator(numToKeepStr:'5'))
    // "wrapper" steps that should wrap the entire build execution
    timestamps()
    timeout(time: 5, unit: 'MINUTES')
  }
  
  
  stages {
    stage("init") {
      steps {
        echo "My branch is: ${env.BRANCH_NAME}"
        
        echo sh(returnStdout: true, script: 'env')
      }
    }
    stage ("build") {
       steps {
        sh 'mvn clean test'
      } 
    }
    
    stage("dev") {
      when {branch "dev"}
      steps {
        echo "branch=dev"
      }
    }

    stage("master") {
      when {branch "master"}
      steps {
        echo "branch=Master"
      }
    }
  }
  post {
    always {
      echo "Hi there"
    }
    changed {
      echo "I'm different"
    }
    success {
      echo "I succeeded"
      archive "**/*"
    }
  }
 }
