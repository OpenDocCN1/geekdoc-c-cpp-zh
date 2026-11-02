| CommonFileQuery | Windows Properties used in query |
| --- | --- |
| orderByNone | Sorted by the System.ItemNameDisplay property (this name is appropriate for use in UI). |
| orderBySearchRank | Sorted by the System.Search.Rank and then by System.DateModified properties. |
| orderByTitle | Sorted by the System.Title property. |
| orderByDate | Sorted by System.ItemDate, which varies with the type of file (e.g., System.Photo.DateTaken for images, System.Media.DateReleased for music). |
| orderByMusicProperties | Sorted by music properties (e.g., System.Music.AlbumTitle, System.Music.Artist, etc.). |

| CommonFolderQuery | Windows properties used in query |
| --- | --- |
| groupByType | Grouped System.ItemTypeText, with one virtual folder per type. |
| groupByTag | Grouped by System.Keywords, with one virtual folder per keyword; files with multiple tags will appear in multiple folders. |
| groupByAuthor | Grouped by System.Author, with one virtual folder per author; files with multiple authors will appear in multiple folders. |
| groupByYear | Grouped by the year in System.ItemDate, with one virtual folder per year. |
| groupByMonth | Grouped by the month in System.ItemDate, with one virtual folder per month. |
| groupByPublishedYear | Grouped by the year in System.Media.Year, with one virtual folder per year. |
| groupByRating | Grouped by System.Rating with one virtual folder per rating. |
| groupByAlbum | Grouped by System.Music.AlbumTitle with one virtual folder per title. |
| groupByArtist | Grouped by System.Music.Artist with one virtual folder per artist. |
| groupByAlbumArtist | Grouped by System.Music.AlbumArtist with one virtual folder per album artist. |
| groupByComposer | Grouped by System.Music.Composer, with one virtual folder per composer; files with multiple composers will appear in multiple folders. |
| groupByGenre | Grouped by System.Music.Genre, with one virtual folder per genre. |

Clearly, many of the common folder queries (and one common file query) apply to music specifically, but others apply much more generally. However, *not every location supports every type of file query*—those that don’t will throw a "parameter is incorrect" exception, which can be confusing if you’re not prepared for it! (This is related to the indexing status of the location in question; libraries are indexed by default.)

The way you check for support is through `StorageFolder.IsCommonFileQuerySupported` and `IsCommonFolderQuerySupported`, to which you pass the desired `CommonFileQuery` and `CommonFolderQuery` value you want to test.

To help you play with this, I’ve modified scenario 4 of the Folder enumeration sample that’s in this chapter’s companion content. I’ve added a drop-down list through which you can select which `CommonFolderQuery` to run; once you’ve chosen a folder, it also checks if the query is supported:

```
```javascript
var select = document.getElementById("selectQuery");
var selectedQuery = queries[select.selectedIndex];

if (!folder.isCommonFileQuerySupported(selectedQuery)) {
    //Show message in output if not supported and return.
    return;
}

//Run query as usual
```
```