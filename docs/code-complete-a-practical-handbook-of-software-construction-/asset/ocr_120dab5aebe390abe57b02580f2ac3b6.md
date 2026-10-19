```
If FindFile( fileList( fileIndex ), fileToPurge ) Then
    If OpenFile( fileToPurge ) Then
        If OverwriteFile( fileToPurge ) Then
            If Not Erase( fileToPurge ) Then
                errorState = FileStatus_FileEraseError
            End If
        Else ' couldn't overwrite file
            errorState = FileStatus_FileOverwriteError
        End If
    Else ' couldn't open file
        errorState = FileStatus_FileOpenError
    End If
Else ' couldn't find file
    errorState = FileStatus_FileFindError
End If
Wend
DeletePurgeFileList( fileList, numFilesToPurge )
End Sub
```

This line is 13 lines away from the If statement that invokes it.

For people used to programming without gotos, this code might be easier to read than the goto version, and if you use it, you won’t have to face an inquisition from the goto goon squad.

Cross-Reference For more details on indentation and other coding layout issues, see Chapter 31, "Layout and Style." For details on nesting levels, see Section 19.4, "Taming Dangerously Deep Nesting."

The main disadvantage of this nested-if approach is that the nesting level is deep, very deep. To understand the code, you have to keep the whole set of nested ifs in your mind at once. Moreover, the distance between the error-processing code and the code that invokes it is too great: the code that sets errorState to FileStatus_FileFindError, for example, is 13 lines from the if statement that invokes it.

With the goto version, no statement is more than four lines from the condition that invokes it. And you don’t have to keep the whole structure in your mind at once. You can essentially ignore any preceding conditions that were successful and focus on the next operation. In this case, the goto version is more readable and more maintainable than the nested-if version.

# Rewrite with a status variable

To rewrite with a status variable (also called a state variable), create a variable that indicates whether the routine is in an error state. In this case, the routine already uses the errorState status variable, so you can use that.

# Visual Basic Code That Avoids gotos by Using a Status Variable

```
* This routine purges a group of files.
Sub PurgeFiles( ByRef errorState As Error_Code )
    Dim fileIndex As Integer
    Dim fileToPurge As Data_File
    Dim fileList As File_List
    Dim numFilesToPurge As Integer

    MakePurgeFileList( fileList, numFilesToPurge )

    errorState = FileStatus_Success
    fileIndex = 0
```