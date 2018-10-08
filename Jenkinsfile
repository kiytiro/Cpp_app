pipeline {
    agent any

    environment {
  //      SONAR_HOST_URL1 = 'http://localhost:9000'
        SONAR_PATH = '/home/labuser/devOPS/sonar-scanner-3.2.0.1227-linux'
        BUILD_WRAPPER = '/home/labuser/devOPS/build-wrapper-3.10/linux-x86-64'
        PYTHON_SCRIPT_PATH = '/home/labuser/pythonScripts'
    }
    stages {

        stage('----compile the C++ code------') {
            steps {
              sh "${BUILD_WRAPPER}/build-wrapper-linux-x86-64 --out-dir bw-outputs ./build.sh"
            }
        }

        stage('----call sonarqube------') {
            steps {
                  sh "${SONAR_PATH}/bin/sonar-scanner"
            }
        }

        stage('----call CheckQualityGate python script------') {
            steps {
               script {
                def props = readProperties file:"${env.SONAR_PATH}/conf/sonar-scanner.properties"

                env.SONAR_HOST_URL = props['sonar.host.url']
                echo "Sonar URL:${SONAR_HOST_URL}"
                echo "Environment:${WORKSPACE}"
              }
     sh "python3 ${PYTHON_SCRIPT_PATH}/CheckSonarQubeQualityGate.py ${WORKSPACE} ${SONAR_HOST_URL} || true"
            }
        }

       stage('----test error code-----') {
            steps {

               echo "Sonar URL:${TEST_ERROR_MKK}"
                echo "Environment:${WORKSPACE}"

            }
        }



    }
}
