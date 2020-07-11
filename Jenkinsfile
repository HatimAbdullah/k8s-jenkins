node {

    checkout scm

    env.DOCKER_API_VERSION="1.23"
    
    sh "git rev-parse --short HEAD > commit-id"

    tag = readFile('commit-id').replace("\n", "").replace("\r", "")
    appName = "good-night-my-love"
    registryHost = "127.0.0.1:30400/"
    imageName = "${appName}:${tag}"
    env.BUILDIMG=imageName

    stage('Build') {

    
        sh "docker build -t ${imageName} ."
}    
    stage('Push'){

        sh "docker push ${imageName}"
}
    stage('Deploy'){

        kubernetesDeploy configs: "k8s/canary/*.yaml", kubeconfigId: 'nobody_kubeconfig'
}
}
