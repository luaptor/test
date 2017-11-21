# First contact with PMcode

In this section you will start learning how to use PMCode by performing a general main program reading. Following sections will teach you [how to upload your own csv file](./How_to_upload_CSV.md) and start using PMCode to get information from your data.

*Note: If you want to learn step by step to create your own PMCode from the beginning, I refer you to [this page]() where you can create a simple project, with the explanation of each line you should add and why they should be added.*

## TPA viewer creation
Once [VisualStudio has been installed](), you should download the Outpatient Department Example: [ODExample.rar](). Extract the [compressed files](https://www.win-rar.com/download.html){:target="_blank"} and double-click on the project "OutpatientDepartmentExample.sln"; VisualStudio will open automatically.

First, open VisualStudio and, in the [*Solution Explorer*]()  panel, open [*MainWindow.xaml.cs*]().

After the headers and initialize the main function, it is created the [TPA viewer]():

``` csharp
// TPA graphical viewer
TPAViewer view = new TPAViewer();
public MainWindow()
{
    InitializeComponent();
    gBase.Children.Add(view);
}
```
Now it is [created a button]() ("bexp1_Click") as follows:
``` csharp
private void bexp1_Click(object sender, RoutedEventArgs e)
{
}
```
Within this button will take place all the steps of the rest of the example:
* Filtros indeterminados
* Log Factory
* …

## Log Factory
The first button funtionality is to load the csv relevant fields. To do that, the "CSV" variable will contain the name of the file on which we are going to work. In this case "OutpatientDepartment.csv".

Then the file will be read using a [Factory]() to generate a [Log](). Remember that, to do so, the .csv file must be [correctly labelled]() according to our own Factory function. Therefore, we have created the Log of the .csv that will be used to work on the rest of the program.
``` csharp
string CSV = "OutpatientDepartment.csv";

// Generate a Log using a CSV Factory
ProcessMiningLog pml = PMLogReader.FromCSV(CSV);
```
That Factory has been created within the same project since it has to be ad hoc for each csv.

## Filtros indeterminados
_**CARLOS: lo siguiente no sé qué quiere decir:**_
``` csharp
// Aplicamos filtro de muestras solo coge las que van de x a y
pml = new SplitLogFilter(0, 100).ProcessLog(pml);
pml = new SequencializeActivities2().ProcessLog(pml); 
```
## PALIA Inference
Now, the Log scheme is inferred using Palia algorithm, and the nodes are distributed along the screen:
``` csharp
 // PALIA is applied to the LOG
    PALIAAlgorithm pa = new PALIAAlgorithm();
    TPATemplate tpa = pa.InfiereEsquema(pml);

    TPATemplateGUI tpagui = new TPATemplateGUI(tpa);
    tpagui = new SpringForcesLayout(500, 10, 10).CalculateLayout(tpagui);
```
# Statistics and colormap
The statistics are obtained and the nodes and transitions are coloured according to the statistics:
``` csharp
//Statistics obtention
InferredTPA inf = new InferredTPA(tpagui.data);
inf.CalculaStats();

view.ShowTPATemplate(inf);

//Colour nodes by activity duration
NodeColorRenderHandler<ActivityDurationAttribute> nc = new NodeColorRenderHandler<ActivityDurationAttribute>()
{
    SatHigh = 1,
    SatLow = 0
};
nc.Render(view.tve);

//Colour transitions by execution number
TransitionColorRenderHandler<ExecutionsNumberAttribute> tc = new TransitionColorRenderHandler<ExecutionsNumberAttribute>()
{
    SatHigh = 1,
    SatLow = 0
};
tc.Render(view.tve);
```
