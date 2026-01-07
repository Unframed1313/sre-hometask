# SRE challenge

Hello!

Thank you for your interest shown by your application to join our team!

Among Namecheap teams, the Cloud team builds its own on-premise cloud-based architecture that is used for hosing WordPress websites, AI-generated websites, CDN and Hyperlift services along with other products. Such a large and loaded system needs constant monitoring and improvement, and this is exactly why we are looking for a newjoiners in the Site Reliability Engineering field. We expect that you will grow with us, learn a lot of new things and contribute to the stability and observability of our vast and complex infrastructure.

🌞 We have three tasks for you to demonstrate your thinking, analytic,and debug skills. You have to clone this repository to complete the following challenges to your own GitHub account. 

Where to start: 

- Make a fork of this repository to your Github account
- Solve the tasks thoroughly
- Commit to your forked repository with your solutions into corresponding folders and files

How to show your results: 

- Share the link to your forked repository with us
- Be ready to discuss tasks briefly on the interview

> AI usage disclaimer:
>
> We surely understand modern world uses AI help daily, and during your potential work with us, you will be doing the same. Thus, we do not restrict AI usage completely during the task resolution, even though we would be happy if you manage to do it with plain googling. In any case, please be ready to explain this or that decision to prove that you understand everything you submit as a solution.


🍀 Good luck! 


## Task 1. A tangle in Kubernetes jungle

Install any local K8s cluster (e.g. `Minikube`) on your machine. Use the `task1/nginx.yaml` file to create resources of a simple webserver. Oops, looks like you need to fix some issues for application to run.
The success is to access Nginx page in browser. 

Desired outcome: 
- created `nginx_new.yaml` file with a working YAML configuration for all Kubernetes resources you found inside the initial YAML file 
- `solution1.md` file with explanations what errors and mistakes you spotted and ways how you spotted and fixed them
- if you wish to share any screenshots, statements, or tips you spotted during investigation - feel free to do it as well for sure! 

Please place both solution-related files to the `task1` folder in your forked repository.


## Task 2. Kindergarten data analytics

You have a file `access.log` in the `task2` folder that contains some webserver access logs. Please retrieve the following information based on analyzing that file: 

- top 5 IP addresses requests come from
- number of requests with '50X' and '200' HTTP response codes
- number of requests per minute;
- which method is the most frequent one?
- any other improvements you can recommend to server admin based on the access log

Desired outcome: 
- `solution2.md` file that should include
    - retrieved answers to the questions above
    - commands you used to get those answers
    - your thoughts on the last question.

Please place the file into the `task2` folder.

## Task 3. Graph Dracula to rule them all

For this task, we are showing a Prometheus alert example below, please check it and anwser the following questions:

```sh
- alert: ReplicationNotRunning
  expr: mysql_slave_status_slave_io_running == 0 or mysql_slave_status_slave_sql_running == 0
  for: 2m
  labels:
    severity: warning
  annotations:
    dashboard: sample-grafana-dashboard
    description: 'Slave replication (IO or SQL) has been down for more than 2 minutes on pod:`{{ $labels.pod }}`'
    summary: Replication is not running
```


Based on this alert, please perform some basic analysis about what this alert should monitor, and create a simple Grafana dashboard with 2-5 panels that would help in case this alert fires.

You can install Grafana on the same `Minikube` cluster, or use online version - here you have all the choice freedom. 

Desired outcome: 
- exported Grafana dashboard as a `.json` file
- screenshot(s) of the dashboard
- file `solution3.md` with your thoughts about reasons why alert may fire and ways to fix it.

Please place all the files to the `task3` folder in your forked repository.