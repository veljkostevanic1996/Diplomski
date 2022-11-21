pipeline {
    agent any

    environment {
        jobs = getJobs()
    }

    stages {
        stage('triger build') {
            steps {
                script {
                    def comm = readJSON text: "$commits"
                    echo comm.toString()
                    //def msg = readJSON text: "$commits[0].message"
                    def msg = "$comm_message"
                    echo msg
                    jobs.each {
                        echo it
                        if (msg.contains(it)) {
                            echo "contains !${it}"
                            build job: it, parameters: [[$class: 'StringParameterValue', name: 'BRANCH', value: "master"],
                            [$class: 'StringParameterValue', name: 'REF', value: "$ref"]]
                        }
                    }

                }

            }
        }
    }
}

def getJobs() {
    return ['test']
}
