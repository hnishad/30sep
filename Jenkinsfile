#!/usr/bin/env groovy
node{
    stage('Git Checkout'){
        git 'https://github.com/hnishad/DevOpsClassCodes.git'
    }
    stage('Compile'){
        withMaven(maven:'MyMaven'){
            sh 'mvn compile'
        }
        
    }
    stage('Test'){
        withMaven(maven:'MyMaven'){
            try{
                sh 'mvn test'
            }finally {
                junit 'target/surefire-reports/*.xml'
            }
        }
    }
    stage('Package'){
        withMaven(maven:'MyMaven'){
            sh 'mvn package'
        }
    }
}
