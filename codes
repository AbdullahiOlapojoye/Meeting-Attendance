from google.colab import files
import re  
from urllib.request import urlopen
import json
import copy
import matplotlib.pyplot as plt

#defining a function that will extract the codes and return the codes&count
def country_connect_count(text_data): 
  new_dict = {}
  #join all the items in the read data for string operations
  joined_data = "".join(i for i in text_data)
  #find all items in bracket
  extracted_data = re.findall(r"\(.*?\)", joined_data)
  #count occurence
  for k in extracted_data:
    # remove spaces and brackets
    i = re.sub(r"[\(\)]",'', str(k))
    item = re.sub(r"\s+", "", str(i))
    if item in new_dict:
      new_dict[item] += 1
    else:
      new_dict[item] = 1
  return new_dict

def format_country_code(x, y):
  url = "https://pkgstore.datahub.io/core/country-list/data_json/data/8c458f2d15d9f2119654b29ede6e45b8/data_json.json" 
  # store the response of URL
  response = urlopen(url) 
  country_name_and_code = json.loads(response.read())
  for j in country_name_and_code: 
    for a in x:
      if j['Code'] == a:
        x[a] = j['Name']
  formatted_list = {x[k]:v for k, v in y.items()}
  sorted_countries_list = sorted(formatted_list.items(), key=lambda x:x[1], reverse = True)
  return sorted_countries_list[0:20]

def plot_results(data):
  ind = []
  fre = []
  for item in data:
    ind.append(item[0])
    fre.append(item[1])
  fig, ax = plt.subplots(figsize =(16, 9))
# barplot
  ax.barh(ind, fre)
  # Remove axes splines
  for s in ['top', 'bottom', 'left', 'right']:
      ax.spines[s].set_visible(False)
  # pad between axes and labels
  ax.xaxis.set_tick_params(pad = 5)
  ax.yaxis.set_tick_params(pad = 10)
  # gridlines
  ax.grid(b = True, color ='grey',
          linestyle ='-.', linewidth = 0.5,
          alpha = 0.2)
  # Show descending order
  ax.invert_yaxis()
  
  # bars notation
  for i in ax.patches:
      plt.text(i.get_width()+0.2, i.get_y()+0.5,
              str(round((i.get_width()), 2)),
              fontsize = 10, fontweight ='bold',
              color ='grey')
  # plot title
  ax.set_title('Meeting attendance by countries (Top 20)',
              loc ='left', )
  # watermark
  fig.text(0.9, 0.15, 'Olapojoye2022', fontsize = 12,
          color ='grey', ha ='right', va ='bottom',
          alpha = 0.7)
  # Show Plot
  plt.show()


#Calling the defined functions
text_file = open("divine_freedom.txt")
country_codes = country_connect_count(text_file)
original_country_count = copy.deepcopy(country_codes)
formatted_countries_list = format_country_code(original_country_count, country_codes)
plot_results(formatted_countries_list)
