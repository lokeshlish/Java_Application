#!/usr/bin/env groovy

library identifier: 'Jenkins_Library@main', retriever: modernSCM(
        [$class: 'GitSCMSource',
         remote: 'https://github.com/lokeshlish/Jenkins_Library.git',
         credentialsId: 'git'
        ]
)_


pipeline {
    agent any
    tools {
        maven 'maven'
    }
    stages {
        stage("build jar") {
            steps {
                script {
                    buildJar(mvn package)
                }
            }
        }
        stage("build and push image") {
            steps {
                script {
                    buildImage 'lokeshlish/java_app:jma-3.0'
                    dockerLogin(docker)
                    dockerPush 'lokeshlish/java_app:jma-3.0'
                }
            }
        }
        stage("deploy") {
            steps {
                script {
                    echo 'deploying image'
                }
            }
        }
    }
}



