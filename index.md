# CSE 15L - Lab Report 2 - Alexander Zhen

## Part 1: Creating ChatServer.java 

### Code used for ChatServer.java, similar to NumberServer.java
```
import java.io.IOException;
import java.net.URI;

class Handler implements URLHandler {
 
    String add_message = "";
    String user = ""; //added new strings, instead of int num.
    String message = "";

    public String handleRequest(URI url) {
        if (url.getPath().equals("/add-message")) { //instead of "/", need to use "/add-message"
            String[] parameters = url.getQuery().split("&");
            //using url.getQuery() like in NumberServer.java, but using '&' to help split up the string when there's a '&' in the link.
            message = parameters[0].split("=")[1];
            //takes the 's' and then divides it on '=' at index [0] and then some value = our message on index [1]. 
            user = parameters[1].split("=")[1];
            //after splitting on '&', takes the second part of 'user' and then divides it on '=' at index [1] and then some value = username on index [1]
 
            add_message += user + ": " + message + "\n"; //concatenates and to format the output

            return add_message;

        } 
        else {
            return "404 Not Found!";
        }
    }
}

class ChatServer { //same part from NumberServer.java
    public static void main(String[] args) throws IOException {
        if (args.length == 0) {
            System.out.println("Missing port number! Try any number between 1024 to 49151");
            return;
        }

        int port = Integer.parseInt(args[0]);

        Server.start(port, new Handler());
    }
}
```

### Screenshots of using `/add-message`. 
![Image][1.PNG]
