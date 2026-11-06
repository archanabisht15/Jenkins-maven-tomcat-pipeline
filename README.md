# Cab Booking Website: Jenkins CI/CD Pipeline with Tomcat

I built an automated pipeline that takes code from GitHub, builds it with Maven,
and deploys it to an Apache Tomcat server using Jenkins.

## About This Project
- The website is a taxi booking site (HTML, CSS, JavaScript). It comes from an open-source project:
  [CloudNinjaa/cab-booking](https://github.com/CloudNinjaa/cab-booking) (I forked it).
- The website has no database and no backend code. The booking form is only the front end.
- **My work:** the Jenkins pipeline (`Jenkinsfile`), the Jenkins setup, the Tomcat server setup,
  and the automatic deployment.

## Tools Used
- Git and GitHub
- Jenkins (pipeline as code)
- Maven (builds the WAR file)
- Apache Tomcat (runs the website)
- Linux server

## How the Pipeline Works
Code on GitHub (`prod` branch) -> webhook -> Jenkins -> Maven build -> WAR file -> Tomcat server

| Step | What it does |
|---|---|
| Checkout | Downloads the latest code from the `prod` branch |
| Verify Maven | Checks that Maven and Java are installed |
| Build | Runs `mvn clean package` to create the WAR file |
| Archive Artifact | Saves the WAR file in Jenkins |
| Deploy to Tomcat | Copies the WAR file to Tomcat's `webapps` folder over SSH |
| Verify Deployment | Logs in to the server and checks that the file is there |

After every run, Jenkins prints a success or failure message and cleans its workspace.

## What I Set Up
- Jenkins with Maven configured
- SSH key saved in Jenkins credentials, so no passwords are written in the code
- Tomcat installed and configured on the server
- A GitHub webhook, so Jenkins starts the pipeline automatically on every push
- A `Jenkinsfile` that runs the whole process automatically

## How to Run
1. Push code to the `prod` branch. The GitHub webhook triggers the Jenkins pipeline automatically.
2. Jenkins builds the project and deploys it to Tomcat.
3. Open the website: `http://<server-ip>:8080/taxi-booking-1.0.1/`

## Screenshots
![Website running on Tomcat](screenshots/website.png)

## Author
Archana Bisht | [LinkedIn](https://www.linkedin.com/in/archanabisht15) | [GitHub](https://github.com/archanabisht15)

