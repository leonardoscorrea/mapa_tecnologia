# MongoDB
***
#### subindo docker de mongodb
sudo docker pull mongo<br />
sudo docker images<br />
//cria um diretório para os dados<br />
sudo mkdir -p /mongodata<br />
//executa o docker montando o /mongodata no diretório do docker /data/db<br />
sudo docker run -it -v /data/db:/mongodata -p 27017:27017 --name mongodb -d mongo<br />
sudo docker ps<br />
sudo docker logs mongodb<br />
sudo docker exec -it mongodb bash<br />
mongo -host localhost -port 27017 <br />
sudo docker stop mongodb<br />
sudo docker start mongodb<br />

#### comandos
list databases

show dbs ===> lista todos os databases do mongo

show collections ===> lista todas as collections do banco selecionado

db.adminCommand( { listDatabases: 1 } )

use nomeDoBanco    ===> seleciona um database

db.runCommand( { listCollections: 1.0, authorizedCollections: true, nameOnly: true } )

db.collection.drop()

db.adminCommand( { listCollections: 1 } )

----------------------------------
db.inventory.find( { status: "D" } )  ==> SELECT * FROM inventory WHERE status = "D"
db.inventory.find( { status: { $in: [ "A", "D" ] } } )  ==> SELECT * FROM inventory WHERE status in ("A", "D")
db.inventory.find( { status: "A", qty: { $lt: 30 } } )   ==> SELECT * FROM inventory WHERE status = "A" AND qty < 30
db.inventory.find( { $or: [ { status: "A" }, { qty: { $lt: 30 } } ] } )  ==> SELECT * FROM inventory WHERE status = "A" OR qty < 30
db.inventory.find( { dim_cm: { $gt: 15, $lt: 20 } } )
db.inventory.find( {
     status: "A",
     $or: [ { qty: { $lt: 30 } }, { item: /^p/ } ]
} )                                                              ===> SELECT * FROM inventory WHERE status = "A" AND ( qty < 30 OR item LIKE "p%")

db.usuarios.find(
                   { estado: { $eq: "Rio de Janeiro" } }
)  ===> SELECT * FROM usuarios WHERE estado = "Rio de Janeiro"


db.usuarios.find({cidade : "Porto Alegre"}).sort({nome:1})    ===> SELECT * FROM usuarios WHERE cidade = "Porto Alegre" ORDER BY nome ASC
db.usuarios.find({cidade : "Porto Alegre"}).sort({nome:-1})    ===> SELECT * FROM usuarios WHERE cidade = "Porto Alegre" ORDER BY nome DESC
db.usuarios.find(('eventos.publicado': ($ne: null))) ====> SELECT * FROM usuarios u INNER JOIN eventos e ON e.id = u.id
                                                           WHERE e.publicado is not null
                                                           GROUP BY u.email   
db.collection.find(<query>).limit(<number>)



myCursor = db.inventory.find( { status: "D" } )
while (myCursor.hasNext()) {
    print(tojson(myCursor.next()));
}



{
 item: "paper",
 qty: 100,
 size: {
   h: 8.5,
   w: 11,
   uom: "in"
   },
 status: "D"
},
{
 item: "planner",
 qty: 75,
 size: {
   h: 22.85,
   w: 30,
   uom: "cm"
   },
 status: "D"
}





criando collection


db.colors.insertMany([
               {name:"red",value:"FF0000"},
               {name:"green",value:"00FF00"},
               {name:"blue",value:"0000FF"}
]);


db.colors.save({name:"red",value:"FF0000"});

db.usuarios.insert( {
                     nome: "Higor Medeiros",
                     cidade: "Porto Alegre",
                     estado: "Rio Grande do Sul"
            }
  )
  
  
MeusDados = {
          nome: "Higor Medeiros",
          cidade: "Porto Alegre",
          estado: "Rio Grande do Sul"
}
db.meudb.save(MeusDados)


try {
   db.products.insertMany( [
      { _id: 10, item: "large box", qty: 20 },
      { _id: 11, item: "small box", qty: 55 },
      { _id: 11, item: "medium box", qty: 30 },
      { _id: 12, item: "envelope", qty: 100},
      { _id: 13, item: "stamps", qty: 125 },
      { _id: 13, item: "tape", qty: 20},
      { _id: 14, item: "bubble wrap", qty: 30}
   ], { ordered: false } );
} catch (e) {
   print (e);
}



db.usuarios.remove( { estado: "Rio Grande do Sul" } ) ===> DELETE FROM usuarios WHERE estado = "Rio Grande do Sul"

db.usuarios.update( { cidade: { $eq:"Rio de Janeiro" } },
                           $set:   { estado: "Rio de Janeiro"} },
                           { multi: true }
  )                                                               ===> UPDATE usuarios SET estado = "Rio de Janeiro" WHERE cidade = "Rio de Janeiro"
