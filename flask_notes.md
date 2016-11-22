
####Introduction
###学习flask过程中练习的小例子
功能：注册、登陆、更改密码

####服务器端：
<pre><code>  
from flask import Flask,request,render_template,Response,abort,url_for,redirect
import time
import datetime
import json
import sqlite3

app = Flask(__name__)

i=datetime.datetime.now()
@app.route( '/') #显示当前日期，最简单的例子
def hello_world ():
    return ('今天是%s年%s月%s日' %(i.year,i.month,i.day))

@app.route( '/login',methods=['POST' ]) # 登陆页面
def login ():
    dic=request.get_json(force= True) #得到客户端提交的数据，并强制转化成json类型数据
    conn=sqlite3.connect( 'userinfo.db')
    u=(dic[ 'username'],) #查询方法要求的参数的数据类型是tuple
    p=(dic[ 'password'],)
    cur=conn.cursor()
    cur.execute('SELECT username FROM users WHERE username=?' ,u)
    this_name=( cur.fetchone())[0 ]
    cur.execute('SELECT password FROM users WHERE username=?' ,u)
    this_password=( cur.fetchone())[0 ]
    conn.close()
    if(len (dic)==2):
        if(this_name==dic['username' ] and this_password==dic[ 'password']):
          #return request.form['username']
          #dic=request.get_json(force=True)
            res = Response( 'add cookies')
            res.set_cookie( 'username',dic['username' ],expires=time.time()+6* 60)
            return res
        else:
            return 'username or password error'
    else:
        return redirect(url_for('register' )) #重定向到register页面
        #abort(401) #显示401错误页面 
        #error = 'Invalid username/password'
        #return error
    #return request.form['info'] 
    #print (repr(request.form['password']))
    #print (repr(request.get_json(force=True)))

    #return request.form.__str__()
    #dic=request.get_json(force=True)
    #return dic['password']
    #return request.get_json(force=True).__str__()
    #return request.args.get('name', '')

@app.route( '/register',methods=['POST' ]) # 注册页面
def register ():
    dic=request.get_json(force= True)
    u=dic[ 'username']
    p=dic[ 'password']
    conn=sqlite3.connect( 'userinfo.db')
    cur=conn.cursor()
    cur.execute("CREATE TABLE IF NOT EXISTS users(username text,password text)" )
    cur.execute("SELECT username FROM users WHERE username=?" ,(u,))
    this_name= cur.fetchone()
    if(not bool(this_name)):
        cur.execute("INSERT INTO users VALUES(?,?)" ,(u,p))
    else:
        return 'user is exist!'
    conn.commit()
    na=( 'zhang',)
    cur.execute("SELECT username FROM users WHERE username=?" ,na)
    #for row in cur.execute("SELECT * FROM users"):
    #print(row[0])
    print(cur .fetchone())
    conn.close()
    return 'success'

@app.route( '/add',methods=['POST' ])
def setcookie ():
    dic=request.get_json(force= True)
    res = Response( 'add cookies')
    res.set_cookie( 'username',dic['username' ],expires=time.time()+6* 60)
    return res
    #return request.cookies.get('username')

@app.route( '/show')
def show ():
    if(request.cookies):
        return request.cookies.__str__()
    else:
        return redirect(url_for('login' ))
    #return request.cookies.__str__()

@app.route( '/del')
def del_cookie ():
    res = Response( 'delete cookies')
    res.set_cookie( 'name', '' , expires=0)
    # print res.headers
    # print res.data
    return res

@app.route( '/updatepassword',methods=['POST' ]) #已登陆的情况下可以修改密码，否则重定向到登陆界面
def updatepassword ():
    dic=request.get_json(force= True)
    newpass=dic[ 'password']

    if(request.cookies):
        user=request.cookies[ 'username']
        conn=sqlite3.connect( 'userinfo.db')
        cur=conn.cursor()
        cur.execute("update users set password=? where username=?" ,(newpass,user))
        conn.commit()
        conn.close()
        return 'update success'
    else:
        return redirect(url_for('login' ))

if __name__ == '__main__' :
    app.run(host= '0.0.0.0',port=12580 ,debug=True)
                                      
</code></pre>

####客户端：
<pre><code>http get localhost:12580/ </code></pre>
向服务器发送get请求，get可以省略
<pre><code>http post localhost:12580/register username=zhang password=123 -v --session zzz</code></pre>
端口号被设置为12580，post方法提交数据给服务器，-v表示显示详细信息，--session zzz 表示操作在名字为zzz的session中
<pre><code>http --help </code></pre>
可以查看关于httpie的文档
####Reference
flask中文文档(http://docs.jinkan.org/docs/flask/index.html)




