pipeline {
    agent { docker { image 'openjdk' } }
    stages {
        stage('Build') {
            steps {
                checkout scm
                sh 'javac -d target -sourcepath src/main/java src/main/java/com/example/math/Calculator.java'
            }
        }
        stage('Test') {
            steps {
                sh 'javac -d target -cp target:junit-platform-console-standalone-1.4.0.jar src/test/java/com/example/math/TestCalculator.java'
                sh 'java -jar junit-platform-console-standalone-1.4.0.jar --class-path target --scan-class-path --reports-dir=target/surefire-reports/'
            }
        }
    }
    post {
         always {
                junit 'target/surefire-reports/*.xml'
         }
    }
}
