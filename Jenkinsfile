node('chef') {
    checkout scm

    def EnvironmentChoices = [ 'integration', 'QA', 'staging', 'production' ].join('\n')
    def userInput = input(message: 'On which environment performance tests should be launched?',
    			      ok: 'Deploy now!',
			      parameters: [choice(choices: EnvironmentChoices, name: 'Environment')]
			      )
	    stage('Deploy') {
		sh '/bin/bash ./apache-jmeter-3.1-TC/bin/jmeter.sh -n -t "./JMX_plans/Ingenico/Ingenico_${userInput}_AHUK.jmx" -l test.log -e -o report_AHUK_${userInput}'
		    }
	    stage('Post Report') {
		perfReport 'report_AHUK_${userInput}'
		    }

}

