node('docker') {
    checkout(scm)

    withEnv(["MYSQL_PORT=${3307 + (env.EXECUTOR_NUMBER ? env.EXECUTOR_NUMBER : 0).toInteger()}"]) {
        // docker.image('mysql:5.6').withRun("-e MYSQL_ROOT_PASSWORD=root -p ${env.MYSQL_PORT}:3306") {
            // sh "mysql -h 127.0.0.1 -P ${env.MYSQL_PORT} -u root -proot --execute='show databases'"
        // }
        docker.image('ruby:2.3').inside('-u root') {
            sh 'ls'
            sh 'ruby --version'
            sh 'apt-get update && apt-get install --yes --force-yes mysql-client-5.6'
            
            // sh "mysql -u root -proot --execute='show databases'"
            sh 'bundle'
        }
    }
}