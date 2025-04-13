library identifier: 'commonPipeline@main', retriever: modernSCM([$class: 'GitSCMSource',
    remote: 'git@github.com:meghdo-aws/shared-libraries.git',
    credentialsId: 'jenkins_agent_ssh'])
commonPipeline (
    accountName: "meghdo",
    accountId: "354918396806",
    clusterName: "meghdo-cluster",
    region: "us-east-1",
    appName: "drizzlego",
    namespace: "default",
    scanOWASP: "false",   // OWASP Scanning takes about 7-10 min of scanning time, turn on when scanning is needed
    scanDir: "src",
    label: 'go'
) {
    container('golang') {
        sh """
        # Set up Go workspace
        export PATH="/usr/local/go/bin:$PATH"
        cd src
        pwd
        go mod tidy
        go mod download
       
        # Build the application
        CGO_ENABLED=0 GOOS=linux go build -a -installsuffix cgo -o ./main .
        """
    }
}   
