pipeline {
    agent any
    parameters {
        string(name: 'VERSION', defaultValue: '1.0', description: 'version to deploy on prod')
        choice(name: 'VERSION1', choices: ['1.1.0', '1.2.0', '1.3.0'])
        booleanParam(name: 'executeTests', defaultValue: true)
    }
    // tools{
    //     maven 'Maven 3.8.6'
    // }
    environment {
        NEW_VERSION = '1.3.0'
        SERVER_CREDENTIAS = credentials('server-credentials') // credentialID from jendins server 
    }
    stages {
        stage("build") {
            when {
                expression {
                    BRANCH_NAME == 'dev' && CODE_CHANGE == true
                }
            }
            steps {
                echo "building the application version ${NEW_VERSION}"
            }
        }
        stage("test") {
            when {
                expression {
                    params.executeTests
                }
            }
            steps {
                echo 'testing the application...'
            }
        }
        stage("deploy") {
            steps {
                echo "deploying the application...${params.VERSION}"
                withCredentials([
                    usernamePassord(credentials: 'server-credentials', usernameVariable: USER, passwordVariable: PWD)
                ]){
                   sh "some script ${USER} ${PWD}" 
                }
            }
        }
    }
}