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
    stage('Review'){
        withMaven(maven:'MyMaven'){
            sh "pmd canComputeNew: false, defaultEncoding: '', healthy: '', pattern: 'target/pmd.xml', unHealthy: ''"
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
    stage('Coverage'){
        withMaven(maven:'MyMaven'){
            sh "cobertura autoUpdateHealth: false, autoUpdateStability: false, coberturaReportFile: 'target/site/cobertura/coverage.xml', conditionalCoverageTargets: '70, 0, 0', failUnhealthy: false, failUnstable: false, lineCoverageTargets: '80, 0, 0', maxNumberOfBuilds: 0, methodCoverageTargets: '80, 0, 0', onlyStable: false, sourceEncoding: 'ASCII', zoomCoverageChart: false"
        }
        
    }
    stage('Package'){
        withMaven(maven:'MyMaven'){
            sh 'mvn package'
        }
    }
}
