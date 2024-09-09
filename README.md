# apex-vue-js

## About

This example shows how to embed the VueJS code (application) into Oracle APEX static region, with the possibility to interact between APEX component (in this case, it is Classc Report) and VueJS form.

## Working Example

https://apex.oracle.com/pls/apex/f?p=174363

https://www.youtube.com/watch?v=v1UgCs4nNo8

## Installation

Perform the following steps:

1. Install the OEHR sample schema in your APEX workspace (SQL Workshop > Utilitites > Sample Datasets).
2. Import the APEX application, provided within "apex" subfolder of this repository.
3. Import three files, provided in the "workspace_files" subfolder of this repository, in the Workspace files section of the Shared Components by creating a "Vue" sub-folder and placing files in it.

## Usage

1. Goto page 2.
2. By clicking the link in the Classic report on the left-hand side, you will open the VueJS form on the right side.
3. By clicking the VueJS button "Submit to Database" on the right-hand side, you will commit changes and refresh the classic report.
4. By clicking the "CHANGE THEME COLOR" in the APEX region, the VueJS region look and feel will slightly change.

## References

The source code of the Vue application in provided in the "source" subfolder of this repository.

## Credits

By courtesy of:
* marko.copic@fadata.eu
* lazar.bajic@fadata.eu
* marko.arsic@fadata.eu
