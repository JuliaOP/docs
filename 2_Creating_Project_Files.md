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

## Generating Project Files

The file is simple and pratical. But if you want a *Project File* generator, you can access our [platform](https://appstart.kingofcode.com.br/) (on alpha) and click "Download as YML" after create the models of your project.

We want to create one friendly and installable UI to generate the files on the future.