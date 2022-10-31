# BeautifulSoup_Python
![image](https://user-images.githubusercontent.com/70150896/198918863-890cfc97-f558-4026-a932-63f514a35088.png)

# sorce code
from flask import Flask

from urllib import request

from bs4 import BeautifulSoup

app = Flask(__name__)
@app.route("/")

def hello():

    target = request.urlopen("http://www.kma.go.kr/weather/forecast/mid-term-rss3.jsp?stnId=108")
    soup = BeautifulSoup(target, "html.parser")

    output = ""
    for location in soup.select("location"):
        output += "<h3>{}</h3>".format(location.select_one("city").string)
        output += "날씨:{}<br/>".format(location.select_one("wf").string)
        output += "최저/최고 기온: {}/{}"\
            .format(\
                location.select_one("tmn").string,\
                location.select_one("tmx").string\
            )
        output += "<hr/>"
    return output

# cmd
![image](https://user-images.githubusercontent.com/70150896/198918921-82047f7f-bad0-4439-baf0-b65e046dde5c.png)

# result
![image](https://user-images.githubusercontent.com/70150896/198918788-748560a5-1138-4bb1-90f5-9f344107657e.png)
