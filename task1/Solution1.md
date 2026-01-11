When trying to upload initial 'nginx.yaml' I received an error 
error: error parsing /home/unfrmd/git_projects/sre-hometask/task1/nginx.yaml: error converting YAML to JSON: yaml: line 25: did not find expected key

I am not familiar with YAML syntax and structure of K8's specific YAML files architecture I:
1) checked it with 
https://yamlchecker.com/
2) looked into the info about Deployments YAML files at 
https://spacelift.io/blog/kubernetes-deployment-yaml

YAML checker showed an issue like this: 
 26 |      containers:
-----------^

Not an obvious error, for a first time. Having consulted with an AI, 
I found out YAML is not only case-sensitive but also indentaion-sensitive and doesn't allow TABs

containers is a part of spec element as well as affinity. So it should be sibling (have same number of spaces) to affinity
>> Added a missing space in front of 'containers:'
nano text editor also showed an excessive space in the end of line 
            cpu: 3 
>> removed. It did not showed as an error i nthe checker, just wanted tro make sure

Latly noticed that operators/parameters containing a few words are written with capital latter starting each new word: 
for eg: nodeAffinity, containerPort and so on
but all lowever-case in 
    targetport: 80

>> also asked AI regarding the syntax and was suggested to use targetPort


Then went to applying the file with kubectl:
$kubectl apply -f ~/git_projects/sre-hometask/task1/nginx1.yaml
service/sretest-service created
Error from server (BadRequest): error when creating "/home/unfrmd/git_projects/sre-hometask/task1/nginx1.yaml": Deployment in version "v1" cannot be handled as a Deployment: strict decoding error: unknown field "spec.template.spec.affinity.nodeAffinity.requiredDuringSchedulingIgnoreDuringExecution"

^did not find a solution for this specific error, unfortunately.
AI suggested removing 'affinity' for testing 
Hence I tested importing the same file with 
minikube dashboard
in my browser. and it has been imported 

Also, deleted the Deployment, the service and tried  --validate=false
to omit strict decoding while imported:

$ kubectl apply -f ~/git_projects/sre-hometask/task1/nginx1.yaml --validate=false
deployment.apps/sretest created
service/sretest-service created

Tests:
unfrmd@linux-pc:~/git_projects/sre-hometask/task1$ kubectl get Deployments
NAME      READY   UP-TO-DATE   AVAILABLE   AGE
sretest   1/1     1            1           50s
unfrmd@linux-pc:~/git_projects/sre-hometask/task1$ kubectl get pods
NAME                       READY   STATUS    RESTARTS   AGE
sretest-5659f5ff68-5d55f   1/1     Running   0          84s
unfrmd@linux-pc:~/git_projects/sre-hometask/task1$ kubectl get service
NAME              TYPE        CLUSTER-IP       EXTERNAL-IP   PORT(S)        AGE
kubernetes        ClusterIP   10.96.0.1        <none>        443/TCP        7h1m
sretest-service   NodePort    10.109.224.148   <none>        80:32653/TCP   99s
unfrmd@linux-pc:~/git_projects/sre-hometask/task1$ minikube ip
192.168.49.2
unfrmd@linux-pc:~/git_projects/sre-hometask/task1$ kubectl get svc sretest-service
NAME              TYPE       CLUSTER-IP       EXTERNAL-IP   PORT(S)        AGE
sretest-service   NodePort   10.109.224.148   <none>        80:32653/TCP   2m55s
unfrmd@linux-pc:~/git_projects/sre-hometask/task1$ curl -Ilk http://192.168.49.2:32653
HTTP/1.1 200 OK
Server: nginx/1.29.4
Date: Sun, 11 Jan 2026 20:11:32 GMT
Content-Type: text/html
Content-Length: 615
Last-Modified: Tue, 09 Dec 2025 18:28:10 GMT
Connection: keep-alive
ETag: "69386a3a-267"
Accept-Ranges: bytes

See also screenshots from minikube dash in the task1 subfolder
