# Library-Management-systemss
INTE/M/1024/09/23-Karanja Alvin Kinyua
The code is below:


#Disable Warning CA1707 ' Identifiers should not contain underscores

Imports System.Data.SqlClient

Public Class Form1
    ' Declare the connection string at the class level
    Private connectionString As String = "Data Source=LibraryManagementSystem;Initial Catalog=LibraryDB;Integrated Security=True"

    ' Method to clear the input fields
    Private Sub ClearFields()
        txtTitle.Clear()
        txtAuthor.Clear()
        txtYearPublished.Clear()
        txtGenre.Clear()
    End Sub

    ' Method to display books in the DataGridView
    Private Sub DisplayBooks()
        Using con = SqlConnection(connectionString)
            con.Dispose()
            Dim query As String = "SELECT * FROM Books"
            Dim cmd As New SqlCommand(query, con)
            Dim adapter As New SqlDataAdapter(cmd)
            Dim table As New DataTable()
                    adapter.Fill(table)
                    dgvBooks.DataSource = table
                End Using


    End Sub

    Private Function SqlConnection(connectionString As String) As IDisposable
        Throw New NotImplementedException()
    End Function

    ' Method to add a new book
    Private Sub BtnAdd_Click(sender As Object, e As EventArgs) Handles BtnAdd.Click
        Using con = SqlConnection(connectionString)
            con.Dispose()
            Dim query As String = "INSERT INTO Books (Title, Author, YearPublished, Genre) VALUES (@Title, @Author, @YearPublished, @Genre)"
            Dim cmd As New SqlCommand(query, con)
            cmd.Parameters.AddWithValue("@Title", txtTitle.Text)
                cmd.Parameters.AddWithValue("@Author", txtAuthor.Text)
                cmd.Parameters.AddWithValue("@YearPublished", txtYearPublished.Text)
                cmd.Parameters.AddWithValue("@Genre", txtGenre.Text)
                cmd.ExecuteNonQuery()
            End Using
            MessageBox.Show("Book added successfully")
            ClearFields()
            DisplayBooks()

    End Sub

    ' Method to update an existing book
    Private Sub BtnUpdate_Click(sender As Object, e As EventArgs) Handles BtnUpdate.Click
        Using con = SqlConnection(connectionString)
            con.Dispose()
            Dim query As String = "UPDATE Books SET Title=@Title, Author=@Author, YearPublished=@YearPublished, Genre=@Genre WHERE ID=@ID"
            Dim cmd As New SqlCommand(query, con)
            cmd.Parameters.AddWithValue("@ID", dgvBooks.SelectedRows(0).Cells(0).Value)
            cmd.Parameters.AddWithValue("@Title", txtTitle.Text)
            cmd.Parameters.AddWithValue("@Author", txtAuthor.Text)
            cmd.Parameters.AddWithValue("@YearPublished", txtYearPublished.Text)
            cmd.Parameters.AddWithValue("@Genre", txtGenre.Text)
            cmd.ExecuteNonQuery()
        End Using
        MessageBox.Show("Book updated successfully")
        ClearFields()
        DisplayBooks()

    End Sub

    ' Method to delete a book
    Private Sub BtnDelete_Click(sender As Object, e As EventArgs) Handles BtnDelete.Click
        Using con = SqlConnection(connectionString)
            con.Dispose() 'Open the connection
            Dim query As String = "DELETE FROM Books WHERE ID=@ID"
            Dim cmd As New SqlCommand(query, con)
            cmd.Parameters.AddWithValue("@ID", dgvBooks.SelectedRows(0).Cells(0).Value)
            cmd.ExecuteNonQuery()
        End Using
        MessageBox.Show("Book deleted successfully")
        ClearFields()
        DisplayBooks()

    End Sub

    Private Shared Function NewMethod() As String
        Return "DELETE FROM Books WHERE ID=@ID"
    End Function

    ' Method to clear the input fields
    Private Sub BtnClear_Click(sender As Object, e As EventArgs) Handles BtnClear.Click
        ClearFields()
    End Sub

    ' Load event to display books when the form loads
    Private Sub Form1_Load(sender As Object, e As EventArgs) Handles MyBase.Load
        DisplayBooks()
    End Sub

End Class




#Enable Warning CA1707 ' Identifiers should not contain underscores
