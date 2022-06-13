
import random,requests,json
from flask import Flask
from bs4 import BeautifulSoup

app = Flask(__name__)

@app.route('/')

def index():
    return "Hi"


@app.route('/combo/', methods=['GET'])
def info():
 v = []
 o = []
 lista = []
 
 url = 'https://hihi2.com/category/real-madrid-news/'
 headers={
 "Accept-Language": "ar-IQ,ar;q=0.9,en-IQ;q=0.8,en;q=0.7,es-IQ;q=0.6,es;q=0.5,en-US;q=0.4",
 'user-agent':'Mozilla/5.0 (X11; Linux x86_64) AppleWebKit/537.36 (KHTML, like Gecko) Chrome/96.0.4664.46 Safari/537.36'
  }
 s = requests.get(url,headers=headers)
 soup = BeautifulSoup(s.content, "html.parser")
 ob = soup.find_all("div", {"class":"entry-excerpt"})
 mm = soup.find_all("span",{"class":"entry-date"})
 for i in range(len(ob)):
  v.append(ob[i].text)
 for i in range(len(mm)):
  o.append(mm[i].text)
 for x in range(len(o)):
  dat = str(' '+v[x]+'الوقت:'+o[x])
  lista.append(dat)
 for mm in lista:
  m = {
  'status':'true',
  'title':mm,
   }

  return json.dumps(m,ensure_ascii=False)
  
app.run()
