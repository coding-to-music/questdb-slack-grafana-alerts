# questdb-slack-grafana-alerts

# 🚀 Javascript full-stack 🚀

https://github.com/coding-to-music/questdb-slack-grafana-alerts

From / By https://github.com/questdb/questdb-slack-grafana-alerts

## Environment variables:

```java

```

## GitHub

```java
git init
git add .
git remote remove origin
git commit -m "first commit"
git branch -M main
git remote add origin git@github.com:coding-to-music/questdb-slack-grafana-alerts.git
git push -u origin main
```

I am attempting this tutorial: https://github.com/questdb/questdb-slack-grafana-alerts

My repo is here: https://github.com/coding-to-music/questdb-slack-grafana-alerts

Community forum post: https://community.grafana.com/t/mkdir-cant-create-directory-var-lib-grafana-plugins-permission-denied/68342

https://github.com/grafana/grafana/issues/51931

When I run `docker-compose up` I get these messages:

## Errors and Messages

```
Attaching to grafana_alerts, questdb_alerts
grafana_alerts | mkdir: can't create directory '/var/lib/grafana/plugins': Permission denied
grafana_alerts | GF_PATHS_DATA='/var/lib/grafana' is not writable.
grafana_alerts | You may have issues with file permissions, more information here: http://docs.grafana.org/installation/docker/#migrate-to-v51-or-later
```

## Steps attempted to fix

When I run this

```
id -u
1000
```

I see that I am user 1000, so I tried that in addition to user 472

Per the recommendation of this page: http://docs.grafana.org/installation/docker/#migrate-to-v51-or-later

I have added this line to the docker-compose.yml

```
user: "472"
```

I have attempted to remove the directory /var/lib/grafana and also change it's ownership

I have tried changing the target directory ownership

and run `docker-compose up` as that user specified in the grafana-->user string

```
sudo chown 472:472 /var/lib/grafana
sudo chown 472:472 /var/lib/grafana/plugins

sudo chown 1000:1000 /var/lib/grafana
sudo chown 1000:1000 /var/lib/grafana/plugins
```

## Similar problem reports:

https://community.grafana.com/t/gf-paths-data-var-lib-grafana-is-not-writable/31369

https://github.com/cfbarbero/tick-grafana-docker/issues/1

Any assistance is appreciated

# QuestDB, Grafana, Slack alerts tutorial

This repository contains the example code for a tutorial about how to send alerts to Slack based on changes in market data streamed to QuestDB.
Stock prices are fetched from the [IexFinance](https://iexcloud.io/docs/api/) API using the [iexfinance](https://pypi.org/project/iexfinance/) Python package, streamed into [QuestDB](https://questdb.io/), a time series database, and alerts are set up in [Grafana](https://grafana.com/) based on the metrics we care about.

## Prerequisites

- [Docker](https://www.docker.com/)
- Python 3.7+
- [IexFinance account](https://iexcloud.io/cloud-login#/register) with an API key, free plans are available
- [Slack workspace](https://slack.com/intl/en-au/help/articles/206845317-Create-a-Slack-workspace)

## Structure

- `./docker-compose.yml`: starts QuestDB and Grafana
- `./python/`: holds Python files used in the tutorial:
  - `mock_stock_data_example.py`: generate mock data
  - `stock_data_TSLA_example.py`: polls IexFinance API and publishes records to QuestDB
  - `.env` file for storing our API key

## Getting started

1. Obtain an API key from [IexFinance console](iexcloud.io/console/tokens)
2. In the `./python` directory, create a file named `.env`
3. Place the API key in this file in the following format:

   ```
   API_KEY=ncp2syw...
   ```

4. Run docker compose:

   ```
   docker-compose up
   ```

The following services are now running:

- QuestDB web console on [port 9000](http://127.0.0.1:9000)
- Grafana for visualizing time series data in QuestDB on [port 3000](http://127.0.0.1:3000)

### Python Setup

Install the necessary packages:

```bash
pip install -r requirements.txt
```

Poll the IexFinance API and send Tesla prices to QuestDB

```bash
cd python
python stock_data_TSLA_example.py
```

(Optional) Run the script to send mock API data to QuestDB:

```bash
cd python
python mock_stock_data_example.py
```
