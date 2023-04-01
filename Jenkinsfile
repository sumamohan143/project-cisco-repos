pipeline {
    agent any
    parameters {
        string(name: 'Number', defaultValue: '2', description: 'Enter a number')
    }
    stages {
        stage('Check if number is prime') {
            steps {
                sh '''
                    #!/bin/bash
                    # Get the input number from the Jenkins job parameter
                    num=$Number
                    # Check if the number is a prime number
                    is_prime=true
                    if [ $num -le 1 ]; then
                        is_prime=false
                    else
                        for ((i=2; i<=num/2; i++)); do
                            if [ $((num%i)) -eq 0 ]; then
                                is_prime=false
                                break
                            fi
                        done
                    fi
                    # Print the result
                    if [ $is_prime = true ]; then
                        echo "$num is a prime number."
                        echo "<html><body><h1>The number $num is a prime number</h1></body></html>" > result.html
                    else
                        echo "$num is not a prime number."
                        echo "<html><body><h1>The number $num is not a prime number</h1></body></html>" > result.html
                    fi
                '''
            }
        }
        stage('Publish HTML file') {
            steps {
                archiveArtifacts artifacts: 'result.html'
            }
        }
        stage('Print the Date') {
            steps {
                sh 'date'
            }
        }
    }
 
    post {
     success {
       emailext (
        subject: "Prime number result",
        body: "Please find attached the prime number result.",
        attachmentsPattern: "result.html",
        to: "mohan.ram1806@gmail.com",
        attachLog: true
      )
    }
    }
}
