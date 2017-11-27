# How to upload a corpus data
In this section you could learn how to upload a corpus data file (in csv format) to get information with PMCode without a deep knowledge of this program. If you do not have idea how PMCode work, I strongly recommend you to read [First contact with PMcode](./FirstContact.md) section.

To upload any corpus in any PM tool the function needed is called [Factory](). Applying the factory we will obtain a Process Mining Log ([PMLog]()). On this object we will apply all the subsequent processing.
## Factory creation
Our Factory will be called "PMLogReader" and it is a [new visualC class]() within the current project. 
### Variables creation
In it, after all the headers, each type of elements that the Factory will identify in the .csv are declared:
```csharp
public const string SEPARADOR = "@";
public const string CABID = "ID";
public const string CABNAME = "NAME";
public const string CABACTIVITY = "ACTIVITY";
public const string CABSTART = "START";
public const string CABEND = "END";
public const string CABSAMPLE = "SAMPLE";
public const string CABRESULT = "RESULT";
```
These elements are the only ones that will be added to the PMLog and therefore the only ones that will be accessible in the rest of the program to work with and obtain information.

The variable "res" is generated, where the final result will be stored. Also the variable “csvi” is created, in which will be stored the [dictionary]() with the information of each read line (with a foreach):
```csharp
public static ProcessMiningLog FromCSV(string csv)
{
ProcessMiningLog res = new ProcessMiningLog();
CSVIterator csvi = new CSVIterator();
}
```
