# Learn Kafka
This is a docker compose file that will help spin a full Kafka environment with monitoring capabilities

## Docker Instructions

In order to spin everything up you need to run ``` docker compose up -d ```

If you want to spin up a particular service you can run a command like ``` docker compose up -d kafka ```

If you want to spin up multiple services you can run a command like ``` docker compose up -d kafka akhq ```

## Instructions
Notes: I leveraged this project for the [kafka-exporter](https://github.com/redpanda-data/kminion).  I also leveraged grafana dashboards referenced in that project.  I'll write out better instructions in my next iteration.
