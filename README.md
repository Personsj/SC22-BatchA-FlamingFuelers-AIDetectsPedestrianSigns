# Final Steps

Do functionality check of frontend features on both webpages (try out all the buttons and links making sure they work properly)

Implement backend features, specifically text to speech in results page

Modify the backend code to have a confidence cutoff for predictions (maybe need 0.5 conf to show result)

update readme

Research other features that you guys are interested in - maybe a button to read out project description to user, or links to each of your githubs by clicking on your picture


# Our Project - AI Detects Pedestrian Signs
#### by: 

### Our Project's Purpose \+ Features

Our Computer Vision project detects common pedestrian signs by the road. Then, it voices out these pieces of information out loud. This is meant to support visually impaired pedestrians, who wouldn’t be able to use their canes to understand these aspects of their surroundings, so that they can more safely navigate around.

### Why We Chose This Project

When we began to brainstorm for projects that we could do, we decided that we would like to create something that would help people with disabilities or just anyone who needed the help. All of our ideas helped people, but this project just seemed to help people more. Sight is one of our senses that shapes society more than others, as signs and other visuals are used to maintain discipline, indicate hazards, and more, so we chose to help people who are visually impaired. However, there are so many different signs in the world, and developing a project within 3 weeks with all the signs would be extremely difficult. As a result, we decided as a team to focus on signs displayed on sidewalks and roads, where people who cannot rely on sight may be unsafe, due to cars and other vehicles. These are a few reasons for why we chose this project.

### Classes of Signs that Our Project can Detect

##### go-cross

This class is dedicated to the electronic crossing sign that you often see on the opposite street when crossing. It is different from the yellow crossing\-sign since it DOES dictate whether it is safe to cross at that very moment. 

##### no-pedestrians

A sign that indicates the area is not a pedestrian\-safe zone. 

##### pedestrian\-stop\-signal

This class is dedicated to the electronic crossing sign that indicates it is NOT okay to cross at the moment, due to moving traffic. It appears in the shape of a hand. 

##### schoolzone\-crossing

This sign indicates that the user is entering a school zone, where crosswalks are likely to be present and crossing guards may be present \(during school hours\). 

##### stop sign

The "stop sign" class refers to the standard red octagonal stop sign with the word “stop” on it.

##### stop-donotproceed

The "stop-donotproceed" class refers to the “Do not enter” sign. It's the sign which has a red circle with a white horizontal line in the middle. This sign indicates the one should not continue walking in that direction.

##### crossing-sign

The "crossing-sign" class consists of signs with pedestrians on them, which indicate where one can cross the road. This class does not include the electrical crosswalk signs.

##### caution

The "caution" class is dedicated to yellow signs with exclamation marks on them. These signs are either a triangle or a rhombus. This class is meant for road signs - not for indoor purposes, like the “caution! Wet floor” sign.

### Setbacks

Throughout the process, we faced several roadblocks. Here are a few:

- The more we trained, the lower the precision became
- The caution class had an abnormally low precision compared to our other classes
- There were many different versions of the same sign, so we had to figure out which version of each sign we would use.
- The text to speech feature was hard to incorporate.

### Techstack

Some tools we used include ...

   - Labeling Data: Roboflow
   - Training the Machine: YOLOv5
   - Transforming 2D Visual text into Machine Readable text: OCR 
   - Text to Speech: gTTS 
   - Website Backend: Flask

# Computer Vision Web Scaffold

A scaffold for deploying dockerized flask applications.

If you have any questions, feel free to open an issue on [Github](https://github.com/organization-x/omni/issues).

### Video Guide

[![Deploy a Web Project with Flask](https://img.youtube.com/vi/JUb-PpejA7w/0.jpg)](https://youtu.be/JUb-PpejA7w "Deploy a Web Project with Flask")

This guide covers how you can quickly deploy most projects with the [Flask](https://flask.palletsprojects.com/) framework and our omni scaffold.

### Quickstart Guide for Local Development

First clone this repository through 

`https://github.com/organization-x/omni`

cd into the `/app` folder

`python3 -m pip install -r requirements.txt`

edit line 29 the `main.py` file to either the URL of the cocalc server you are on or `localhost` if you are running it on your own PC

Then, clone ultralytics yolov5 in the app folder, by running 

`git clone https://github.com/ultralytics/yolov5`
`pip install -r yolov5/requirements.txt`

Run

 `python3 -m main`

to start the server on local, most changes while developing will be picked up in realtime by the server

### Quickstart Guide for Local Deployment

Make sure docker is installed on your system. Look that up if you don't know what that means.

cd into the root director of the repo then run 

`docker build -t omni .`

once built, run

`docker run -d -p 9000:80 --restart=unless-stopped --name omni omni`

you should then be able to see the `omni` container running when you run 

`docker ps -a`

if it seems to be stuck (i.e. constantly listed as `Restarting`), something is wrong with the docker image or code inside causing it to repeatedly fail.

you can start debugging the project by running 

`docker logs -f omni` 

or

`docker exec -it omni /bin/bash` for an interactive bash terminal (this option only works if the container is running and not stuck in a restart loop)

### Common Issues

`$'\r': command not found` when attempting to start docker container

this is caused by the the `entrypoint.sh` script somehow having CLRF line endings instead of LF line endings.

to fix this run

`sed -i 's/\r$//' entrypoint.sh`

### File Structure

The files/directories which you will need to edit are **bolded**

**DO NOT TOUCH OTHER FILES. THIS MAY RESULT IN YOUR PROJECT BEING UNABLE TO RUN**

- .gitignore
- config.py
- Dockerfile
- READMD.md
- entrypoint.sh
- nginx_host
- host_config
- app/
     - **main.py**
     - **best.pt** <- you will need to upload this yourself after cloning the repo when developing the site
     - **requirements.txt**
     - **utils.py**
     - templates/
          - **index.html**

### How to upload best.pt to your file structure?

Run 
`cp ../path/to/best.pt best.pt`

### best.pt ###

The weights file - must upload if you are running file on coding center or are trying to deploy.

### main.py ###

Contains the main flask app itself.

### requirements.txt ###

Contains list of packages and modules required to run the flask app. Edit only if you are using additional packages that need to be pip installed in order to run the project.

To generate a requirements.txt file you can run

`pip list --format=freeze > app/requirements.txt`

the requirements.txt file will then be updated. Keep in mind: some packages you install on one operating system may not be available on another. You will have to debug and resolve this yourself if this is the case.

### static/ ###

Contains the static images, CSS, & JS files used by the flask app for the webpage. You will need to create this and put files in it. Place all your images used for your website in static/images/ so that you can then reference them in your html files.

### utils.py ###

Contains common functions used by the flask app. Put things here that are used more than once in the flask app.

### templates/ ###

Contains the HTML pages used for the webpage. Edit these to fit your project. index.html is the demo page.

### Files used for deployment ###

`config.py`
`Dockerfile`
`entrypoint.sh`
`nginx_host`
`host_config`
**Only modify `host_config`. Do not touch the other files.**

