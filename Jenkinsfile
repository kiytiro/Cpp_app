pipeline {
    agent any

    environment {
        SONAR_PATH = '/home/labuser/devOPS/sonar-scanner-3.2.0.1227-linux/bin'
        SOURCE_CODE = '/home/labuser/devOPS/sonar-scanning-examples-master_Jenkins/sonarqube-scanner-build-wrapper-linux'
        BUILD_WRAPPER = '/home/labuser/devOPS/build-wrapper-3.10/linux-x86-64'
    }
    stages {
            
        stage('----compile the C++ code------') {
            steps {
     //           sh "cd /home/labuser/devOPS/sonar-scanning-examples-master_Jenkins/sonarqube-scanner-build-wrapper-linux"
                sh "/home/labuser/devOPS/build-wrapper-3.10/linux-x86-64/build-wrapper-linux-x86-64 --out-dir bw-outputs ./build.sh"

            }
        }

        stage('----call sonarqube------') {
            steps {
                sh "cd /devOPS/sonar-scanning-examples-master_Jenkins/sonarqube-scanner-build-wrapper-linux"
                sh "/home/labuser/devOPS/sonar-scanner-3.2.0.1227-linux/bin/sonar-scanner"

            }
        }


    }

}
