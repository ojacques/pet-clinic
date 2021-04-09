podTemplate(
    containers: [
        containerTemplate(name: 'python-container', image: 'python:3.5.10-alpine3.12', command: 'cat', ttyEnabled: true),
        containerTemplate(name: 'container-2', image: 'ubuntu:xenial-20200807', command: 'cat', ttyEnabled: true)
    ],
    annotations: [
        podAnnotation(key: "traffic.sidecar.istio.io/excludeOutboundIPRanges", value: '0.0.0.0/0') // Allows connectivity between the pod and internet services
    ]
)
{
    node(POD_LABEL) {
        stage('Print Hello World')
        {
            container ('python-container'){
                echo 'HELLO WORLD!!'
                sh 'echo "This is bash"'
                sh '''
                uptime;
                date;
                python --version
                '''
            }
        }
        stage('Second stage')
        {
            container ('container-2'){
                echo 'This is container 2'
                sh '''
                uptime;
                date;
                python --version || (echo "python not found" && exit 0)
                '''
            }
        }
    }
}
