#Docker Usage

##Starting the environment
`cd backend/laradock`<br>
`sudo docker-compose build`<br>
`sudo docker-compose up`<br>
It'll take ~10 minutes

##Find docker IP Address
`ifconfig docker0 | grep 'inet' | cut -d: -f2 | awk '{ print $1}' | head -n`

##Further instuctions
(@TODO: Automate this)<br>

###Setting up postgres
Set docker ip address as DB host in `.env` file.<br>
Edit `.env` as<br>
```.env
MAIL_DRIVER=smtp
MAIL_HOST=mailtrap.io
MAIL_PORT=2525
MAIL_USERNAME=1d4da5fe2a7b6c
MAIL_PASSWORD=8b9cc755d476d5
```
`sudo docker exec -it laradock_postgres_1 bash`<br>
`su - postgres`<br>
`createdb immivertex`<br>
`exit`<br>
Put immivertex.sql (DB dump) in /var/lib/postgres directory on your local machine.<br>
`psql -h localhost -U postgres immivertex < /var/lib/postgres/immivertext.sql`

###Backend & frontend setup
`sudo docker exec -it laradock_workspace_1 bash`<br>
`composer install`<br>
`cd ../frontend`<br>
`npm install`<br>
`bower install --allow-root`

##Go into shell
`sudo docker exec -it laradock_workspace_1 bash`

##Working application
The frontend would be running on `http://127.0.0.1:81`<br>
The backend would be running on `http://127.0.0.1:80`<br>
Do **NOT** use `http://localhost`