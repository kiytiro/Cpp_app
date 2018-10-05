pipeline {
    agent any

    environment {
        SONAR_PATH = '/home/labuser/devOPS/sonar-scanner-3.2.0.1227-linux/bin'
        BUILD_WRAPPER = '/home/labuser/devOPS/build-wrapper-3.10/linux-x86-64'
        PYTHON_SCRIPT_PATH = '/home/labuser/pythonScripts'
    }
    stages {

            
        stage('----compile the C++ code------') {
            steps {
//                sh "/home/labuser/devOPS/build-wrapper-3.10/linux-x86-64/build-wrapper-linux-x86-64 --out-dir bw-outputs ./build.sh"

              sh "${BUILD_WRAPPER}/build-wrapper-linux-x86-64 --out-dir bw-outputs ./build.sh"
            }
        }

        stage('----call sonarqube------') {
            steps {
//                sh "/home/labuser/devOPS/sonar-scanner-3.2.0.1227-linux/bin/sonar-scanner"
                  sh "${SONAR_PATH}/sonar-scanner"

            }
        }
        stage('----call CheckQualityGate python script------') {
            steps {
               script {
                def props = readProperties file:'/home/labuser/devOPS/sonar-scanner-3.2.0.1227-linux/conf/sonar-scanner.properties'
                def SONAR_HOST_URL = props['sonar.host.url']
                echo "Sonar URL:${SONAR_HOST_URL}"
                echo "Environment:${WORKSPACE}"
//         sh "python3 /home/labuser/pythonScripts/CheckSonarQubeQualityGate.py ${WORKSPACE} ${SONAR_HOST_URL}"
                 sh "python3 ${PYTHON_SCRIPT_PATH}/CheckSonarQubeQualityGate.py ${WORKSPACE} ${SONAR_HOST_URL}"
              }
          //    sh "python3 ${PYTHON_SCRIPT_PATH}/CheckSonarQubeQualityGate.py ${WORKSPACE} ${SONAR_HOST_URL}"

            }
        }
    }
}
