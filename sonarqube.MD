1. launch one t3.medium machine and install sonarqube

    https://docs.sonarsource.com/sonarqube/latest/try-out-sonarqube/

2. Install sonar scanner on jenkins agent machine (i;e on catalogue machine)

3. Informing sonar qube scanner, the details of sonar qube server

    after installing sonar scanner on the the agent machine go to 

    cd sonar/conf ---> sonar-scanner.properties file will be available

4. open that file vi sonar-scanner.properties and give the sonar qube server ip

    --------------------Default Sonarqube server
    sonar.host.url=http://172.31.17.177:9000 
    sonar.login = hkjdhfjwehlkfhewrifwelkflkrh
    
5. for authentication create token in sonar qube console going to myaccount/security/generate tokens/ give the token name 
   
   (jenkins token) and generate the token and give that token below the sonarqube server ip in this file.

   sonar.login = hkjdhfjwehlkfhewrifwelkflkrh

6. As a devops engineer we need to create quality gates :

   1. predefined sets of conditions or rules that are applied to code during the code analysis process. 

   2. These quality gates act as checkpoints to ensure that the code meets certain quality criteria before it can be considered 
   
      acceptable for deployment or further development.   

   3. create quality gate in sonarqube with name "roboshop" and create condition on overall code or on new code 

      create quality gate for code coverage that code coverage should not be less than 80% and another condition is security review 
      
      rating should not be less than A. And code smells should greater than 0 and bugs greater than 0.

   4. Apply this quality gate on our catalogue project.    

sonar.qualitygate.wait=true:
  
  process of code scanning and evaluation, performed by SonarQube, will be completed immediately without waiting for the Quality Gate 
  
  status to be determined. 

Code smells: SonarQube refer to certain patterns or structures in code that indicate potential problems or areas for improvement. 
   
   These aren't necessarily bugs, but they can make the code harder to maintain, understand, or extend. SonarQube uses static code 
   
   analysis to detect these smells automatically. 