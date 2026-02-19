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


App hosted on **EC2 (REMOTE MACHINE)** (**with** IIS Express / Nginx):

```

                    EC2 (REMOTE MACHINE)
                   --------------------------------------------------------------------------------------------------------
                   |                                                                                                      |
         http                                          request                                    request           
users ---------->  |   IIS  Express / Niginx      -------------------->           Kestrel         ---------->    APP      |
        request       (web server)                    forwarded                  (app server)     reaching    
                   |      80 port                                                                                         |
                          handles http/https                                 handles running 
                   |       requests i.e web traffics                  the app and returning response json                 |
                   --------------------------------------------------------------------------------------------------------




                    EC2 (REMOTE MACHINE)
                   --------------------------------------------------------------------------------------------------------
                   |                                                                                                      |
         https                                          request                                    request           
users ---------->  |   IIS  Express / Niginx      -------------------->           Kestrel         ---------->    APP      |
        request       (web server)                    forwarded                  (app server)     reaching    
                   |      443 port                                                                                        |
                          handles http/https                                 handles running 
                   |       requests i.e web traffics                  the app and returning response json                 |
                   --------------------------------------------------------------------------------------------------------



```


App Hosted on **EC2 (REMOTE MACHINE)** (**without** IIS Express/Nginx):

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
