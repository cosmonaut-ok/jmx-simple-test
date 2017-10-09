def sendToChoices = ['alice@xy.com', 'bob@xy.com', 'somelist@xy.com'].join('\n')
def userInput = input(message: 'Deploy this build to production?',
		      ok: 'Yes deploy now!',
		      parameters: [choice(choices: sendToChoices, name: 'SEND_EMAIL_TO')]
		      )

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

