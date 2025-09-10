TODO: Improve this by making this more detailed and easier to follow
To extract local database scheme with data
```
docker exec -it [NAME OF DOCKER CONTAINER] pg_dump -U postgres -d postgres > name_of_file.sql 
```

To insert data into local database scheme
```
docker cp name_of_file.sql [NAME OF DOCKER CONTAINER]:/name_of_file.sql
```

Going into the docker container
```
docker exec -it [NAME OF DOCKER CONTAINER] bash
```

Add it into local db (make sure you're in the same directory as the file that you downloaded)
```
psql -U postgres -d postgres -f /name_of_file.sql 
```

Connecting to the cloud server through psql
```bash
postgresql://postgres.[PROJECT-REF]:[YOUR-PASSWORD]@aws-0-ap-southeast-1.pooler.supabase.com:5432/postgres
```