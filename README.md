wordlists
=========
•1 Button 
•1 RichTextBox 

 

 

Option Strict On
Option Explicit On
Option Infer Off

Public Class Form1

 Dim wordList As New List(Of String)

 Private Sub Button1_Click(ByVal sender As System.Object, ByVal e As System.EventArgs) Handles Button1.Click

  Dim fileContent As String = ""

  Using ofd As New OpenFileDialog
   ofd.InitialDirectory = My.Computer.FileSystem.SpecialDirectories.MyDocuments
   ofd.Filter = "Text files only|*.txt"

   Dim result As DialogResult = ofd.ShowDialog
   If result = Windows.Forms.DialogResult.OK And ofd.FileName <> String.Empty Then
    fileContent = My.Computer.FileSystem.ReadAllText(ofd.FileName)
   End If

  End Using

  If fileContent <> String.Empty Then
   Dim fileLines() As String = fileContent.Split(System.Environment.NewLine.ToCharArray, System.StringSplitOptions.RemoveEmptyEntries)
   Dim splitChars() As Char = (" `1234567890-=[];'#\,./€¬!£$%^&*()_+{}:@~|<>?" & """").ToCharArray
   wordList = fileContent.Split(splitChars, System.StringSplitOptions.RemoveEmptyEntries).ToList
  End If

  RichTextBox1.Lines = wordList.ToArray

 End Sub
End Class
