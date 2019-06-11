```python
from aguaclara.core.units import unit_registry as u
from aguaclara.core import physchem as pc
from aguaclara.core import pipes as pipes
from aguaclara.core import utility as ut
from aguaclara.core import constants as con
from aguaclara.research import floc_model as fm
import pandas as pd
import numpy as np
import matplotlib.pyplot as plt
import urllib
from urllib.request import urlopen
from bs4 import BeautifulSoup

filepath = 'DC/SelectUnitOpsData.xlsx'
xls = pd.ExcelFile(filepath)
contaminantsheet = pd.read_excel(xls, 'contaminants')
df2 = pd.read_excel(xls, 'unitops')
len(df1)
contaminantsheet.Contaminant[1]

epaurltemplate = 'https://safewater.zendesk.com/hc/en-us/articles/211403778-7-How-will-contaminant-be-removed-from-my-drinking-water-'
epaurl = epaurltemplate.replace("contaminant",contaminantsheet.Contaminant[4])
epaurl

allunitops=[]
allepatext=[]
junk="myjunk"
allepatext.append(junk)
allepatext

allepatext=[]
epaurl=[]
for i in range(len(contaminantsheet)):
  epaurl.append(epaurltemplate.replace("contaminant",contaminantsheet.Contaminant[i]))

i=10
epaurl[i]

html = urlopen(epaurl[i]).read()
html
soup = BeautifulSoup(html, "lxml")
for script in soup(["script", "style"]):
    script.extract()    # rip it out

# get text
epatext = soup.get_text()
epatext

for i in range(len(contaminantsheet)):
  epaurl = epaurltemplate.replace("contaminant",contaminantsheet.Contaminant[i])
  html = urlopen(epaurl).read()
  soup = BeautifulSoup(html, "lxml")

  # kill all script and style elements
  for script in soup(["script", "style"]):
      script.extract()    # rip it out

  # get text
  epatext = soup.get_text()

  # break into lines and remove leading and trailing space on each
  lines = (line.strip() for line in epatext.splitlines())
  # break multi-headlines into a line each
  chunks = (phrase.strip() for line in lines for phrase in line.split("  "))
  # drop blank lines
  epatext = '\n'.join(chunk for chunk in chunks if chunk)
  allepatext.append(epatext)

allepatext[5]

((((epatext.partition("to below")[2]).partition(":"))[2]).partition("."))[0]

unitopnames = ["coagulation/filtration","reverse osmosis"]
len(unitopnames)
unitopbools = [False] * len(unitopnames)

for i in range(len(unitopnames)):
  unitopbools[i] = epatext.find(unitopnames[i]) > 0

unitopbools


text.find("coagulation/filtration")
text.find("reverse osmosis")



<a data-p_id="201454937" class="parent_cat" href="https://safewater.zendesk.com/hc/en-us/categories/201454937-Fact-Sheets">Fact Sheets</a>
epaurl = "https://safewater.zendesk.com/hc/en-us/categories/201454937-Fact-Sheets"
html = urlopen(epaurl).read()
soup = BeautifulSoup(html, "lxml")
soup
# kill all script and style elements
for script in soup(["script", "style"]):
    script.extract()    # rip it out
epatext = soup.get_text()
epatext

```
