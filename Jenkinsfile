pipeline {
  agent any
  stages {

        stage('AWS Credentials') {
            steps {
                // Example AWS credentials
                withCredentials(
                [[
                    $class: 'AmazonWebServicesCredentialsBinding',
                    accessKeyVariable: 'AWS_ACCESS_KEY_ID',
                    credentialsId: 'jenkinsforaws',  // ID of credentials in Jenkins
                    secretKeyVariable: 'AWS_SECRET_ACCESS_KEY'
                ]]) {
                     sh """
                            mkdir -p ~/.aws
                            echo "[default]"  >~/.aws/credentials
                            echo "[default]"  >~/.boto
                            echo "AWS_ACCESS_KEY_ID=${AWS_ACCESS_KEY_ID}"  >>~/.boto
                            echo "AWS_SECRET_ACCESS_KEY=${AWS_SECRET_ACCESS_KEY}"  >>~/.boto
                            echo "AWS_ACCESS_KEY_ID=${AWS_ACCESS_KEY_ID}"  >>~/.aws/credentials
                            echo "AWS_SECRET_ACCESS_KEY=${AWS_SECRET_ACCESS_KEY}"  >>~/.aws/credentials
                        """
                }
            }
        }

        stage('Create EC2 instance') {
            steps {
              ansiblePlaybook playbook: 'main.yaml', inventory: 'inventory'
            }
        }

  // stage('Build') {
  //   steps {
  //     sh 'echo "Hello world"'
  //   }
  // }

    // stage('Lint HTML') {
    //   steps {
    //     sh 'tidy -q -e *.html'
    //   }
    // }

    // stage('Upload to AWS') {
    //   steps {
    //     withAWS(region: 'us-east-2', credentials: 'jenkinsforaws') {
    //       s3Upload(bucket: 'jenkinsbuckets', includePathPattern: '**/*')
    //     }
    //   }
    // }

    // stage('Build image') {
    //     /* This builds the actual image; synonymous to
    //      * docker build on the command line */
    // steps{

    // }
    // }


    // stage('Scan') {
    // steps{
    //     script{
    //       docker.build("devops/static-app")
    //     }
    //     aquaMicroscanner imageName: 'devops/static-app', notCompliesCmd: 'exit 1', onDisallowed: 'fail', outputFormat: 'html'
    //  }
    //  }

  }
}
