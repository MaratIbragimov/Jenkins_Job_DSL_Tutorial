
## Groovy job DSL script with docker publish:
In the previous step we built the application and started it manually using `npm start`.
In this section we will dockerize and push the application to **docker-hub**.



## Jobs DSL plugin installation:

* Open Jenkins

* Navigate to **Manage Jenkins -> Manage plugins**, select **available** tab and insall **Jobs DSL** plugin

* Click **download now and install after restart**

* Check **Restart Jenkins when installation is completed and no jobs are running**


## Create a new jenkins job:

* Open Jenkins

* Click on **New Item**

* Select **Frestyle project**

* Enter projects name e.g **Job DSL with docker publish example**

* Click ok

* In jobs configuration go to **Source management** and select **Git**

* Enter the url of the git repository that contains your Jenkins jobs DSL e.g https://github.com/marat643/Jenkins_Job_DSL_Tutorial.git

* Go to **Build** section and click on **Add a build step** and select **Process job DSLs** 

* In **DSL Scripts** enter the relative path of the **groovy** file **Jenkins_Job_DSL/nodejsdocker.groovy**, this file contains the commands:
```groovy

job('NodeJS Docker example') {
    scm {
        git('git://github.com/wardviaene/docker-demo.git') {  node -> // is hudson.plugins.git.GitSCM
            node / gitConfigName('DSL User')
            node / gitConfigEmail('jenkins-dsl@newtech.academy')
        }
    }
    triggers {
        scm('H/5 * * * *') // pull scm every 5 minutes
    }
    wrappers {
        nodejs('nodejs') // this is the name of the NodeJS installation in 
                         // Manage Jenkins -> Configure Tools -> NodeJS Installations -> Name
    }
    steps {
        dockerBuildAndPublish {
            repositoryName('marati643/docker-nodejs-demo') // repository where we publish
            tag('${GIT_REVISION,length=9}') // Git commit hash with a length of 9
            registryCredentials('dockerhub') // registry credentials
            forcePull(false)
            forceTag(false)
            createFingerprints(false)
            skipDecorate()
        }
    }
}
```

# Setup Docker hub credentials:

* Go to **Jenkins->Manage Jenkins->Manage credentials** click on **Global->Add credentials** 

* In **Global credentials** enter your username and password and enter **dockerhub** in the ID text input.

* Click **ok**



## Run the job:

* Open Jenkins 

* Select **Job DSL with Docker example**

* Click on **Build Now**

* The scrpit should fail with **ERROR: script not yet approved for use**, because the groovy script is not approved to use from our github repo.

* To approve the script for use go to **Jenkins -> Manage Jenkins -> In-process script approval** and click on **Approve**.

* Go back to **Job DSL with docker publish example** project and click on **Build now**
