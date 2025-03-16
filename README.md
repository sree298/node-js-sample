### This repository is no longer maintained!

**For the most up to date test app to get you started on Heroku, head on over to [`node-js-getting-started`](https://github.com/heroku/node-js-getting-started).**

---

# node-js-sample

A barebones Node.js app using [Express 4](http://expressjs.com/).

## Running Locally

Make sure you have [Node.js](http://nodejs.org/) and the [Heroku Toolbelt](https://toolbelt.heroku.com/) installed.

```sh
git clone git@github.com:heroku/node-js-sample.git # or clone your own fork
cd node-js-sample
npm install
npm start
```

Your app should now be running on [localhost:5000](http://localhost:5000/).

## Deploying to Heroku

```
heroku create
git push heroku master
heroku open
```

Alternatively, you can deploy your own copy of the app using the web-based flow:

[![Deploy to Heroku](https://www.herokucdn.com/deploy/button.png)](https://heroku.com/deploy)

## Documentation

For more information about using Node.js on Heroku, see these Dev Center articles:

- [10 Habits of a Happy Node Hacker](https://blog.heroku.com/archives/2014/3/11/node-habits)
- [Getting Started with Node.js on Heroku](https://devcenter.heroku.com/articles/getting-started-with-nodejs)
- [Heroku Node.js Support](https://devcenter.heroku.com/articles/nodejs-support)
- [Node.js on Heroku](https://devcenter.heroku.com/categories/nodejs)
- [Using WebSockets on Heroku with Node.js](https://devcenter.heroku.com/articles/node-websockets)


## Steps:
1. Login to https://github.com, https://hub.docker.com
2. Create PAT in github and dockerhub
3. Create repo node-js-sample in github
4. RUN bellow command to create package-lock.json -
   npm install 
6. setup github in local-
   git config --global user.name "github username"
   git config --global user.email "email"
   git init
   git add .
   git commit -m "Initial commit"
   git branch -M main
   git remote add origin https://github.com/Sandip9292/node-js-sample.git
   git push -u origin main
7. write dockerfile, deployment.yaml, persistent-volume.yaml, network-policy.yaml
8. login to docker -
   docker login
   enter username and password
9. RUN bellow command on terminal to avoid docker access issue at jenkins-
   sudo usermod -aG docker $USER
   newgrp docker
10. build image -
   docker build -t sandip9292/node-js-sample:1.0 .
11. Login jenkins and install plugins
12. create jenkins pipeline job with name "Node.js-Deployment" and write jeninsfile
13. create global creadential for github and dockerhub. Use PAT for password.
14. Kubectl commands-
    kubectl apply -f k8s/deployment.yaml
    kubectl apply -f persistent-volume.yaml
    kubectl apply -f network-policy.yaml
    kubectl get all
    kubectl get pods
    kubectl get svc
    kubectl get pv
    kubect get pvc
    kubectl get networkpolicies
    kubectl describe pod podname
    kubectl describe networkpolicy <network-policy-name>
    kubectl describe pvc <pvc-name>
    kubectl describe pv <pv-name>
    kubectl label pod pod_name app=node-js
15. How to find minikube ip - 
    minikube ip
16. How to access application through browser-
    http://minikubeip:30007

I68QxiWferEhkQOJX6dMNOmP83q9Wi4Af7PC
mkdir -p ~/.docker/cli-plugins
curl -L https://github.com/docker/buildx/releases/download/v0.8.0/buildx-v0.8.0.linux-amd64 > ~/.docker/cli-plugins/docker-buildx
chmod +x ~/.docker/cli-plugins/docker-buildx

sudo vi /etc/docker/daemon.json

{
  "dns": ["8.8.8.8", "8.8.4.4"]
}

sudo usermod -aG docker jenkins
sudo usermod -aG docker jenkins
sudo systemctl restart jenkins
kubectl port-forward service/node-js-sample 5000:5000
127.0.0.1:5000

    
