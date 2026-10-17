```
$Row = 4;
$Count = 0;
foreach $Food (@GroupA, @GroupB) {
    printf(" %-15s", $Food);
    $Count++;
    if($Count == $Row) {
        print($NL);
        $Count=0;
    }
}
print($NL. $NL . "=" x 60 . $NL);
#Create the references
$GroupARef = \@GroupA;
$GroupBRef = \@GroupB;
#2. Pass the references to the function that compares the groups
$ResultArray = compareGroups($GroupARef, $GroupBRef);
#4 Print the first item in the dereferenced array
print "$NL Number of matches: @$ResultArray[0]": ";
#5 Dereference individual items.
for($Itr = 0; $Itr < @$ResultArray[0]; $Itr++)
{
    print "$NL $$ResultArray[1]->[$Itr]";
}
print($NL. $NL . "=" x 60 . $NL);
#======================================================================
#3 --------- Definition of compareGroups() ------------
#compareGroups(@Array , @Array)
sub compareGroups{
    ($xArray, $yArray) = @_;
    $Count = 0;
    foreach $ItemA (@$xArray)
    {

```