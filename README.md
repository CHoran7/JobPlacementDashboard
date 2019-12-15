# Live Project
## Introduction
During my time at The Tech Academy I completed three live projects. Each live project was worked on in a two week sprint. The first was a Python project using the Django framework. This was a website for an imaginary space bar, and students worked on different applications for the page. The next two projects were completed in C# working with in Visual Studio. This was a website page for a construction company displaying different schedules, jobs and other things their employees or admins might need. The first sprint was the web developement sprint and then the back end sprint.

## Creating a Mining Wiki
One of the stories was to create a wiki scraping information from a specific section of a Wikipedia page.
  
  ```
  page = requests.get("https://en.wikipedia.org/wiki/Asteroid_mining")
  soup = BeautifulSoup(page.content, 'html.parser')
  ```
  
This code simply grabs the Wikipedia page that I took information from.

```
  textSurfaceMining = soup.find_all('p')[24].get_text().replace("[22]", "").replace("[34]", "")
  textShaftMining = soup.find_all('p')[25].get_text()
  textMagneticRakes = soup.find_all('p')[26].get_text().replace("[22]", "").replace("[35]", "")
  textHeating = soup.find_all('p')[27].get_text().replace("[36]", "").replace("[37]", "").replace("[38]", "") + soup.find_all('p')[28].get_text().replace("[22]", "").replace("[39]", "")
  textMondProcess = soup.find_all('p')[29].get_text().replace("[40][41][42]", "")
  textSelfReplicating = soup.find_all('p')[30].get_text().replace("[43]", "").replace("[44]", "").replace("[45]", "")
  ```
  
This code is an example of grabbing the individual paragraphs and replacing the references to the articles on the Wikipedia pages because those will mean nothing to this web pages' reader.

```
  def miningWiki(request):
      context = {'Title': textTitle, 'secTitle1': textSection1, 'secTitle2': textSection2, 'secTitle3': textSection3, 'secTitle4': textSection4, 'secTitle5': textSection5, 'secTitle6': textSection6, 'p1': textSurfaceMining, 'p2': textShaftMining, 'p3': textMagneticRakes, 'p4': textHeating, 'p5': textMondProcess, 'p6': textSelfReplicating,}
      return render(request, 'miningWiki/miningWiki.html', context)
 ```

This code is just an example of turning my text into dictionaries so I can call them later in the HTML code. It also showcases the render function that will often be used in Django.

Suntracker App
The function of this app was merely to tell the user when the sunrises and sets at their location for the current day.

```
  info = requests.get("http://ip-api.com/json/?fields=lat,lon")
  ```
  
The first API, ip-api, would take the parameters lat and lon specified by the code above and return the ip addresses longitude and latitude. I will need this to feed the longitude and latitude to the next API which will tell me the sunrise and sunset at that location.

```
  suncalc = requests.get("https://api.sunrise-sunset.org/json?" + location + "&formatted=0")
  ```
  
This is a call to the other API where location is a string containing the latitude and longitude information gathered earlier. This also returns the information in a specific format so it was easier for me to work with.

```
  def datetime_from_utc_to_local(utc_datetime):
    now_timestamp = time.time()
    offset = datetime.fromtimestamp(now_timestamp) - datetime.utcfromtimestamp(now_timestamp)
    return utc_datetime + offset
   ```
    
This function will convert the time to the users timezone. The times I originally had were always in UTC which isn't convenient for the user.

Other Things Learned
Of course this was all done in the Django framework so I had to do research on how the Django framework works. This includes learning about models, views, urls and templates. All of this was necessary in order to get this project to work. I learned great communication skills from this project as well as developed my problem solving skills in coding. While this mostly involves googling things there is a certain skill to it.
