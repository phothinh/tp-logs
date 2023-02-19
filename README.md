# Loki & Prometheus

This is a simple stack project that connects loki and prometheus to grafana made for my students.


## Getting Started

in the **prometheus** folder, run the following command : 

```
docker compose up -d
```

This will create a "metrics_default" network which will be used by loki. 

in the **loki** folder, then, you can run the following command : 

```
docker compose up -d
```

## Configuration

Grafana is exposed on port 3000 (default : admin/admin). Once you're logged in, you can add two new datasources : 

### Prometheus

Specify the HTTP Url to : `http://prometheus:9090`, and that's it! Don't forget to save.

### Loki

In Loki, you'll have to specify : 
HTTP Url : `http://gateway:3100`

And then Add a custom HTTP Header:
```
X-Scope-OrgID: tenant1
```

Don't forget to save.

You're now ready to go.
