# Utils

### SQL Server 

- Criar container com SQL Server usuário SA
```
docker run -e 'ACCEPT_EULA=Y' -e 'SA_PASSWORD=SQLServerP@$$' \
   -p 1433:1433 --name mssql2017 \
   -d microsoft/mssql-server-linux:2017-latest
```
- Alterar Senha SQL Server usuário SA

```
docker exec -it sql1 /opt/mssql-tools/bin/sqlcmd \
   -S localhost -U SA -P '<YourStrong!Passw0rd>' \
   -Q 'ALTER LOGIN SA WITH PASSWORD="SQLServerP@$$"'
```
#

### Rancher
- Host não aparece no Rancher Server
   
https://rancher.com/docs/rancher/v1.6/en/faqs/agents/#reference-to-localhost-present-in-etcresolvconf

https://docs.docker.com/install/linux/linux-postinstall/#specify-dns-servers-for-docker


Specify DNS servers for Docker
The default location of the configuration file is /etc/docker/daemon.json. You can change the location of the configuration file using the --config-file daemon flag. The documentation below assumes the configuration file is located at /etc/docker/daemon.json.

Create or edit the Docker daemon configuration file, which defaults to /etc/docker/daemon.json file, which controls the Docker daemon configuration.
```sh
$ sudo nano /etc/docker/daemon.json
```

Add a dns key with one or more IP addresses as values. If the file has existing contents, you only need to add or edit the dns line.
```json
{
	"dns": ["8.8.8.8", "8.8.4.4"]
}
```

If your internal DNS server cannot resolve public IP addresses, include at least one DNS server which can, so that you can connect to Docker Hub and so that your containers can resolve internet domain names.

Save and close the file.

Restart the Docker daemon.

```sh
$ sudo service docker restart
```
#

### RabbitMQ
https://hub.docker.com/_/rabbitmq/

- Management Plugin 

```
docker run -d --hostname rabbitmq-server --name rabbitmq-server -p 8091:15672 -p 8090:5672 rabbitmq:3-management
```

- Versão alterando o usuário padrão
```
docker run -d -p 8090:5672 -p 8091:15672 --hostname rabbit-mq-server --name rabbit-mq-server rabbitmq:3.7-management -e RABBITMQ_DEFAULT_USER=admin -e RABBITMQ_DEFAULT_PASS=password rabbitmq:3.7-management
```

- Solução para resolver a conexão com o rabbitmq em um container docker
https://groups.google.com/forum/#!topic/masstransit-discuss/bvmHfka5TVk

> Problem solved...I was making two instances!

> For those who are interested by any chance, you need to expose both ports 5672 and 15672
  
```
docker run -d -p 8090:5672 -p 8091:15672 --hostname rabbitmq-server --name rabbitmq-server -e RABBITMQ_DEFAULT_USER=admin -e RABBITMQ_DEFAULT_PASS=password rabbitmq:3-management
```


  


