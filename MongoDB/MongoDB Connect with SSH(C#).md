> # MongoDB SSH로 접속하기

---

SSH로 MongoDB에 접속하기 위해선 MongoDB Server의 HostName으로 
SSH에 연결한 상태에서   
MongoDB에 접속을 해주면된다.

> SSH Connecting
``` c#
    using Renci.SshNet;

    static void Main(){
        SshClient ssh = new SshClient("HOSTNAME", "USERNAME","USERPASSWD");
        ssh.Connect();
        var port = new ForwardedPortLocal("127.0.0.1", 27017, "localhost", 27017);
        ssh.AddForwardedPort(port);
        port.Start();
    }
```

> MongoDB Connecting

``` c#
    using MongoDB.Driver;
    using MongoDB.Bson;

    public void ConnectDB(){
        string connectionString = "mongodb://localhost:27017";
        MongoClient client = MongoClient(connectionString);


        IMongoDatabase db = client.GetDatabase("admin");
    }
```

 GetDatabase 로 DB를 불러온 후 확인해보면   
 접속이 되었다는것을 확인할 수 있다.
