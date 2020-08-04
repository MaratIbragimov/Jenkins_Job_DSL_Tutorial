# Jenkins Jobs DSL

A Jenkins job DSL a plugin that allows us to define/configure jenkins jobs programmatically.

## Jobs DSL plugin installation:

* Open Jenkins

* Navigate to **Manage Jenkins -> Manage plugins**, select **available** tab and insall **Jobs DSL** plugin

* Click **download now and install after restart**

* Check **Restart Jenkins when installation is completed and no jobs are running**


## Create a new jenkins job:

* Open Jenkins

* Click on **New Item**

* Select **Frestyle project**

* Enter projects name e.g **Job DSL example**

* Click ok

* In jobs configuration go to **Source management** and select **Git**

* Enter the url of the git repository that contains your Jenkins jobs DSL e.g https://github.com/marat643/Jenkins_Job_DSL_Tutorial.git

* Go to **Build** section and click on **Add a build step** and select **Process job DSLs** 
