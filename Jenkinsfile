pipeline {
    agent any
    tools { 
        maven 'MAVEN_3_6_3' 
        jdk 'JDK_17_0_2'
    }
	
    stages {
        stage ('Compile Stage 2022-01') {

            steps {
                withMaven(maven : 'MAVEN_3_6_3') {
                    bat 'mvn clean compile'
                }
            }
        }

        stage ('Testing Stage 2022-01') {

            steps {
                withMaven(maven : 'MAVEN_3_6_3') {
                    bat 'mvn test'
                }
            }
        }


        stage ('package Stage') {
            steps {
                withMaven(maven : 'MAVEN_3_6_3') {
                    bat 'mvn package'
                }
            }
        }

		stage('Deploy tomcat') {
            steps {
                echo "Running ${env.BUILD_ID} on ${env.JENKINS_URL} direcion ${env.WORKSPACE}"
                withMaven(maven : 'MAVEN_3_6_3') {
					bat '"C:\\Program Files\\Git\\mingw64\\bin\\curl.exe" -T ".\\target\\sistema-ventas-spring.war" "http://tomcat:tomcat@localhost:8080/manager/text/deploy?path=/sistema-ventas-spring&update=true"'
                }
            }
        }

    }
}
