## Jenkins email notification


Go to jenkins dashboard  -->  manage jenkins  --> plug-ins -->  installed plug-ins  --> ( Email Extension plugins ) ,,, if not then install

Go to gmail & enable 2-step verification --> go to home --> search app passwords --> app name = Jenkins ---> create --> copy pw


Go to manage jenkins  --> Credentials  --> add Credentials

        - Kind = username & password
        - Username = use your gmail id
        - password = use your app password
        - ID = mygmail
        - Description = gmail app pw
        - create
    
( Credentials created successfully )
               - 
     
#### step-4 :- go to manage jenkins  --> system  --> scroll down & go to `Extended E-mail Notification`

  - SMTP server  = smtp.gmail.com
  - SMTP Port  = 465
  - Go to advance  --> Credentials = use your created Credentials
  - Use SSL  = allow
  - Default Recipients  = use your gmail add

  - `scroll down & go to E-mail Notification`
    
        - SMTP server  = smtp.gmail.com
    
        - click advanced  -->  Use SMTP Authentication  -->  User Name = your gmail add   -->  Password  = use your app password
        - SMTP Port = 465
        - Test e-mail recipient  = your gmail add ( test it )
    

  - save
    




-----------------------------------------------------------
