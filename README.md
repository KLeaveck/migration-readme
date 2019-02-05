***The included source code, service and information is provided as is, and OmniUpdate makes no promises or guarantees about its use or misuse. The source code provided is recommended for advanced users and may not be compatible with all implementations of OU Campus.***

# Ruby Migration Script For XML Exported Wordpress Content into OU Campus. 
- This script will allow uses to migrate their wordpress content into OU campus. 

## Exporting Wordpress Content. 
1. Starting in your wordpress dashboard navigate to mysite --> settings and then select "Export". 
You will be provided with a XML file.

## Setting up the migration process. 
1. Download the complete migration folder from github. 
2. Copy the xml file generated from the previous task into the ou-migration-tool --> source folder.
3. If you will be using a "migration map" during this process upload the migration-map.csv into the ou-migration-tool --> migration_maps folder 


## Configuring the migration process. 
###### 1. In the root of ou-migration-tool open the config.rb file in a text editor.

#### 2. Mapping Toogle

At the top of the config.rb file there is a mapping toggle section. 

-If you have uploaded a csv and are using a migration map then this section should be set to 

MAP = "yes"

-If you are not using a migration map and will be strictly migration from your xml source only then this section should be set to 

MAP = "no"

#### 3. SOURCE_URL_BASE
The <link> node in your xml soucres will be a absolute source URL. Becuase that URL will be different when uploading your content to OU campus we need to remove it. In our example the base url is https://www.gallena.edu however yours will be different unless you are usings our xml source. 

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

 
