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
1. In the root of ou-migration-tool open the config.rb file in a text editor.
#### 2. Mapping Toogle

At the top of the config.rb file there is a mapping toggle section. If you have uploaded a csv and are using a migration map then this section should be set to.

      MAP = "yes"

    If you are not using a migration map and will be strictly migration from your xml source only then this section should be set to.

     MAP = "no"

#### 3. SOURCE_URL_BASE



