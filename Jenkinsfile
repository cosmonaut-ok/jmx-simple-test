properties([parameters([choice(choices: ['integration', 'QA', 'staging', 'production'], description: 'Choose environment to perform tests', name: 'ENVIRONMENT')]), pipelineTriggers([])])

node('chef') {
    properties([parameters([choice(choices: ['integration', 'QA', 'staging', 'production'], description: 'Choose environment to perform tests', name: 'ENVIRONMENT')]), pipelineTriggers([])])
    checkout scm
        if (env.BRANCH_NAME == 'master') {
            stage('Deploy') {
                sh '/bin/bash ./apache-jmeter-3.1-TC/bin/jmeter.sh -n -t "./JMX_plans/Ingenico/Ingenico_QA_AHUK.jmx" -l test.log -e -o report_AHUK_${ENVIRONMENT}'
                sh 'zip -r report_AHUK_${ENVIRONMENT}.zip report_AHUK_${ENVIRONMENT}'
                    }
            stage('Post Report') {
                perfReport 'report_AHUK_${ENVIRONMENT}.zip'
                    }

        }
}

