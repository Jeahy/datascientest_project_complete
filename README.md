# New York Times API Data Pipeline - Course Project

<img src="https://github.com/Jeahy/datascientest_project_complete/blob/main/images/nyt_developers.png" align="centre">

Final Project of the DataScientest Data Engineer Course
created in collaboration with [KSuljic](https://github.com/KSuljic) and [AdelRCh](https://github.com/AdelRCh)



## Architecture 
![Pipeline Architecture](https://github.com/Jeahy/datascientest_project_complete/blob/main/images/architecture.png)

Pipeline Consists of various modules:

1. Data Mining
   - requests library
3. Database
   - MongoDB
   - database: NY_Project
   - collections: ny_articles, ny_articles_aggregated_data, times_newswire
   - JSON format
5. Data Aggregation
   - PyMongo Pipeline
   - saving aggregated data in collection
7. Data Serving
   a) Website
     - Dash/Plotly
   b) API
     - FastApi
     - Basic Authentication
9. Dockerization
    - Docker-Compose
    - Network
    - several ports
    - volume



## Project Task
![Project Task](https://github.com/Jeahy/datascientest_project_complete/blob/main/images/project_task.png)

My contributions:
- basic Dash website
- API
- request script to load book review data in database (that we didn't need in the end)



## Dash Website
![Project Task](https://github.com/Jeahy/datascientest_project_complete/blob/main/images/dash_page.png)

The Dash page provides:
- some basic stats: number of articles and average wordcount
- 5 latest articels that have been loaded into the database
- live article search
- on another page the average word count per article per section



## API
![Project Task](https://github.com/Jeahy/datascientest_project_complete/blob/main/images/api1.png)
![Project Task](https://github.com/Jeahy/datascientest_project_complete/blob/main/images/api2.png)
The Dash page provides:
- some basic stats: number of articles and average wordcount
- 5 latest articels that have been loaded into the database
- live article search
- on another page the average word count per article per section

```
tbd
```

