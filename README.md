# Learn Kafka
This is a docker compose file that will help spin a full Kafka environment with monitoring capabilities

## Docker vs Podman

I have tested this using Docker and Podman. I personally use Podman and can confirm the docker compose commands will work seemlessly.
## Docker/Podman Instructions

In order to spin everything up you need to run ``` docker compose up -d ```

If you want to spin up a particular service you can run a command like ``` docker compose up -d kafka ```

If you want to spin up multiple services you can run a command like ``` docker compose up -d kafka akhq ```

## Instructions
Notes: I leveraged this project for the [kafka-exporter](https://github.com/redpanda-data/kminion).  I also leveraged grafana dashboards referenced in that project.  

1. Run ``` docker compose up -d ``` to start everything 
    - All containers are set to auto restart unless stopped, so don't be surprised if Kafka has to restart a couple times until Zookeeper is fully up and running.
2. You can verify `kafka-exporter` is working by running this command in terminal or powershell: ``` curl http://localhost:9308/metrics ```
    - You should see an output like this as you scroll down. The key is as you look through the output you'll see information like topics from your kafka instance.
    ```
    kminion_kafka_broker_info{address="kafka",broker_id="1",is_controller="true",port="9092",rack_id=""} 1
    ```
3. You can verify Prometheus is running by going to this page: ``` http://localhost:9090/targets?search= ```
    - You should see both targets UP and in green status
4. Open Grafana by going to ``` http://localhost:3000 ```
    - Login with 
        - user: admin
        - password: admin
        - you will be prompted to change the password, but for testing purposes you can just "change it" to admin (LOL)
    - You will want to add a Data Source 
        - Choose Prometheus
        - update url to ``` http://prometheus:9090 ```
        - Click `Sve & test` button
    - Go to `Dasboards` and choose `+import`
        - Where it says `Import via grafana.com` type ``` 14012 ``` (Cluster Info) and click `Load`
            - You will need to set the `Data Source` to Prometheus data source you just created
        - You can repeat this step by importing ``` 14013 ``` (Topic Info) and ``` 14014 ``` (Consumer Info) for the other 2 dashboards 
    - You should see a populated grafana dashboard!

## Here's some resources to help learn Kakfa

You can't go wrong by going to learning from [Robin Moffat](https://rmoff.net)

Also here's a link to his [youtube channel](https://www.youtube.com/c/rmoff)

