## K8S-Nodejs-MySQL Application

##### Generate the base64 key and use it in the mysql-secret.yaml file #####
`echo -n 'khaleel' | base64`

##### First Create Secret for MySQL #####
`kubectl apply -f mysql-secret.yaml`

##### Now deploy the pv, pvc manifest file, where all your mysql data will be stored. Here i used nfs #####
`kubectl apply -f mysql-pv_pvc.yaml`

##### Now deploy the Mysql Pod #####
`kubectl apply -f mysql-deployment.yaml`

##### Now deploy the Mysql Service #####
`kubectl apply -f mysql-service.yaml`

##### Once the POD and Service of MySQL are running, the next step is to create the DB & Tables in MySQL #####
`kubectl exec nodejs-mysql -it -- bash`
##
CREATE DATABASE node_crud; <br />
use node_crud;<br />

CREATE TABLE `users` (<br />
  `id` int(11) NOT NULL,<br />
  `name` varchar(150) NOT NULL,<br />
  `email` varchar(150) NOT NULL,<br />
  `phone_no` varchar(25) NOT NULL<br />
) ENGINE=InnoDB DEFAULT CHARSET=latin1; <br />

ALTER TABLE `users` ADD PRIMARY KEY (`id`);<br />

ALTER TABLE `users` MODIFY `id` int(11) NOT NULL AUTO_INCREMENT, AUTO_INCREMENT=1; COMMIT;<br />

ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'khaleel';<br />

ALTER USER 'root'@'%' IDENTIFIED WITH mysql_native_password BY 'khaleel';<br />

flush privileges;<br />

##### Now edit index.js file and change the mysql credentials #####
`docker build -t nodecrud:v1 .`

`docker image tag nodecrud:v1 shaikabdulkhaleel/nodecrud:v1`

`docker push shaikabdulkhaleel/nodecrud:v1`

##### Now deploy the nodejs k8s manifest file, which has deployment and service objects #####
`kubectl apply -f node-deployment.yaml`

`kubectl get pods,svc -l app=node-app`

## Now Access the Application using the Any NodeIP:32100 ##


