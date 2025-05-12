# SUPABASE vector database service

### Web panel - port 8000

Working not as root

Create a folder for work
```
git clone --depth 1 https://github.com/supabase/supabase
```

Go to the directory for starting container assembly
```
cd supabase/docker
```

Prepare a file
```
cp .env.example .env
```

Specify new credentials in this file (instead of the default old ones). Basic authentication will be used
```
DASHBOARD_USERNAME=mysupabasesupers...
DASHBOARD_PASSWORD=this10_pass20_is30_insecure40_and50_should60_be70_upda.....
```

Download the necessary images for containers
```
sudo docker compose pull
```

Run the container build
```
sudo docker compose up -d
```

For key access, you must use SERVICE_ROLE_KEY (from the file supabase/docker/.env)
```
SERVICE_ROLE_KEY=eyJhbGciOiJIUzI1NiIsInR5cCI6IkpXVCJ9.eyAgCiAgICAicm9sZSI6ICJzZXJ2aWNlX3JvbGUiLAogI.......
```

Running the test script test.sql. The result is as follows
```
PostgreSQL 15.8 on x86_64-pc-linux-gnu, compiled by gcc (GCC) 13.2.0, 64-bit
```

Configuring additional indexing in the database. The number of lists is usually equal to the square root of the total number of records. You can check the quality of indexing using the commands
```
SELECT * FROM pg_indexes WHERE tablename = 'documents';
EXPLAIN SELECT * FROM documents ORDER BY embedding <=> '[0.1, 0.2, 0.3]' LIMIT 10;

REINDEX INDEX idx_embedding;
```
