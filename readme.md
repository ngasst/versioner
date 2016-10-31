# graphml-schema-generator
A tool to generate TypeScript interfaces from graphml graphical files.
This tool has a very specific use-case. While it's not for everyone, I believe it to be easy enough to modify to suit similar needs.

## Usage
(Make sure you read the use-case and caveats sections below!)

### Global Install
    npm install -g graphml-schema-generator

To have the wizard assist you with questions, type:
    gschema
And answer the questions until finished.

Alternatively, you can use the following syntax:
    gschema <path/to/graphml/file> <path/to/out/directory>
The paths can be either relative or absolute. The tool should pick on it either way.


### Local Install
    npm install --save graphm-schema-generator

You can either type the whole path to the file each time, such as:
    ./node_modules/gml-to-typescript/build/index
Or you can create an npm script that references the path

However you choose to go about it, the usage is exactly the same as stated in the Global Install section. Please refer to that.

If you don't want to pollute your development environment this might be a better way to install this. Then you can use npm scripts to alias it to a more manageable command.

## Use case
The generator is intended to transform a graphml file generated by tools such as [yWork Yed](http://www.yworks.com/yed).

For instance the following entity defined graphically using yEd translate to the typescript code just underneath it.

<img src="./entity.png" style="align: center" width="25%" height="25%"/>

    import { ObjectID } from 'mongodb';

    interface User {
        _id?: ObjectID;
        username: string;
        password: string;
        email: string;
    }

This code will be saved into the directory of your choosing with this naming convention: entities.interface.ts. The interface name itself will be the singular version of entities.

Like I said, this is very specific, but the whole goal of this was to avoid the arduous task of having to do the work twice. 
This way, the whole schema can be defined inside a tool such as yEd and the interfaces are generated automatically.

## Caveats
There are a few things to take into consideration before using this module.
* Only works with yEd and TypeScript. Should there be any type of interest in this, I don't mind expanding the scope, but I first developed this for my own use and it suits them just fine.
* Inside of yEd, you need to use the first type of node inside of "Entity Relationship" category. This is because this node allows for two labels (one for the entity name, and one for the parameters).

## TODO:
* Generalize usage to more graphml tools
* Generalize to output to vanilla JS, perhaps to mongoose schemas?