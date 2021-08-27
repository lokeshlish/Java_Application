#!/usr/bin/env groovy
df gv


pipeline {
    agent any
    tools {
        maven 'maven'
    }
    stages {
        stage("build jar") {
            steps {
                script {
                    buildJar 'mvn package'
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



