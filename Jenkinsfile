pipeline {
    agent any

    stages {

        stage('Checkout Code') {
            steps {
                git branch: 'main',
                    url: 'https://github.com/Vikas-Abhimanyu/spring-boot-demo.git'
            }
        }

        stage('Test') {
            steps {
                sh 'mvn clean test'
            }
        }

        stage('Build') {
            steps {
                sh 'mvn clean package -DskipTests'
            }
        }

        stage('Deploy') {
            steps {
                sh '''
                if pgrep -f "demo-0.0.1-SNAPSHOT.jar" > /dev/null; then
                    pkill -f "demo-0.0.1-SNAPSHOT.jar"
                    echo "App was running and has been killed"
                else
                    echo "App is not running"
                fi

                JENKINS_NODE_COOKIE=dontKillme \
                nohup java -jar target/demo-0.0.1-SNAPSHOT.jar > app.log 2>&1 &
                '''
            }
        }
    }
}

