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
    
    stage ("cleanup") {
       steps {
        sh 'mvn clean'
      } 
    }
    stage ("PR"){
      when {env.BRANCH_NAME.startsWith('PR-')}
       steps {
        echo "PULL REQUEST"
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
 }
