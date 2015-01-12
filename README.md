Utility Structure Exchange Format
===================================

This project provides the schema definitions to enable the exchange of structure definitions among different utility companies wishing to share the information in a generic manner. 

Overview
----------

Currently the standard is a JSON based schema definition.  JSON was chosen because of its simplicity and ubiquitiy.  It is very readable and can be constructured with nothing more than a text editor.  This allows for the standard to be truely platform agnostic.

### Design Philosphy

1. Exchange file content should be human readable.
1. The definition files should be as self documenting as possible.

### Concepts

1. If you are not familiar with JSON.  Try this short [tutorial](http://www.w3schools.com/json/default.asp).

How to Contribute
------------------

We will be using the "fork and pull" workflow, github has excellent [documentataion](https://help.github.com/articles/using-pull-requests/) on the this process of doing public collaboration.    We will be using method here.

In general any pull request will be reviewed for following criteria:

1. Constancy with the rest of the standard - Is the variable naming and structure similar to the rest of the schema?  
2. General usefulness of the feature - Is it of general use to the industry or specific to a particular vendor?
3. Documention provided - Are the relevant readme's and descriptions provided for user clarity?
4. Testing - has the appropriate test cases been provided to ensure expected behavior.

Validation
===========

Command Line
------------

We include a command line validator to validate against any of our included schemas. To run the command, use the validateJson gradle task

    gradlew :validateJson -Pschema=/path/to/schema -PjsonFile=/path/to/json
    schema - path to schema starting from resources. eg. /v1/schema/spidacalc/calc/structure.schema
    json - json file to be validated.

For example, to validate the "one of everything" structure example, from the schema directory you would type:

    gradlew :validateJson -Pschema=/v1/schema/structure/structure.schema -PjsonFile=resources/v1/examples/designs/one_of_everything.json

The tool uses the included Validator java class.

External
---------

If you are in need of actually validating some JSON data against the schema there several options depending on your language.  The one we use in our tests is the excellent library by [fge](https://github.com/fge/json-schema-validator).  It gives very good validation errors and also does all the references for you, so there is no need to load all the linked schema.  You will also notice in our tests we use a namespace of a file system.  This could be any location you put the file, you could even use a "resource:/" uri for referencing in a jar.

Another lightwight option is the javascript based validator located here http://geraintluff.github.io/tv4/

