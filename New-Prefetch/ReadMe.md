# New-Prefetch

This PowerShell cmdlet creates a [prefetch](http://developer.bigfix.com/action-script/reference/download/prefetch.html) command to download and verify a file in [IBM BigFix](http://www.ibm.com/security/bigfix) actionscript:

```actionscript
prefetch <name> sha1:<sha1> size:<size> <url> [sha256:<sha256>]`
```

To create the command, the cmdlet downloads the file specified by the `Url` parameter to the folder location specified by the `DownloadLocation` parameter; it then calculates the [SHA-1](http://en.wikipedia.org/wiki/SHA-1) and size of the downloaded file.

## Syntax

```powershell
New-Prefetch -Url <url> [-PrefetchName <prefetch name>] [-DownloadFolder <download folder>] [-ForceDownload] [-IsPrefetchItem]
```
Where:
* `Url` is the complete url of the file to be downloaded
* `PrefetchName` is the name the prefetch command should use to download the file as
* `DownloadFolder` is the download location for the file (default is `%TEMP%`, which is normally the `C:\Users\<current user>\AppData\Local\Temp` folder
* `ForceDownload` specifies whether or not to force the download (by default, if a file with the same name already exists in `DownloadFolder`, it is not re-downloaded)
* `IsPrefetchItem` re-formats the prefetch command as an [add prefetch item](http://developer.bigfix.com/action-script/reference/download/add-prefetch-item.html) command

## Examples

To create a [prefetch](https://developer.bigfix.com/action-script/reference/download/add-prefetch-item.html) command to download [this picture of Hodor](http://i.imgur.com/YAUeUOG.jpg):

```powershell
New-Prefetch http://i.imgur.com/YAUeUOG.jpg
```
This creates the following command:

```
prefetch YAUeUOG.jpg sha1:ce842e0af799f2ba476511c8fbfdc3bf89612dd0 size:57656 http://i.imgur.com/YAUeUOG.jpg sha256:74f69205a016a3896290eae03627e15e8dfeba812a631b5e0afca140722a322b
```
### Optional: Specifying a Different Name

To download the file as `hodor.jpg`:

```powershell
New-Prefetch http://i.imgur.com/YAUeUOG.jpg -Name hodor.jpg
```

This creates the following command:

```
prefetch hodor.jpg sha1:ce842e0af799f2ba476511c8fbfdc3bf89612dd0 size:57656 http://i.imgur.com/YAUeUOG.jpg sha256:74f69205a016a3896290eae03627e15e8dfeba812a631b5e0afca140722a322b
```

### Optional: Add to Prefetch Block

To download:

```powershell
New-Prefetch http://i.imgur.com/YAUeUOG.jpg -Name hodor.jpg -IsPrefetchItem
```

This creates the following command:

```
add prefetch item name=hodor.jpg size=57656 sha1=ce842e0af799f2ba476511c8fbfdc3bf89612dd0 url=http://i.imgur.com/YAUeUOG.jpg sha256=74f69205a016a3896290eae03627e15e8dfeba812a631b5e0afca140722a322b
```
