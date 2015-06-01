

[Active Directory](#ActiveDirectory) |  [PSDrives](#PSDrives) | [File Administration](#FileAdministration)
[Output](#Output) | [GIT](#GIT) | [Control and Escape Characters](#ControlCharacters)

<a name="ActiveDirectory"></a>
# Active Directory

## User Administration

### Get a list of groups a user is in

    Get-ADPrincipalGroupMembership 61408a | select name

### Check if AD user exists

    $ADUser = Get-ADUser -Filter {SamAccountName -eq $User.Name}

<ul>
	<li>If user does not exist, $ADUser will be $null</li>
	<li><a href="http://social.technet.microsoft.com/wiki/contents/articles/12037.active-directory-get-aduser-default-and-extended-properties.aspx">Get-ADUser Default and Extended Properties</a></li>
</ul>

### Group Administration

#### Get members of a group
    Get-ADGroupMember GROUPNAME | select name

#### Add user to a group
    Add-ADGroupMember "GroupNAME" -Member USERNAME

#### Remove a user from a group

remove-adgroupmember "GroupNAME" -Member USER_NAME

#### Find names of groups containing a string

    Get-ADGroup -Filter {name -like "*STRING*"} | select name

### ACL - Access Control List

#### Get ACL for a folder

    get-acl | format-list
<a href="https://technet.microsoft.com/en-us/library/ff730951.aspx">Working with Security Descriptors</a>



<a name="PSDrives"></a>
# PSDrives

## Create a PSDrive

    New-PSDrive -PSProvider filesystem -Root FILE_PATH -Name NAME_FOR_DRIVE

#### List filesystem PSDrives

	Get-PSDrive -PSProvider filesystem

#### Push/Pop Location - Save location, switch to a different location, then return to original location

###### Push current location onto the stack (alias for Push-Location)

	pushd

###### cd to new location and do some work

	cd NEW_PATH

###### Pop previous location off the stack (alias for Pop-Location)

	popd

#### Delete a drive

	Remove-PSDrive -Name DRIVE_PATH

#### Mount a network drive - Create a PSDrive

	New-PSDrive -PSProvider filesystem -Root FILE_PATH -Name NAME_FOR_DRIVE

#### List PSDrives

	Get-PSDrive -PSProvider filesystem    

<a name="FileAdministration"></a>
# File Administration

#### Search files in a folder for a text pattern

	Get-ChildItem -recurse | Select-String -pattern "dummy" | group path | select name

<a name="Output"></a>
# Output

#### Append to a file

	... | out-file <FILENAME> -append</code>

#### Create new file with same name

	... | out-file <FILENAME> -force</code>

<a name="GIT"><h1>GIT with Powershell</h1></a>

- Install Windows Git software
- Install <a href="https://github.com/dahlbyk/posh-git">posh-git</a></li>

Resource : <a href="http://git-scm.com/book/en/v2/Git-in-Other-Environments-Git-in-Powershell"> Git in Powershell</a><br>

<a name="ControlCharacters"></a>
# Control and Escape Characters

<div class="row">
    <div class="col-md-6">
    <table class="table table-striped">
      <tr>
        <th>Character</th>
        <th>Description</th>
      </tr>
      <tr>
        <td>`0</td>
        <td>Null</td>
      </tr>
      <tr>
        <td>`a</td>
        <td>Alert bell/beep</td>
      </tr>
      <tr>
        <td>`b</td>
        <td>Backspace</td>
      </tr>
      <tr>
        <td>`f</td>
        <td>Form feed (use with printer output)</td>
      </tr>
      <tr>
        <td>`n</td>
        <td>New Line</td>
      </tr>
      <tr>
        <td>`r</td>
        <td>Carriage Return</td>
      </tr>
      <tr>
        <td>`r`n</td>
        <td>Carriage return + New line</td>
      </tr>
      <tr>
        <td>`t</td>
        <td>Horizontal tab</td>
      </tr>
      <tr>
        <td>`v</td>
        <td>Vertical tab (use with printer output)</td>
      </tr>
      <tr>
        <td>``</td>
        <td>To avoid using a Grave-accent as the escape character</td>
      </tr>
      <tr>
        <td>`#</td>
        <td>To avoid using # to create a comment</td>
      </tr>
      <tr>
        <td>`'</td>
        <td>To avoid using ' to delimit a string</td>
      </tr>
      <tr>
        <td>`"</td>
        <td>To avoid using " to delimit a string</td>
      </tr>
    </table>
  </div>
</div>

Resource : <a href="http://ss64.com/ps/syntax-esc.html">Escape characters, Delimiters and Quotes</a><p>
