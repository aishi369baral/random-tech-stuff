#### IIS Express vs Kestrel Vs Ec2

App Hosted **LOCALY** (**with** using IIS Express):
```
                   LOCAL MACHINE (LAPTOP)
                   ------------------------------------------------------------------------------------
                   |                                                                                  |
         http                            request                               request           
users ---------->  |   IIS  Express    ----------->           Kestrel         ---------->    APP      |
        request       (web server)      forwarded             (app server)     reaching    
                   |      37217 port                                                                  |
                          handles http/https                    handles running 
                   |       requests i.e web traffics            the app and returning response json   |
                   ------------------------------------------------------------------------------------




                   LOCAL MACHINE (LAPTOP)
                   -------------------------------------------------------------------------------------
                   |                                                                                   |
         https                            request                               request           
users ---------->  |   IIS  Express    ----------->             Kestrel        ---------->    APP      |
        request       (web server)      forwarded               (app server)     reaching    
                   |      44316 port                                                                   |
                          handles http/https                     handles running 
                   |       requests i.e web traffics             the app and returning response json   |
                   --------------------------------------------------------------------------------------


```

App hosted **LOCALY** (**without** using IIS Express):
```
                   LOCAL MACHINE (LAPTOP)
                   ------------------------------------------------
                   |                                              |
         http                           request           
users ---------->  |   Kestrel         ---------->    APP         |
        request        (app server)      reaching    
                   |      5101 port                               |
                            handles running 
                   |        the app and returning response json   |
                   ------------------------------------------------




                   LOCAL MACHINE (LAPTOP)
                   ------------------------------------------------
                   |                                              |
         https                           request           
users ---------->  |   Kestrel         ---------->    APP         |
        request        (app server)      reaching    
                   |      7135 port                               |
                            handles running 
                   |        the app and returning response json   |
                   ------------------------------------------------
```


App hosted on **EC2 (REMOTE MACHINE)** (**with** IIS / Nginx):
- IIS can only run on EC2 with a Windows OS.
- Niginx can only run on EC2 with a Linux OS.

```

                    EC2 (REMOTE MACHINE)
                   --------------------------------------------------------------------------------------------------------
                   |                                                                                                      |
         http                                          request                               request           
users ---------->  |     IIS / Niginx      -------------------->           Kestrel         ---------->    APP      |
        request          (web server)                 forwarded         (app server)      reaching    
                   |      80 port                                                                                         |
                          handles http/https                                 handles running 
                   |       requests i.e web traffics                  the app and returning response json                 |
                   --------------------------------------------------------------------------------------------------------




                    EC2 (REMOTE MACHINE)
                   --------------------------------------------------------------------------------------------------------
                   |                                                                                                      |
         https                                          request                                    request           
users ---------->  |            IIS / Niginx      -------------------->           Kestrel         ---------->    APP      |
        request                 (web server)           forwarded                  (app server)     reaching    
                   |           443 port                                                                                        |
                          handles http/https                                 handles running 
                   |       requests i.e web traffics                  the app and returning response json                 |
                   --------------------------------------------------------------------------------------------------------



```


App Hosted on **EC2 (REMOTE MACHINE)** (**without** IIS /Nginx):

```



                    EC2 (REMOTE MACHINE)
                   -------------------------------------------------------------------------------------------
                   |                                                                                         |
         http                request                                                   request
users ---------->  |   -------------------->           Kestrel                       ---------->    APP      |
        request             forwarded                  (app server)                   reaching    
                   |                                   5000 port
                                                     handles running 
                   |                       the app and returning response json                               |
                   -------------------------------------------------------------------------------------------




                    EC2 (REMOTE MACHINE)
                   --------------------------------------------------------------------------------------------
                   |                                                                                          |
         https               request                                                    request           
users ---------->  |-------------------->           Kestrel                           ---------->    APP      |
        request              forwarded             (app server)                        reaching    
                   |                                 5001 port                                                |
                                                handles running 
                   |                       the app and returning response json                                |
                   --------------------------------------------------------------------------------------------



```


**It is Recommend or best practise to use a Web Server(IIS Express / Niginx) **

**It is also Recommend to have a Application Load Balancer before Web Server**

```
users -> ALB -> Ec2 -> web server -> app server -> app
```


#### For the Frontend (React + Vite) in Development Environment:
 In case we are using React + Vite for the frontend code:
 - We can use Vite.

Vite:
```
A development only tool that provides a fast Http Server for dev environment,
- Handles Http/Https requests,
- Returns Static files as response.
- Adds dev-only magic (hot reload, module replacement)

```


#### Difference between IIS Express | IIS |  Nginx  | Kestrel | Vite :
 All of these are different types of servers:

| IIS Express          | IIS                                     | Nginx                                | Kestrel                    | Vite                       |
| ---------------------| --------------------------------------- |-------------------- ---------------  | -------------------------- | -------------------------- |
| A Web Server         | A Web Server (in a EC2 with windows OS) | A Web Server (in a EC2 with linux OS)| A App Server + HTTP Server | A HTTP Server + build tool |
| for development only | for production only                     | for production only                  | for dev & prod both        | for development only       |

