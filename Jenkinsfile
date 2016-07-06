node('docker') {
    checkout(scm)
    def projectName = "${env.EXECUTOR_NUMBER}"

    try {
        sh "docker-compose -p $projectName up -d"

        sh """
            docker-compose -p $projectName run web bash -c "
                ruby --version
                pwd
                ls
                bundle install --quiet --frozen
                bundle exec rake default[db,'']
            "
        """
    } finally {
        sh "docker-compose -p $projectName down --rmi local"
    }
}