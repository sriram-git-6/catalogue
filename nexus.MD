1. Install nexus by taking one t3.medium instance and download the file from this location

    https://help.sonatype.com/en/download.html

2. After building, we need to push the zip file with version into the nexus repo. So to do this, we need to install one plugin

   to push the artifactory into the nexus repo 

3. Install nexus artifact uploader plugin     

4. login into the nexus repo and create the repository
 
    Name: catalogue
    
    version policy : mixed
    
    layout policy: permissive
    
    strict content type validation: uncheck the box
    
    deployment policy: allow redeploy # if disable this you can cannot deploy the same version of software multiple types

    click on create repository

5. Now upload the package through pipeline

   