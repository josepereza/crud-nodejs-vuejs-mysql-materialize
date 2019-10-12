# nodejs-hbs-materialize
crud api/web con nodejs- handelbars (hbs) y materialize 1.0.0 (completo)

- Hay tres formas de acceso:
  * Una como api, mediante: myip:3000/api/(listado|crear|modificar|borrar|buscar).
     Ejemplo: myip:3000/api/modificar/11
  * Otra como web, mediante: myip:3000/users/listado
     Ejemplo: http://173.242.39.9:3000/users/listado
  * Y la otra es a traves de Vuejs con el puerto 8080 o el que te diga al ejecutar en la siguiente ruta : 
     #crud-nodejs-vuejs-mysql-materialize -> client ->  npm run serve
     Ejemplo: http://173.441.31.9:8080

Funcionamiento basico:
```ruby
mysql>CREATE DATABASE seq_db;
$ git clone https://github.com/josepereza/crud-nodejs-vuejs-mysql-materialize.git
$ cd crud-nodejs-vuejs-mysql-materialize
$mysql -u root -p seq_db < db.sql
//Tenemos que modificar los datos de acceso a mysql en:controllers/apicrud.js  y controllers/listado.js
$ npm install
$ npm start
// en otro terminal
$ cd crud-nodejs-vuejs-mysql-materialize
$ cd client
$ npm install
$ npm run serve
```

Este proyecto lo hemos creado utiliando express-generator:

```ruby
$ npm install -g express-generator
$ express --hbs miapp
$ cd miapp
$ npm install
$ vue create client


```
![Alt text](todolist2.png)
