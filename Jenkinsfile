node {

    checkout scm

    env.DOCKER_API_VERSION="1.23"
    
    sh "git rev-parse --short HEAD > commit-id"

    tag = readFile('commit-id').replace("\n", "").replace("\r", "")
    appName = "my-app"
    registryHost = "127.0.0.1:30400/"
    imageName = "${registryHost}${appName}:${tag}"




    // mytag="${tag}"
    // env.BUILD_TAG=mytag

    // def VAL = mytag
    


    stage "Build"
    
        sh "docker build -t ${imageName} -f applications/hello-eric/Dockerfile applications/hello-eric"
    
    stage "Push"

        sh "docker push ${imageName}"

    stage "Deploy"

        kubernetesDeploy configs: "applications/${appName}/k8s/*.yaml", kubeconfigId: 'kenzan_kubeconfig'

}