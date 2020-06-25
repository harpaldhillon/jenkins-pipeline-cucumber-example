pipeline{

    agent {
        kubernetes {
            yaml '''
apiVersion: v1
kind: Pod
spec:
  containers:
  - name: shell
    image: mvn
    command:
    - sleep
    args:
    - infinity
'''
            defaultContainer 'mvn'
        }
    }

    stages {

        stage ('Compile Stage') {

            steps {

                    sh 'mvn clean install'


            }
        }
    stage ('Test Stage') {

            steps {

                    sh 'mvn test'

            }
        }


        stage ('Cucumber Reports') {

            steps {
                cucumber buildStatus: "UNSTABLE",
                    fileIncludePattern: "**/cucumber.json",
                    jsonReportDirectory: 'target'

            }

        }

    }

}
