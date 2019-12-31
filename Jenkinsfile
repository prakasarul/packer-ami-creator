
    node {
        stage('Checkout') {
            // Clean the workspace
            cleanWs()
            // Get some code from a GitHub repository
            checkout scm
        }
        
        stage('Validate') {
            sh "packer validate rhel_hard_ansi_manifestout.json"
        }
        stage('Build') {

    //used cloudbees aws credentials plugin
        withCredentials([[$class: 'AmazonWebServicesCredentialsBinding', accessKeyVariable: 'AWS_ACCESS_KEY_ID', credentialsId: 'aws_access_keys', secretKeyVariable: 'AWS_SECRET_ACCESS_KEY']]) {
    // Run the packer build
            sh "packer build  rhel_hard_ansi_manifestout.json"
}
          
        }
        stage('Store Artifacts') {
            archiveArtifacts 'manifest.json'
        }
    }

