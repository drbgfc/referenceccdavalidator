This document is meant to outline the steps to successfully configure and deploy the reference ccda application.
NOTE: This project uses the reference-ccda-api project for vocabulary validation. https://github.com/siteadmin/referenceccdavalidator

1. Assumptions
    a. Tomcat 7 or above has been installed and NOT running. https://tomcat.apache.org/download-70.cgi

    b. You are using a pre-built referenceccdaservice.war file. In other words, the .war file was not built from the project directly.
        Such a thing is possible but beyond the scope of this document.

    c. With Tomcat installed and the referenceccdaservice.war in your hands, you are ready to begin configuration and deployment.

NOTE - IF THIS IS A FIRST TIME INSTALL, CONTINUE TO NUMBER 2, ELSE REMOVE THE FOLLOWING ARTIFACTS TO ENSURE YOU ARE RUNNING THE APPLICATION WITH THE LATEST CONFIGURATION
    *** ENSURE THE TOMCAT INSTANCE HAS BEEN SHUTDOWN***
    - IN THE TOMCAT/WEBAPPS DIRECTORY, DELETE REFERENCECCDASERVICE.WAR AND THE REFERENCECCDASERVICE DIRECTORY
    - IN THE VOCABULARY CONFIGURATION DIRECTORY, DELETE CCDAREFERENCEVALIDATORCONFIG.XML

2. Configuration Instructions
    There are 3 main components to this application:
        1. Artifacts needed for Vocabulary Validation
        2. The war
        3. Server (tomcat) configuration

    Vocabulary Artifacts
        1. Create a directory that will hold the vocabulary artifacts. For example, E:\Development\Environment\VocabularyConfiguration
            a. this folder will contain the needed vocabulary configuration files

        2. Place the ccdaReferenceValidatorConfig.xml in this folder. For example, E:\Development\Environment\VocabularyConfiguration\ccdaReferenceValidatorConfig.xml

        3.Download the code repository and valueset repository and place them (OR OVER-WRITE IF THEY ALREADY EXIST) in this directory. For example,
            a. E:\Development\Environment\VocabularyConfiguration\Vocabulary\code_repository
            b. E:\Development\Environment\VocabularyConfiguration\Vocabulary\valueset_repository\VSAC

    The referenceccdaservice.war
            1. Navigate to the webapps directory in your Tomcat instance. For example, E:\Development\Environment\servers\apache-tomcat-7.0.57\webapps

            2. Place the referenceccdaservice.war file here


    Server Configuration
            1. Place a copy of referenceccdaservice.xml in $CATALINA_BASE/conf/[enginename]/[hostname]/. For example, E:\Development\Environment\servers\apache-tomcat-7.0.57\conf\Catalina\localhost
            2. Edit the referenceccdaservice.xml key values to point to the locations configured in the previous steps. For example;

            Context reloadable="true">
                <Parameter name="vocabulary.localCodeRepositoryDir" value="E:/Development/Environment/VocabularyConfiguration/Vocabulary/code_repository" override="true"/>
            	<Parameter name="vocabulary.localValueSetRepositoryDir" value="E:/Development/Environment/VocabularyConfiguration/Vocabulary/valueset_repository" override="true"/>
            	<Parameter name="referenceccda.configFile" value="E:/Development/Environment/VocabularyConfiguration/ccdaReferenceValidatorConfig.xml" override="true"/>
            </Context>

3. Run the application instructions
    1. Start your tomcat instance - you should see output showing the databases getting initialized and the .war file getting deployed.
    NOTE: Allow a few moments for the vocabulary valuesets and codes to be inserted into the in-memory database.

    2. Access the endpoint. For example, localhost:8080/referenceccdaservice/
