# NodeJS API and PostgreSQL with docker compose

Simple NodeJS todo app connects with PostgreSQL database.

### Building and running your application

>Before starting the app, make sure change the **postgres.env.example** file to **postgres.env** and **.env.example** file in app/ dir to **.env**, and change the password values inside.

When you're ready, start your application by running:

`$ docker compose up -d`

Your application will be available at http://localhost:3000.

### Add a new task
``$ curl -X POST http://localhost:3000/tasks -H "Content-Type: application/json" -d '{"title": "Task 1", "description": "This is task 1"}'``

### Update the existing task
``$ curl -X PUT http://localhost:3000/tasks/1 -H "Content-Type: application/json" -d '{"title": "Updated Task 1", "description": "Updated description", "completed": true}'``

### Retrieve tasks
``$ curl http://localhost:3000/tasks``
``$ curl http://localhost:3000/tasks/1``

### Delete tasks
``$ curl -X DELETE http://localhost:3000/tasks/1``
### Note to Remember

1. For PostgreSQL:
    >PostgreSQL default user is **postgres**. Creating different user using **POSTGRES_USER** variables can generate **"FATAL: database "your-db-username" does not exist"** error. This is because (as far as I know) of **healthcheck**. 
    >If you don't specify the database name in **pg_isready** heathcheck command, it assume the default database name as the same as database username.

    >**Just specify the username, password(optional) and database name in your ``pg_isready`` healthcheck command as required**.

    >Env variables need to be called by **double dollar sign($$)** in **healthcheck**.


2. PostgreSQL database create at startup (docker compose):
    >Create init.sql file in the same folder as compoese and add your postgresql command.
    Mount the file in compose file. [Tutorial](https://mkyong.com/docker/how-to-run-an-init-script-for-docker-postgres/)

    ```yaml
    volumes:
        - ./init.sql:/docker-entrypoint-initdb.d/init.sql
    ```
