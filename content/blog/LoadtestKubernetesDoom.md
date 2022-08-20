---
title: "Loadtest, Kubernetes und Doom!"
date: 2021-08-22T17:17:23+02:00
featureImage: https://img.youtube.com/vi/RQzs1FIu5EU/0.jpg
tags: [ "Load", "Performance", "Testing"]
draft: false
---


[![Loadtest, Kubernetes und Doom!](https://img.youtube.com/vi/RQzs1FIu5EU/0.jpg)](https://www.youtube.com/watch?v=RQzs1FIu5EU "Loadtest, Kubernetes und Doom!")



In diesem Beispiel wurde lokal eine Kubernetes Umgebung mit Hilfe von [Terraform](https://www.terraform.io) aufgebaut.

Ziel ist es die Auswirkungen bei Pod-Ausfällen mit Hilfe von „Kube DOOM“ (Tool aus dem Bereich Chaos Engineering) unter Last zu demonstrieren.

Eingesetzte Frameworks & Tools:  

|     |     |
| --- | --- |
| Tool | Zweck |
| [Kubernetes](https://kubernetes.io) | Orchestrierung unserer Umgebung |
| [](https://www.terraform.io)[Terraform](https://www.terraform.io) | Aufbau der Infrastruktur als Code |
| [Promoteus-Stack](https://prometheus.io) (mit Grafana) | Visualisierung der Kubernetes- und Last-Metriken |
| [InfluxDB](https://www.influxdata.com) | Last-Reports Datenhaltung |
| [JMeter](https://jmeter.apache.org) | Lastgenerator als eigenes Docker mit Deployment |
| [Lens](https://k8slens.dev) | Kubernetes-Dashboard zur Visualisierung |
| [Kube DOOM](https://github.com/storax/kubedoom) | Tool aus dem Bereich Chaos Engineering |
