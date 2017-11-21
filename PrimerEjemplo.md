# My first PMCode from my CSV

In this page you are going to start using PMCode without a deep knowledge of the program, uploading your own csv file to get information from your data.

*Note: If you want to learn step by step to create your own PMCode from the beginning, I refer you to this [page]() where you can create a simple project, with the explanation of each line you should add and why they should be added.*

Once [VisualStudio has been installed](), click  to download the  "[OutpatientDepartmentExample.rar]()". Extract the [compressed files](https://www.win-rar.com/download.html) and double-click on the project "OutpatientDepartmentExample.sln"; VisualStudio will open automatically.

First, open VisualStudio and, in the *Solution Explorer*  panel, open *MainWindow.xaml.cs*.

After the headers and initialize the main function, it is created the TPAs viewer:

``` csharp
// visor grafico de TPAs
TPAViewer view = new TPAViewer();
public MainWindow()
{
    InitializeComponent();
    gBase.Children.Add(view);
}
```