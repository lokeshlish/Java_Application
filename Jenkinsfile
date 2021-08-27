#!/usr/bin/env groovy


def gv

pipeline {
    agent any
    tools {
        maven 'maven'
    }
    stages {
        stage("init") {
            steps {
                script {
                    gv = load "script.groovy"
                }
            }
        }
        stage("package") {
            steps {
                script {
                    sh 'mvn package'
                }
            }
        }
        stage("dockerLogin") {
            steps {
                script {
                    withCredentials([script.usernamePassword(credentialsId: 'docker', passwordVariable: 'PASS', usernameVariable: 'USER')]) {
                    sh "echo $script.PASS | docker login -u $script.USER --password-stdin"

                }
            }
        }
       
        stage("build") {
            steps {
                script {
                sh 'docker build -t lokeshlish/java_app:1.0.0'
                    
                }
            }
        }
        stage("push") {
            steps {
                script {
                    sh 'docker push lokeshlish/java_app:1.0.0'
                }
            }
        }
        stage("deploy") {
            steps {
                script {
                    gv.deployApp()
                }
            }
        }
    }
}
