### Commands
``` 
gcloud beta sql connect sql-instance --user=root
mysql -u root -p --host 
```

### Cloud SQL proxy
Create the proxy to the SQL server instance from the SQL client
```
wget https://dl.google.com/cloudsql/cloud_sql_proxy.linux.amd64 -O cloud_sql_proxy
chmod +x cloud_sql_proxy
```

- https://cloud.google.com/sql/docs/mysql/sql-proxy