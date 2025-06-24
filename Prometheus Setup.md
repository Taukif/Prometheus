---
title: Website Monitoring Setup Guide (Prometheus)
---

# Download Prometheus

Prometheus\
Download from: <https://prometheus.io/download>

**OR**\
\
command write in wsl:\
**(\"cd\"** stands for **change directory)**

**cd /mnt/c/Users/91754/website_monitoring**

**(wget** is a tool used to **download files from the internet** using a
link**)**\
**wget**
<https://github.com/prometheus/prometheus/releases/download/v2.52.0/prometheus-2.52.0.linux-amd64.tar.gz>

**(tar** is a tool used to **extract compressed archive files)**\
**tar -xvf prometheus-2.52.0.linux-amd64.tar.gz**

**{x: extract the file**

**v: show the extraction process (verbose)**

**f: file name to extract**

**}**

**(mv** means **move\[**prometheus-2.52.0.linux-amd64 → to →
prometheus**\])**\
**mv prometheus-2.52.0.linux-amd64 prometheus**

# Configure Prometheus

> Edit the config file:\
> \
> **cd /mnt/c/Users/91754/website_monitoring/prometheus\
> nano prometheus.yml**\
> \
> **\### In .prometheus.yml file \####**
>
> **global:\
> scrape_interval: 15s\
> \
> scrape_configs:\
> - job_name: \'blackbox\'\
> metrics_path: /probe\
> params:\
> module: \[http_2xx\]\
> \
> static_configs:\
> - targets:\
> - https://flocard.app \# Replace with your target website\
> \
> relabel_configs:\
> - source_labels: \[\_\_address\_\_\]\
> target_label: \_\_param_target\
> - source_labels: \[\_\_param_target\]\
> target_label: instance\
> - target_label: \_\_address\_\_\
> replacement: localhost:9115 \# Blackbox exporter port**\
> \
> \
> **Run Prometheus:**\
> \
> **./prometheus \--config.file=prometheus.yml**
>
> **After completing all steps , then**\
> **Visit: http://localhost:9090**
