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
        
      }
    }
    
    stage ("cleanup") {
       steps {
        sh 'mvn clean'
      } 
    }
    
    stage("dev") {
      when {
        expression {
          echo "test for dev branch"
          return true
        }
      }
      
      steps {
        echo "branch=dev"
      }
      
    }
    stage("master") {
      steps {
        echo "branch=Master"
      }
    }
  }
 }
