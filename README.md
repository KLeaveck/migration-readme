***The included source code, service, and the information is provided as is, and OmniUpdate makes no promises or guarantees about its use or misuse. The source code provided is recommended for advanced users and may not be compatible with all implementations of OU Campus.***

**This tool is only meant to migrate organic WordPress content.**  
**This tool is not meant to migrate content inside of plugins or other applications.**

# Ruby Migration Script For XML Exported Wordpress Content into OU Campus. 
-This script will allow users to migrate their WordPress content into OU campus. 

## Setting up Simple Site
This package contains code for a small sample website that can be used in OU Campus and will be to destination for your migrated WordPress content. 
### Installation
1. Navigate to https://github.com/omniupdate/example-code-simple-site#simple-site and download simple site as a Zip file.
2. Upload Zip file to the root in your OU site.
3. After upload Publish all files.
4. Navigate to the published pages and see if the content renders correctly.
5. If the simple site is on a C# server then configure the ASP includes in the functions.xsl file. Also change PCF extensions via find and replace to desired extension

## Exporting Wordpress Content. 
1. Starting in your WordPress dashboard navigate to mysite --> settings and then select "Export". On the next screen, you will have the option to export your entire site or pick and choose which elements you would like to export. Once desired elements have been chosen, click "Down Load Export File" button and an xml file of the WordPress site content will be downloaded. 

## Setting up the migration process. 
1. Download this complete migration folder from GitHub. 
2. Copy the xml file generated from the previous task into the ou-migration-tool --> "source" folder.
3. If you will be using a **migration map** during this process copy the migration-map.csv into the ou-migration-tool --> migration_maps folder 


## Configuring the migration process. 
###### 1. In the root of ou-migration-tool open the config.rb file in a text editor.

#### 2. Mapping Toogle

At the top of the config.rb file there is a mapping toggle section. 

-If you have uploaded a CSV and are using a migration map then this section should be uncommented

MAP = "yes"

-If you are not using a migration map and will be strictly migration from your xml source only then this section should be uncommented

MAP = "no"

#### 3. SOURCE_URL_BASE
As we migrate individual page content into OU campus we will target the <link></link> nodes in the xml source and use these as the new file paths for the carried over pages. Because the URL will an absolute path of the old WordPress site we will need to clean up the URL and remove the website root. In our example source, one of the link nodes contains the URL. 


`<link>https://www.gallena.edu/academics/library</link>`


By entering https://www.gallena.edu into the SOURCE_URL_BASE variable 


https://www.gallena.edu/academics/library
 
Will become...

academics/library 

After we upload the new pages to OU Campus they will have a full URL of 

http://dev.yourOUsite.edu/academics/library.pcf

#### 4. Template Path
For this tutorial, we suggest using the default templates. 

#### 5. Logs
For this tutorial, we suggest using the default logs and log paths. 

#### 6. MIGRATION_MAP_PATH
If you are using a migration map then update this variable to point to the location of the CSV map you uploaded previously. If not using a map you can skip this step. 

#### 7. WP_SOURCE_FILE 
If using a source other then the one provided in our example you will need to update this variable to match the name of your xml export file that you copied to the source folder. 

#### 8. OUTPUT_EXTENSION 
Update this variable to reflect the language your OU server uses. 

#### 9. INDEX_NAME 
Update this variable to be "index" if server language is PHP or "default" if server language is ASP 

#### 10. WP_PLUGIN_CODE_DISPLAY
These configurations give users a variety of options on how to deal with WordPress plugin tags. 

#### 11. Adjusting def process_rows_from_csv(row, i, xml_doc) function
If using a migration map you may need to configure the def process_rows_from_csv(row, i, xml_doc) function to reflect the setup of your migration-map.csv. Navigate to migrate_from_wordpress.rb file and scroll down until you locate the def process_rows_from_csv(row, i, xml_doc) function. Inside of the function, there are 3 variables that need to be updated if they are not already pointing to the correct index on your migration map.

  orig_path = row[0]
  
  ex: academics/library 
  
  new_path = row[1]
  
  ex: academics/library 
  
  template = row[2]
  
  ex: interior.pcf

## Running the migration process. 

1. Open a terminal 

2. Navigate to your migration folder.

3. Enter "ruby migrate_from_wp.rb"

 ## Uploading to OU Campus.
1. After you have run your script and generated your output files, move them into a zip file. 
2. Navigate to the desired location in a site in OU Campus. 
3. Click upload and choose the **Import Zip File** option. 
4. Choose the start upload button and check to make sure there are no errors. 
5. Click the upload button. 
6. Open newly uploaded files in preview mode and check that the desired content was transferred. 
7. Publish out the uploaded folder and correct any errors that may have been reported during the publishing process. 

 ## Trouble Shooting. 
If you are missing content after uploading to OU campus 
1. Check the various migration log files. 
2. Make sure you exported the desired elements in your WordPress export. 
3. Republish in OU and look for the errors log after publish completes. 
