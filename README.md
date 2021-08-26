# Set Family Parameters

The purpose of this project is to simplify editing multiple family parameters across different .rfa files. This project uses two Dynamo scripts that extract and export family names and values to an Excel file, where they can be edited then reimported into the family to be saved. 

## Installation

After downloading the repository, ensure that [Orchid](https://github.com/erfajo/OrchidForDynamo) is installed in Dynamo for Revit 2018. At the minimum, your project should contain: 
* MASTER/RCMASTER18.rvt
* paramList.xlsm
* setFamilyParam18.dyn
* setFamilyParam18-2.dyn

## Usage
1. Import a family .rfa file into a .rvt file. Feel free to use RCMASTER18.rvt.
2. Run setFamilyParam18.dyn.
3. Edit the family parameters inside of paramList.xlsm.
4. Copy the input strings from the INPUT sheet into the Code Block in setFamilyParam18-2.dyn and run.
5. Edit the family and save the .rfa file back in the original location.

## License
[MIT](https://choosealicense.com/licenses/mit/)