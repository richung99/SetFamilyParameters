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
* instanceToType.dyn
* setFamilyParam18.dyn
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

## Match Parameters (WIP)
Often times, families downloaded from the manufacturers will contain manufacturer parameters that need their values to be copied over to commonly shared parameters. By using string metrics to compare the parameter names provided by the manufacturer, we can automatically retrieve and populate these parameters by using the existing scripts. There are two string metrics used to evaluate string similarity in this project:
1. <b> Levenshtein Distance </b> <br />
This is a basic distance algorithm that provides the total number of changes (via insertion, deletion, or substition) to get from the original string to the target string. Levenshtein distances that are lower indicate more similarity between words.
2. <b> Fuzzy Lookup </b> <br />
No clue how this one works, besides that it typically performs better than Levenshtein Distances. The VBA implementation of a fuzzy lookup algorithm was taken from this [forum post](https://www.mrexcel.com/board/threads/fuzzy-matching-new-version-plus-explanation.195635/).

I'm still looking into alternative algorithms to compare string similarities, so this is far from complete. Eventually, the idea is to use some sort of combined score from several different methods. The optimal weights for these combinations could be determined from a neural net.

## License
[MIT](https://choosealicense.com/licenses/mit/)