# Dynamic Form (UI5)

This is a component which makes up part of a library of components which each provide a dynamic control (user-interface) in JavaScript, using the OpenUI5 franework.  This component builds a responsive form (sap.ui.layout.form.SimpleForm in OpenUI5) based on configurations made in a JSON file.  The data structure modeled in JSON can also be reflected in a database, or any other structured model. 

## Prerequisites

OpenUI5 must be downloaded and extracted.  The bootstrap for this component then needs to be adapted to the location of the UI5 folder on the filesystem.  This can be done by editing the following lines of code in the index.html file, or wherever the main application bootstrap is:

```
<script src="../../../../libs/ui5/resources/sap-ui-core.js" 
  id="sap-ui-bootstrap" 
  data-sap-ui-theme="sap_belize_plus" 
  data-sap-ui-bindingSyntax="complex" 
  data-sap-ui-compatVersion="edge" 
  data-sap-ui-preload="async" 
  data-sap-ui-language="en" 
  data-sap-ui-resourceroots='{
    "dynamic.SimpleForm": "./"  }'>
</script>

```

More specifically, this line:

```
<script src="../../../../libs/ui5/resources/sap-ui-core.js" 

```

## Installing

Download the package to the host computer (desktop or server), then navigate
to the project's directory on the filesystem using a command-prompt or terminal.

```
~/DynamicTable
```

## Usage

The index.html file is not necessary, but has been included as an example of how to use the component.  The basic idea is to modify the JSON file found in the /model folder, which looks something like this:

```
{
    "record": {
        "company": {
            "customer": {
                "formContainers": [{
                    "title": "Test Title",
                    "label": "Test Label",
                    "control": {
                        "fragment": "Input",
                        "binding": {
                            "value": "data>TestField"
                        }
                    }
                },{
                    "label": "Second Label",
                    "control": {
                        "fragment": "Input",
                        "binding": {
                            "value": "data>SecondField"
                        }
                    }
                }, {
                    "label": "Third Label",
                    "control": {
                        "fragment": "Input",
                        "binding": {
                            "value": "data>ThirdField"
                        }
                    }
                }, {
                  "title": "Again",
                  "label": "Again",
                  "control": {
                    "fragment": "Input",
                    "binding": {
                      "value": "data>bind"
                    }
                  }
                }]
            }
        }
    }
}
```

Values associated with a fragment property are references to the fragments found in the /fragment folder.  These are templates for the controls which will be used to compose the form's content (title, labels, input fields, dropdown menus, etc.).  More details on the configurations can be found in the OpenUI5 library for the [sap.ui.layout.form.SimpleForm](https://sapui5.hana.ondemand.com/#/api/sap.ui.layout.form.SimpleForm).

Once the config file is maintained, the component can be called from an application like so:

```
var sMethod = "record";
var sSubject = "company";
var sClass = "customer";

var pComponent = new Promise((resolve, reject) => {
	resolve(getInstance(sMethod, sSubject, sClass, null));
}).then(function (oComponent) {
	var oControl = oComponent.getControl(sMethod, sSubject, sClass, null);
	oControl.placeAt("body");
});

```

## Built With

* [OpenUI5](https://github.com/openui5) - The user-interface framework


## Authors

* **Harrison Holland** - [Harrison's GitHub](https://github.com/hwholland)
