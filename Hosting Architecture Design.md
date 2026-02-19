#### IIS Express vs Kestrel Vs Ec2

App Hosted locally (IIS Express used):
```
                   LOCAL MACHINE (LAPTOP)
                   --------------------------------------------------------------------------
                   |                                                                        |
         http                            request                       request           
users ---------->  |   IIS  Express    ----------->      Kestrel    ---------->    APP      |
        request       (web server)      forwarded     (app server)     reaching    
                   |      37217 port                                                        |
                          handles http/https           handles running 
                   |       requests i.e web traffics    the app and returning response json |
                   --------------------------------------------------------------------------


                   LOCAL MACHINE (LAPTOP)
                   --------------------------------------------------------------------------
                   |                                                                        |
         https                            request                       request           
users ---------->  |   IIS  Express    ----------->      Kestrel    ---------->    APP      |
        request       (web server)      forwarded     (app server)     reaching    
                   |      44316 port                                                        |
                          handles http/https           handles running 
                   |       requests i.e web traffics    the app and returning response json |
                   --------------------------------------------------------------------------


```
