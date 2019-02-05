***The included source code, service and information is provided as is, and OmniUpdate makes no promises or guarantees about its use or misuse. The source code provided is recommended for advanced users and may not be compatible with all implementations of OU Campus.***

# Ruby Migration Script For XML Exported Wordpress Content into OU Campus. 
- This script will allow uses to migrate their wordpress content into OU campus. 

## Exporting Wordpress Content. 
 1. Starting in your wordpress dashboard navigate to mysite --> settings and then select "Export". On the next screen you will have the option to export your entire site or pick and choose which elements you would like to export. Once desired elements have been chose click the export button and a xml file of the wordpress site content will be downloaded. 

## Setting up the migration process. 
 1. Download this complete migration folder from github. 
 2. Copy the xml file generated from the previous task into the ou-migration-tool --> "source" folder.
 3. If you will be using a **migration map** during this process upload the migration-map.csv into the ou-migration-tool --> migration_maps folder 


## Configuring the migration process. 
###### 1. In the root of ou-migration-tool open the config.rb file in a text editor.

#### 2. Mapping Toogle

At the top of the config.rb file there is a mapping toggle section. 

-If you have uploaded a csv and are using a migration map then this section should be uncommented

MAP = "yes"

-If you are not using a migration map and will be strictly migration from your xml source only then this section should be uncommented

MAP = "no"

#### 3. SOURCE_URL_BASE
As we migrate individual page content into OU capus we will target the <link></link> nodes in the xml source and use these as the new file paths for the carried over pages. Because the URL will a absolute path of the old wordpress site we will need to clean up the url and remove the website root. In our example source one of the link node contains the URL. 


`<link>https://www.gallena.edu/academics/library</link>`


By entering https://www.gallena.edu into the SOURCE_URL_BASE variable 


https://www.gallena.edu/academics/library
 
  
<br> Will become...

academics/library 

After we upload the new pages to OU Campus they will have a full URL of 

http://dev.yourOUsite.edu/academics/library.pcf


#### 4. WP_SOURCE_FILE 
If using a source other then the provided in our example you will need to update this variable to match the name of your xml export file that you copied to the source folder. 

#### 5. OUTPUT_EXTENSION 
Update this variable to refelct the language your OU server uses. 

#### 6. INDEX_NAME 
Update this vairable to be "index" if server language is PHP or "default" if server language is ASP 

#### 7. Adjusting def process_rows_from_csv(row, i, xml_doc) function
If using a migration map you may need to configure the def process_rows_from_csv(row, i, xml_doc) funciton to refelect the setup of your migration-map.csv. There are 3 variabes that need to be updated if they are not pointing to the correct index on your migration map.

  orig_path = row[0]
  
  new_path = row[1]
  
  template = row[2]

## Running the migration process. 

1. Open a teriminal 

2. Navigate to your migration folder.

3. Enter "ruby migrate_from_wp.rb"

 
