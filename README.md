# play-java-crud
play-java-rest-api with mongodb

 #add dependency
build.sbt
// https://mvnrepository.com/artifact/org.mongodb.morphia/morphia
libraryDependencies += "org.mongodb.morphia" % "morphia" % "1.3.0"

#connection
public class Mongo {
    public static Datastore datastore;

    public static Datastore datastore(){
        if(datastore == null){
            initDatastore();
        }

        return datastore;
    }

    public static void initDatastore(){
        final Morphia morphia = new Morphia();

        // tell it to fine model class
        morphia.mapPackage("models.investor");

        String host = ConfigFactory.load().getString("mongodb.host");
        int port = ConfigFactory.load().getInt("mongodb.port");
        String username = ConfigFactory.load().getString("mongodb.username");
        String database = ConfigFactory.load().getString("mongodb.database");
        String password = ConfigFactory.load().getString("mongodb.password");


        MongoClient mongoClient = new MongoClient(singletonList(new ServerAddress(host,port)),
                singletonList(MongoCredential.createCredential(username, database, password.toCharArray())));

        datastore = morphia.createDatastore(mongoClient, database);
    }
}

#Stature
- Controller
- Repos
- Service
- Model




