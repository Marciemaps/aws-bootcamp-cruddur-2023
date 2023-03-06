# Week 2 — Distributed Tracing

Honeycomb 

I am going to instrument the backend flask application to use Open Telemetry (OTEL) with Honeycomb.io as the provider. Honeycomb is an observability solution that shows patterns and outliers of how users experience code in complex and unpredicatble environments.
Honeycomb is not in the environment, the environment sends standardized messages to Honeycomb and stored in the database.

1. Open your gitpod from the main branch.
1a. Sign up or log into your Honeycomb app (watch @Giftedlane's video for the setup)
1b. Create an environment and you can call it "bootcamp".
        - You will find your API Keys, copy-paste in your gitpod empty page. 
           -export HONEYCOMB_API_KEY= ""
           -gp env HONEYCOMB_API_KEY= ""

2.  export HONEYCOMB_SERVICE_NAME= "Crudder"
2a. gp env HONEYCOMB_SERVICE_NAME= "Crudder"
   -Paste this into your terminal
   

3. I copy-pasted the above code with my keys into the terminal.
   - Check if it has been set: env | grep HONEY

I will configure OTEL(Opentelementy) this sends the data to Honeycomb
4. Copy-paste OTEL_SERVICE_NAME: 'backend-flask' into the docker-compose.yml file in line 6 under "BACKEND_URL"
4.a Copy-paste the first two lines from : "Add the following Env Vars to backend in docker-compose" under after line 7

I opened a new terminal(Bash) to make sure that the service name is set: env | grep HONEYCOMB

![Honeycomb Instrument](https://user-images.githubusercontent.com/95619710/223202228-1da147c7-d115-4baa-b0b2-03c00f2719e7.png)



5. Open requirements.txt in backend-flask, copy-paste the first code in Github from under "Honeycomb" into the requirements.txt folder into line 4
5a. In the terminal, add the dependencies: copy-paste: pip install -r requirements.txt
5b. Next " Add to the app.py" using the code from Github or the ones in the Honeycomb. Add to line 16 and name it " #Honeycomb ---------"
5c. Copy-paste the 2nd paragraph next and name it "Honeycomb-----"
5d. Copy-paste the last paragraph. The 2nd line place it on its own as this may cause an error.
   Output should look like this: 

   app = Flask(_name_)
   FlaskInstrumentor().instrument_app(app)
   RequestsInstrumentor().instrument()

I used the documentation: Opentelemetry Python.
Now: 
1. cd ..(you should be in the main file)
2. Docker Compose up
2a. Checked my docker container for any potential changes by checking the logs by right clicking.
3. Unlock your ports.

* Permanent unlocking of the locks: 
 - Add the ports code from github week 2 to gitpod yml line 15
**Commit** - "Add additional ports
Open the application and the data of the frontend should show up

In Honeycomb open datasets ( you may not see anything, if not check at the bottom for the troubleshooting)

1. In the dockerfile folder open Backend-flask in services select (home_activities)
1a. Copy-paste the first line from "Acquiring a Tracer" & paste into line 2 then copy-paste: tracer= trace.get_tracer("home.activities")------into line 4 (used the Honeycomb opentelemetry python documentation)
2. Copy-paste "the creating Spans" Code in line 3 and paste in the: homeactivities
                                                                    def run (): above "now"
                                                                    replace within the () with ("home-activities-mock-data")
3. Check honeycomb for data
4. Copy-paste from "Adding Span Attribute" the last two code lines: 
   span = trace.get_current_span()
   now
   span.set_attribute("app.now", now isoformant())
4. At the bottom-above "return result" copy-paste "span.set_attribute("app.result_length", len(results())

![HoneyComb Data](https://user-images.githubusercontent.com/95619710/223202584-83bf86a6-0823-4b33-a7e3-bb30ad9890f1.png)

Instrument XRay AWS
XRAY AWS helps to analyze behaviour of distributed apps by providing request tracing, exception collection & profiling capabilities
Documentation: SDK'S Ffor Python (Boto3) search for Xray( github.com/aws/aws-xray-sdk-python

Opened my gitpod
* For x ray to work you have to have Daemon(This sends data to x ray)

1. NPM i (cd into frontend-react-js)
 - To permanently have it in the code add the following code to gitpod.yml under:
   cd $Theia...
 - name: react-js
 command:
   cd frontend-react-js
   npm i
2. Commit to code: Update gitpod yml to install npmi

Go back to your main branch: 
a) cd ..
b) ls
c) clear

3. From the "Add to the requirements.txt' code paste to requirements.txt in the backend flask tab into  line 10
now: 
a) ls
b) cd backend-flask/
c) pip install -r requirements.txt

Now I will setup the sampling rates: 
4. From the "Add to app.py" copy the first two lines into app.py in line 26 and name it #Xray ------
   The last two  lines will be in line 36 with the same #Xray-----
Note the change for line 38 : xray_recorder.configure(service = 'backend-flask,',....
Xray middleware place in line 49

5. From " Setup AWS Resources " add the code to aws/json folder and name the file xray.json
a) Change the "ServiceName" to "backend-flask",
b) "AWS xray create group.. "service(\"backend-flask\") into the terminal

![Xray](https://user-images.githubusercontent.com/95619710/223203351-73b58edb-142b-4df0-85f7-c528a0a30e40.png)

![Xray](https://user-images.githubusercontent.com/95619710/223203384-3a881545-7290-4b56-8038-7f1d37450c81.png)

INSTALL DAEMON

1. From "Add Daemon Service to Docker Compose" paste into DockerCompose.yml under volumes: 
                                                                                  -/frontend-react-js
a) make sure to correct you location
b) From "Env vars' code to the backend-flask in docker-compose under OTEL_EXPORTER

2. Commit the code: Instrument Xray then compose up
3. Check ports and logs, look for data in xray under traces
4. Commit: Xray is now working

What I struggled with: 

-I struggled with the add subsegments area and I may have messed up my code. 
-I also have been struggling with codespaces and this potentially has more than confused me.
-I will take the time to learn codespaces to better understand it and hopefully will manage to redo or fix code that may have been messed up



