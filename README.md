# Set Family Parameters

This project contains several Dynamo scripts that retrieve and manipulate family parameters.

## Installation

After cloning the repository, ensure that the following packages are installed in Dynamo for Revit 2018:
* [Orchid](https://github.com/erfajo/OrchidForDynamo)
* [Clockwork](https://github.com/andydandy74/ClockworkForDynamo)
* [spring nodes](https://github.com/dimven/SpringNodes)
* RIE

Verify that the following files were cloned:
* getFamilyParam18.dyn
* setFamilyParam18.dyn
* instanceToType.dyn
* setMark.dyn
* paramList.xlsm

If you choose to use my existing Revit template files for testing, verify that the MASTER folder contains
* RCMASTER18.rvt
* RC FAMILIES
	* M-AHU MZ_AnnexAir (AHU-2).rfa
	* M-Blower Coil Unit_Magicaire DUC Series.rfa
	* M-FCU Horizontal Concealed_Trane FCCB040.rfa
	* M-FCU Horizontal Concealed_Trane FCCB080.rfa
	* M-FCU Horizontal Concealed_Trane FCCB100.rfa
	* M-FCU Horizontal Concealed_Trane FCCB120.rfa

## Retrieving Parameters
getFamilyParam18.dyn can be used in conjunction with a .rvt file to retrieve all parameters and parameter values from a family. After loading a family into a .rvt file, use the drop down menu to select that family from the Dynamo script.

![getFamilyParamDrop](/images/getFamilyParamDrop.PNG?raw=true "getFamilyParam Dropdown Menu")

After running the script, all instance parameters are imported to the INSTANCE sheet of paramList.xlsm, and all type parameters are imported to the TYPE sheet.

## Set Parameters
setFamilyParam18.dyn can be used in conjunction with a .rvt to set a list of parameter values. After parameter retrieval, values can be edited in column B of sheets INSTANCE and TYPE.

![paramList](/images/paramList.PNG?raw=true "Edit parameters")

Changing values in column B will also update the DATE in column C, which can be used to filter recently edited parameters. PARAMs and VALs can be copied from the INSTANCE and TYPE sheets into columns A and B of the INPUT sheet starting from row 3.

![paramListINPUT](/images/paramListINPUT.PNG?raw=true "Edit parameters")

Split text to columns can be used in column B to remove units. Columns D and E are automatically populated. On the last used row of columns D and E, edit the cell formula to delete the extra &",".

![paramListFormat](/images/paramListFormat.PNG?raw=true "Edit parameters")

Rows A and B are autopopulated based on columns D and E. Copy rows A and B into the Code Block of setFamilyParam18.dyn and run the script.

![setFamilyParam](/images/setFamilyParam.PNG?raw=true "setFamilyParam")

## Match Parameters
Often times, families downloaded from the manufacturers will contain manufacturer parameters that need their values to be copied over to commonly shared parameters. By using string metrics to compare the parameter names provided by the manufacturer, I try to automatically retrieve and populate these parameters by using the existing values. There are two string metrics used to evaluate string similarity in this project:
1. <b> Levenshtein Distance </b> <br />
This is a basic distance algorithm that provides the total number of changes (via insertion, deletion, or substition) to get from the original string to the target string. Levenshtein distances that are lower indicate more similarity between words.
2. <b> [Fuzzy Lookup](https://www.mrexcel.com/board/threads/fuzzy-matching-new-version-plus-explanation.195635/) </b> <br />

## Instance to Type
instanceToType.dyn changes a list of instance based parameters to type based. Using getFamilyParam18.dyn, extract all parameters to paramList.xlsm. Following similar steps to Set Parameters, copy the desired parameters from the INSTANCE and TYPE sheets into column A of INPUT. Copy the list of parameters in row 1 to the code block of instanceToType.dyn.

## Setting Mark
setMark.dyn combines custom shared parameters into the default Mark parameter in Revit. In a project file, create one or more schedules containing all desired elements to be edited. In the project browser, ctrl-select one or more schedules. In setMark.dyn, switch the Boolean box from False to True, then back to False. The updated changes should now be reflected in the schedules.

## License
[MIT](https://choosealicense.com/licenses/mit/)