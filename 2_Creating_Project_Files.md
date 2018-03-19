# Creating Project Files

The *Project File* is a YAML file (*.yml) that describes all the models, fields and relationships of a project. Here you can see a simple example:

```yml
name: Inventory Control
models:
    product:
        fields:
            name:
                type: string,128
                element: text
                validation: required
                searchable: true
            type:
                type: enum
                items: physical,digital|Is digital?,undefined
                default: physical
                validation: required
        belongsTo:
            brand:
                element: select
                validation: required
        hasMany:
            grid:
                element: simple-datagrid
    
    # ...
```

## The Project File structure

The basic *Project File* structure is represented below:

```yml
name: Project Name
models:
    model_name:
        fields:
            field_name:
                # field attributes
        belongsTo:
            model_name:
                # relationship attributes
        belongsToMany:
            model_name:
                # relationship attributes
        hasOne:
            model_name:
                # relationship attributes
        hasMany:
            model_name:
                # relationship attributes
    
    # ...
```

Let's understand each level of the file.

### The Main level

The Main Level is the first level of the file, it supports, at this moment, three types of attributes:

Name|Description|Obligatory?
----|-----------|-----------
name|The project name|Yes, if not specified, you need to specify the name during the project generation with argument *--name*
index|Project index, can be used to identify the project. It is like the name, and can be used for automatizated generators|No
models|The models array, we will explain more below|Yes, for "--generate project", but No for "--generate model"

Example:

```yml
name: My First project
index: my_first_project123
models:
    # the models array ...
```

### The Models Level

On this level, each model is represented as a new sub-level of the models level:

```yml
models:
    first_model: # It is the model name on singular
        # ...
    second_model:
        # ...
```

Each model accepts these attributes:

Name|Description|Obligatory?|Accepted Values
----|-----------|-----------|---------------
fields|The array of fields, see below|Yes|Fields Array
namePlural|The model name on plural|No, because PWC will automatically convert the model name to plural (English). But in some languages, you will need to specify the plural.|Strings
description|The model description. It can be used for Views Titles. You can pass it on the format ```Singular|Plural```, Eg: ```User|Users```.|No, PWC will automatically create it based on model name. But some languages different from english needs to specify this attribute.|Strings, format: ```Singular|Plural```
onlyModel|This attribute specifies that the generator will not generate main CRUD for this model. Eg: this model is item in an order, then you specify onlyModel:true, it will not generate CRUD views for item. So, in the Order model, you will create a relationship hasMany(item), with the element: datagrid.

### The Fields Level

On this level, each field is represented as a new sub-level of the *model* level:

```yml
fields:
    first_field: # It is the field name
        # ...
    second_field:
        # ...
```

Each model accepts these attributes:

Name|Description|Obligatory?|Accepted Values
----|-----------|-----------|---------------
type|Specifies the field type. Format: ```Type|Size?```|Yes|The default values are: ```string```, ```text```, ```integer```, ```decimal```, ```boolean```, ```date```, ```datetime```, ```timestamp```, ```time```, ```enum```, ```file```, ```image```

## Generating Project Files

The file is simple and pratical. But if you want a *Project File* generator, you can access our [platform](https://appstart.kingofcode.com.br/) (on alpha) and click "Download as YML" after create the models of your project.

We want to create one friendly and installable UI to generate the files on the future.