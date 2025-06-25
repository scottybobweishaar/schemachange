pipeline {
    agent {
        docker {
            image "python:3.8"
            args '--user 0:0'
        }
    }

    environment {
        SF_OCSP_FAIL_OPEN = 'true'
        PYTHONHTTPSVERIFY = '0'
    }

    stages {
        stage('Run schemachange') {
            steps {
                sh "echo SF_OCSP_FAIL_OPEN=$SF_OCSP_FAIL_OPEN"
                sh "pip install schemachange --upgrade"
                sh "schemachange -f migrations -a ${SF_ACCOUNT} -u ${SF_USERNAME} -r ${SF_ROLE} -w ${SF_WAREHOUSE} -d ${SF_DATABASE} -c ${SF_DATABASE}.SCHEMACHANGE.CHANGE_HISTORY --create-change-history-table"
            }
        }
    }
}