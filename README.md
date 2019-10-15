# QThenticate
A REST API that authenticates and authorizes an application. Authorization attempts are logged. 

This will form part of the development of a industrial monitoring application. 

This serves as a back-end authenticator for applications deployed to various client machines. Each application authenicates and validates at the start, if authorization fails, i.e. enabled is set to False, the application will stop. The purpose is to manage client access to applications from a central point of access.

Although developed for a specific implementation, this API should work for any application that has access to make API calls. 

**Installation**
Download this repo.
1. Updte config.py settings:
```
configs = {
    'SECRET_KEY' : 'chooseakey',
    'SQLALCHEMY_DATABASE_URI' : 'sqlite:///site_manager.db'
}
```
2. Create site.db 
Run python
```
>from qthenticate import db
>db.create.all()
```
3. Run application
```
python qthenticate.py
```


**Example** 
```
import requests
r = requests.get('http://localhost:5000/login', auth=('test_site', 'password'))
session_token = r.json()['token']
print(session_token)

r = requests.get('http://localhost:5000/validate', headers={"x-access-token":session_token})
validation_response = r.json()

print(validation_response)

if not validation_response['enabled']:
    print('This site is not authorized to operate')
    exit()
print("The application can now continue")
'''
...
THE REST OF THE APPLICATION
...
'''
```

[TODO]
*   Interface to add sites 
*   Add controller data
