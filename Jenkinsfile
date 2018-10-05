pipeline {
    agent any
//    def props = readProperties file:'/home/labuser/devOPS/sonar-scanner-3.2.0.1227-linux/conf/sonar-scanner.properties'
//    def sonar_url =  props['sonar.host.url']

//    environment {
//
//        SONAR_HOST_URL = "${sonar_url}"
//        SONAR_PATH = '/home/labuser/devOPS/sonar-scanner-3.2.0.1227-linux/bin'
//        SOURCE_CODE = '/home/labuser/devOPS/sonar-scanning-examples-master_Jenkins/sonarqube-scanner-build-wrapper-linux'
//        BUILD_WRAPPER = '/home/labuser/devOPS/build-wrapper-3.10/linux-x86-64'
//:    }
    stages {

        stage('----get the sonarqube host url------') {
            steps {
  script {
//              def props = readProperties file:'/home/labuser/devOPS/sonar-scanner-3.2.0.1227-linux/conf/sonar-scanner.properties'
//            def sonar_url =  props['sonar.host.url']
    environment {
        props = readProperties file:'/home/labuser/devOPS/sonar-scanner-3.2.0.1227-linux/conf/sonar-scanner.properties'

//        SONAR_HOST_URL = "${sonar_url}"
        SONAR_HOST_URL = ${props['sonar.host.url']}
        SONAR_PATH = '/home/labuser/devOPS/sonar-scanner-3.2.0.1227-linux/bin'
        SOURCE_CODE = '/home/labuser/devOPS/sonar-scanning-examples-master_Jenkins/sonarqube-scanner-build-wrapper-linux'
        BUILD_WRAPPER = '/home/labuser/devOPS/build-wrapper-3.10/linux-x86-64'
    }
}

            }
        }

            
        stage('----compile the C++ code------') {
            steps {
     //           sh "cd /home/labuser/devOPS/sonar-scanning-examples-master_Jenkins/sonarqube-scanner-build-wrapper-linux"
                sh "/home/labuser/devOPS/build-wrapper-3.10/linux-x86-64/build-wrapper-linux-x86-64 --out-dir bw-outputs ./build.sh"

            }
        }

        stage('----call sonarqube------') {
            steps {
                sh "/home/labuser/devOPS/sonar-scanner-3.2.0.1227-linux/bin/sonar-scanner"

            }
        }
        stage('----call CheckQualityGate python script------') {
            steps {
 //              script {
//                def props = readProperties file:'/home/labuser/devOPS/sonar-scanner-3.2.0.1227-linux/conf/sonar-scanner.properties'
//                def sonar_url = props['sonar.host.url']
                echo "Sonar URL:${SONAR_HOST_URL}"
                echo "Environment:${WORKSPACE}"
              //  sh "python3 /home/labuser/pythonScripts/CheckSonarQubeQualityGate.py ${WORKSPACE} ${sonar_url}"
//              }
              sh "python3 /home/labuser/pythonScripts/CheckSonarQubeQualityGate.py ${WORKSPACE} ${SONAR_HOST_URL}"

            }
        }
    }
}
