### Étape 1 : Démarrer les instances mongod

###### 1. Commencez par créer un répertoire data avec trois sous-répertoires : db1, db2 et db3 via le terminal

```bash
  mkdir -p data/db1 data/db2 data/db3
```

###### 2. Ouvrez le fichier de configuration MongoDB mongod.conf dans un éditeur de texte et activez la réplication

```bash
  sudo nano /etc/mongod.conf
```

Décommenter ```réplication:``` et ajouter :
```
replication:
   replSetName: 'rs0'
```

###### 3. Démarrez une première instance mongod sur le port 27017, en utilisant le répertoire db1 pour les fichiers de données et le fichier mongod.conf pour la configuration. Consultez les options --replSet et --port

```bash
  sudo mongod --port 27017 --dbpath ./data/db1 --replSet rs0 --config /etc/mongod.conf
```

###### 4. Démarrez une deuxième instance mongod sur le port 27018, en utilisant le répertoire db2 pour les fichiers de données et le fichier mongod.conf

```bash
  sudo mongod --port 27018 --dbpath ./data/db2 --replSet rs0 --config /etc/mongod.conf
```

###### 5. Démarrez une troisième instance mongod sur le port 27019, en utilisant le répertoire db3 pour les fichiers de données et le fichier mongod.conf

```bash
  sudo mongod --port 27019 --dbpath ./data/db3 --replSet rs0 --config /etc/mongod.conf
```

### Étape 2 : Se connecter à une des instances mongod

###### 1. Connectez-vous à la première instance mongod sur le port 27017 avec le shell mongo ou mongosh

```bash
  mongosh --port 27017
```

###### 2. Initialisez l’ensemble de réplication

```bash
  rs.initiate()
```

###### 3. Ajoutez les deuxième et troisième instances mongod à l’ensemble de réplication

```bash
  rs.add("127.0.0.1:270178")
  rs.add("127.0.0.1:270179")
```

###### 4. Vérifiez que l’ensemble de réplication fonctionne correctement. 

```bash
rs.status()
```

### Étape 3 : Créer une base de données et insérer des données

###### 1. Créez une base de données nommée GameOfThrones.


###### 2. Créez une collection nommée characters


###### 3. Insérez les documents dans la collection


### Étape 4 : Vérifier la réplication

###### 1. Connectez-vous à la deuxième instance mongod sur le port 27018 avec le shell mongo ou mongosh


###### 2. Interrogez la base de données GameOfThrones et la collection characters pour vérifier que les données ont été répliquées


###### 3. Pouvez-vous lire les données ? Pouvez-vous écrire des données ?


###### 4. Connectez-vous à la troisième instance mongod sur le port 27019 avec le shell mongo ou mongosh


###### 5. Interrogez la base de données GameOfThrones et la collection characters pour vérifier que les données ont été répliquées


###### 6. Pouvez-vous lire les données ? Pouvez-vous écrire des données ?



