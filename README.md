# FBTools
Facebook Automation Tools  
>Python 3.10 - 3.12   
<br>

## Installation
```python
pip install FBTools
```
<br>  
<br>

### Create Account
```python
from FBTools.CreateAccount import CreateAccount

name = 'Input Your Name Here'
password = 'Input Your Password Here'
birthday = '25/12/1995' # DD/MM/YYYY
email = 'examplename@example.com'
gender = 1 # 1=Male, 0=Female
CA = CreateAccount()
CA.SetData(name=name, password=password, birthday=birthday, email=email, gender=gender)
CA.Create()
```
Parameter  
>name : Name You Want To Create (string, default=None)  
password : Password You Want To Create (string, default=None)  
birthday : Birth Date You Want To Set (string, default=None)  
email : Email You Want To Register (string, default=None)  
phone : Phone You Want To Register (string, default=None)  
gender : Gender You Want To Set (bool, default=0 -> female)  
<br>  
<br>

## Login

### Parameter
```python
cookie   = 'datr=nxbaxnynx; sb=axn...' # Input Your Cookie Here
email    = 'dapuntaxayonara@gmail.com' # Input Your Email Here
phone    = '6282245780524'             # Input Your Phone Here
password = 'satusampaidelapan'         # Input Your Password Here
```

### Login With Cookie
```python
from FBTools import Start
FB = Start(cookie=cookie)
```

### Login With Email & Password
```python
from FBTools import Start
FB = Start(email=email, password=password)
```

### Login With Phone & Password
```python
from FBTools import Start
FB = Start(phone=phone, password=password)
```

### Note
```python
# You must declare
from FBTools import Start
FB = Start(cookie=cookie) # or
FB = Start(email=email, password=password) # or
FB = Start(phone=phone, password=password)
# When you want to run any feature of this package
```
<br>  
<br>

## Get Access Token
```python
from FBTools import Start
cookie = 'datr=nxbaxnynx; sb=axn...' # Input Your Cookie Here
Start(cookie=cookie)

from FBTools import GetToken
GT = GetToken()

TokenEAAG = GT.TokenEAAG()
TokenEAAB = GT.TokenEAAB()
TokenEAAD = GT.TokenEAAD()
TokenEAAC = GT.TokenEAAC()
TokenEAAF = GT.TokenEAAF()
TokenEABB = GT.TokenEABB()
```
<br>  
<br>

### Get Info Account
```python
from FBTools.GetInfo import GetInfoAccount

cookie = 'Input Cookie Here'
target = 'Input ID Target Here'

GIA = GetInfoAccount(cookie=cookie, target=target)
Profile = GIA.GetInfoProfile(general=True, friend=True, followers=True)

id         = Profile['id']
username   = Profile['username']
name       = Profile['name']
short_name = Profile['short_name']
hometown   = Profile['hometown']
location   = Profile['location']
friend     = Profile['friend']
followers  = Profile['followers']
```
Parameter  
>cookie : Your Facebook Cookie (string, default=None)  
target : ID/Username/URL Target Profile (string, default='me')  
general : Get General Information [id,username,name,shortname,hometown,location] (bool, default=True)  
friend : Get The Number Of Friends [friend] (bool, default=False)  
followers : Get The Number Of Followers [followers] (bool, default=False)  

Note  
>If you have logged in with cookies/email on Login(), you don't need to provide cookie parameters
<br>  
<br>

## Auto Post

### Parameter
```python
# Must Be Included
cookie  = 'Input Your Cookie Here'                           # Cookie (string, default=None)
text    = 'Hello! Test Bot Post'                             # Caption (string, default=None)
group   = '1824553201274304'                                 # Group ID (string, default=None)
# 'group' must include if post to group
# You must post at least 1 text or 1 photo

# Optional
url     = ['https://e.top4top.io/p_2916o42201.jpg']          # Picture URL (list, default=None)
tag     = ['1827084332','100000415317575','100000200420913'] # Friend ID You Want To Tag (list, default=None)
privacy = 1 # 1=Public, 2=Friends, 3=OnlyMe                  # Post Privacy (int, default=None)
```

### Post To Feed
```python
from FBTools import Start
cookie = 'datr=nxbaxnynx; sb=axn...' # Input Your Cookie Here
Start(cookie=cookie)

from FBTools import AutoPost
AP = AutoPost()
Post = AP.PostToFeed(text=text, url=url, tag=tag, privacy=privacy)
```

### Post To Group
```python
from FBTools import Start
cookie = 'datr=nxbaxnynx; sb=axn...' # Input Your Cookie Here
Start(cookie=cookie)

from FBTools import AutoPost
AP = AutoPost()
Post = AP.PostToGroup(group=group, text=text, url=url, tag=tag, privacy=privacy)
```

### Return
```python
{'status':'success','id':idpost,'message':None}
{'status':'pending','id':idpost,'message':'Pending Post'}
{'status':'failed','id':None,'message':'cookie invalid'}
{'status':'failed','id':None,'message':"Don't Create Same/Duplicate Post"}
{'status':'failed','id':None,'message':'Your Account Restricted To Post In Group'}
{'status':'failed','id':None,'message':'Terjadi Kesalahan'}
```

### Note
```python
# You must declare
from FBTools import Start
FB = Start(cookie=cookie) # or
FB = Start(email=email, password=password) # or
FB = Start(phone=phone, password=password)
# When you want to run any feature of this package
```
<br>  
<br>

## Auto Comment

### Parameter
```python
# Must Be Included
post   = 'Facebook.com/6929777330379375'                    # ID/URL Post Target (string, default=None)
text   = 'Hello! Test Bot Comment'                          # Caption (string, default=None)
# You must comment at least 1 text or photo

# Optional
cookie = 'Input Your Cookie Here'                           # Cookie (string, default=None)
photo  = 'https://e.top4top.io/p_2916o42201.jpg'            # Picture URL (string, default=None)
tag    = ['1827084332','100000415317575','100000200420913'] # Friend ID You Want To Tag (list, default=None)
```

### Comment To Post
```python
from FBTools import AutoComment as AC

Comment = AC.CommentToPost(cookie=cookie, post=post, text=text, photo=photo, tag=tag)
Exec = Comment.Execute()
```

### Return
```python
{'status':'success','id':comment_id,'message':None}
{'status':'failed','id':None,'message':'Spam Or Something Else'}
{'status':'failed','id':None,'message':'Terjadi Kesalahan'}
```

Note  
>If you have logged in with cookies/email on Login(), you don't need to provide cookie parameters
<br>  
<br>

## Auto React

### Parameter
```python
# Must Be Included
post   = 'Facebook.com/6929777330379375'                            # ID/URL Post Target (string, default=None)
react  = 2 # 1=Like, 2=Love, 3=Haha, 4=Wow, 5=Care, 6=Sad, 7=Angry  # Reaction Type (int, default=2=Love)

# Optional
cookie = 'Input Your Cookie Here'                                   # Cookie (string, default=None)
```

### React To Post
```python
from FBTools import AutoReact as AR

Reaction = AR.ReactToPost(cookie=cookie, post=post, react=react)
Exec = Reaction.Execute()
```

### Return
```python
{'status':'success','react_type':react_type,'message':None}
{'status':'failed','react_type':react_type,'message':'Spam Or Something Else'}
{'status':'failed','react_type':react_type,'message':'Terjadi Kesalahan'}
```

Note  
>If you have logged in with cookies/email on Login(), you don't need to provide cookie parameters
<br>  
<br>

## Auto Share

### Parameter
```python
# Must Be Included
post    = 'Facebook.com/6929777330379375'                    # ID/URL Post You Want To Share (string, default=None)
group   = '1824553201274304'                                 # Group ID (string, default=None)
# 'group' must include if share to group

# Optional
cookie  = 'Input Your Cookie Here'                           # Cookie (string, default=None)
text    = 'Hello! Test Bot Share'                            # Caption (string, default=None)
tag     = ['1827084332','100000415317575','100000200420913'] # Friend ID You Want To Tag (list, default=None)
privacy = 1 # 1=Public, 2=Friends, 3=OnlyMe                  # Share Privacy (int, default=None)
```

### Share To Feed
```python
from FBTools import AutoShare as AS

Share = AS.ShareToFeed(cookie=cookie, post=post, text=text, tag=tag, privacy=privacy)
Exec  = Share.Execute()
```

### Share To Group
```python
from FBTools import AutoShare as AS

Share = AS.ShareToGroup(cookie=cookie, post=post, group=group, text=text, tag=tag, privacy=privacy)
Exec  = Share.Execute()
```

### Return
```python
{'status':'success','id':idshare,'message':None}
{'status':'pending','id':idshare,'message':'Pending Post'}
{'status':'failed','id':None,'message':"Don't Create Same/Duplicate Post"}
{'status':'failed','id':None,'message':'Your Account Restricted To Post In Group'}
{'status':'failed','id':None,'message':'Terjadi Kesalahan'}
```

Note  
>If you have logged in with cookies/email on Login(), you don't need to provide cookie parameters
<br>  
<br>

