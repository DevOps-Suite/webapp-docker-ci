# webapp-docker-ci
This repository contains python code for web application built using fastapi, dockerfile for creating its image, and continuous integration pipeline.

### RUNNING WEBAPP IN LOCAL ENVIRONMENT (INSTRUCTIONS AS PER MACOS)
- Requires following two packages installed locally:
  ```shell
  python 3.x
  postgres 15.x
  ```
- Spin up a virtual environment and activate it:

  ```
  python3 -m venv venv
  source venv/bin/activate
  ```

- Install required dependencies:

  ```shell
  pip3 install -r requirements.txt
  ```

- Have Postgresql service running on your local:
   - Use below command if installed using homebrew on Mac

     ```shell
     brew services start <service_name>

     eg: brew services start postgresql@15
     ```

- Create a user with password on your local postgres using psql:

  ```shell
  CREATE USER <username> WITH PASSWORD '<password>'
  ```

- Create `.env` file and add below variable with your database configuration in its value:

  ```shell
  DATABASE_URL=postgresql://<postgres_user>:<postgres_password>@localhost/<database_name>
  ```

- Run the webapp using below command in your virtual environment:

  ```shell
  fastapi dev webapp
  ```

- Now access application endpoints from backend by using tools like Postman. Following endpoints are available:

  1. `GET /healthz`: Checks application and database connection

  2. `GET /items`: Lists all the available items

  3. `POST /items`: Allows to add an item using JSON payload in below format:
      ```json
      {
        "name":"Milk",
        "price":100,
        "description":"Dairy product",
        "discount":true
      } 
      ```

  4. `GET /item/<item_id>`: Lists details of the item with given item_id

  5. `PUT /item/<item_id>`: Allows to update an item with given item_id

  6. `DELETE /item/<item_id>`: Allows to delete an item with given item_id