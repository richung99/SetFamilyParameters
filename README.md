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

## Match Parameters (WIP)
Often times, families downloaded from the manufacturers will contain manufacturer parameters that need their values to be copied over to commonly shared parameters. By using string metrics to compare the parameter names provided by the manufacturer, we can automatically retrieve and populate these parameters by using the existing scripts. There are two string metrics used to evaluate string similarity in this project:
1. Levenshtein Distance
This is a basic distance algorithm that provides the total number of changes (via insertion, deletion, or substition) to get from the original string to the target string. Levenshtein distances that are lower indicate more similarity between words.
2. Fuzzy Lookup
No clue how this one works, besides that it typically performs better than Levenshtein Distances. The VBA implementation of a fuzzy lookup algorithm was taken from this [forum post](https://www.mrexcel.com/board/threads/fuzzy-matching-new-version-plus-explanation.195635/).
I'm still looking into alternative algorithms to compare string similarities, so this is far from complete. Eventually, the idea is to use some sort of combined score from several different methods. The optimal weights for these combinations could be determined from a neural net.

## License
[MIT](https://choosealicense.com/licenses/mit/)