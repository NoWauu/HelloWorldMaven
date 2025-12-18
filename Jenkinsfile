pipeline {
    agent any

    tools {
        maven "M3"
    }

    stages {
        stage('Build') {
            steps {
                // Jenkins automatically checks out code if this file is in SCM,
                // but since you have it explicitly:
                git 'https://github.com/NoWauu/HelloWorldMaven.git'

                sh "mvn -Dmaven.test.failure.ignore=true clean package"
            }

            post {
                success {
                    junit '**/target/surefire-reports/TEST-*.xml'
                    archiveArtifacts 'target/*.jar'
                }
            }
        }

        stage('Tag Release') {
            steps {
                script {
                    // 1. Configure identity LOCALLY for this specific folder
                    sh "git config user.email 'jenkins@example.com'"
                    sh "git config user.name 'Jenkins CI'"

                    // 2. Create the tag (using the Jenkins Build Number)
                    sh "git tag -a build-${env.BUILD_NUMBER} -m 'Build ${env.BUILD_NUMBER} passed tests'"

                    sh "git push origin build-${env.BUILD_NUMBER}"
                }
            }
        }
    }
}
